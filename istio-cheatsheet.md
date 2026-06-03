# Istio cheatsheet

## Component definitions

### envoy
**Envoy** is the high-performance L4/L7 proxy that Istio uses as its data plane. Every network interaction inside the mesh passes through an Envoy process. Istio never modifies Envoy's source code; instead it drives Envoy entirely through the **xDS API** (Listener Discovery Service, Route Discovery Service, Cluster Discovery Service, Endpoint Discovery Service) pushed by Istiod.

Envoy handles: connection management, TLS termination and origination, HTTP/2 and gRPC, load balancing, retries, timeouts, circuit breaking, rate limiting, distributed tracing, and access logging — all without changes to application code.

### sidecar
The **sidecar** (`istio-proxy`) is an Envoy process injected as a second container into every application pod. It intercepts all inbound and outbound TCP traffic via `iptables` rules added by the `istio-init` init container (or via CNI plugin), making it transparent to the application.

The sidecar maintains two sets of listeners:
- **Inbound listeners** — one per declared service port, applying [PeerAuthentication](#peerauthentication), [RequestAuthentication](#requestauthentication), [AuthorizationPolicy](#authorizationpolicy), and [WasmPlugin](#wasmplugin) on arriving traffic.
- **Outbound listeners** — one per cluster in the mesh, applying [VirtualService](#virtualservice) routing rules, [DestinationRule](#destinationrule) connection policies, and [ServiceEntry](#serviceentry) external registrations on departing traffic.

Istiod pushes the full mesh config to every sidecar by default; a [Sidecar](#sidecar) resource scopes that down to reduce memory and propagation cost.

### ingressgateway
The **ingress gateway** is a standalone Envoy pod (not a sidecar) deployed at the mesh edge, typically exposed via a Kubernetes `LoadBalancer` service. It is the single entry point for external traffic into the mesh.

Unlike a sidecar it has no application container alongside it. Its listener configuration comes exclusively from [Gateway](#gateway) resources, and its routing rules come from [VirtualService](#virtualservice) resources that reference it in the `gateways` field. [PeerAuthentication](#peerauthentication), [RequestAuthentication](#requestauthentication), [AuthorizationPolicy](#authorizationpolicy), [DestinationRule](#destinationrule), [EnvoyFilter](#envoyfilter), [Telemetry](#telemetry), and [WasmPlugin](#wasmplugin) also apply here.

### egressgateway
The **egress gateway** is a standalone Envoy pod deployed at the mesh edge for controlling and observing traffic leaving the mesh toward external services. Traffic is directed to it by routing sidecars to send designated external traffic through the gateway pod rather than directly out of the cluster.

It enables centralised policy enforcement on outbound traffic: logging, mTLS origination toward external endpoints, and [AuthorizationPolicy](#authorizationpolicy) to restrict which workloads may reach which external destinations. [Gateway](#gateway), [VirtualService](#virtualservice), [DestinationRule](#destinationrule), [ServiceEntry](#serviceentry), [EnvoyFilter](#envoyfilter), [Telemetry](#telemetry), and [WasmPlugin](#wasmplugin) all apply here.
## Introduction to resource types

### Gateway
**Applies to:** istio-ingressgateway, istio-egressgateway — **server side**

A **Gateway** configures the listeners (ports, hostnames, and TLS settings) exposed by an ingress or egress gateway Envoy pod. It is pure configuration — it has no effect on application sidecar proxies. A `Gateway` on its own does not route traffic; it must be paired with a [VirtualService](#virtualservice) that references it in its `gateways` field.

**Key use cases:** expose HTTP/HTTPS services to external traffic; terminate or pass-through TLS at the mesh edge; control which hosts and ports the egress gateway forwards.

### VirtualService
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — **server side** (gateway-bound) and **client side** (mesh-bound)

A **VirtualService** defines routing rules for traffic addressed to a host. Where it takes effect depends entirely on the `gateways` field: set to `mesh` it controls outbound routing from sidecars (client side); set to a named gateway it controls how that gateway routes inbound traffic (server side). A single VirtualService can target both simultaneously.

**Key use cases:** header/URI/weight-based routing; canary and blue-green deployments; timeouts, retries, and fault injection; traffic mirroring; URI and header rewriting.

### PeerAuthentication
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — **server side**

A **PeerAuthentication** policy controls how a workload's Envoy proxy handles **mutual TLS (mTLS)** on its inbound connections. It can enforce strict mTLS, allow permissive mode (plaintext and mTLS side-by-side), or disable mTLS entirely for specific ports.

**Key use cases:** enforce mesh-wide or namespace-wide strict mTLS; run permissive mode during a migration from plaintext; exempt health-check ports from mTLS.

### RequestAuthentication
**Applies to:** istio-ingressgateway, istio-proxy — **server side**

A **RequestAuthentication** policy validates **JSON Web Tokens (JWT)** on inbound requests. It specifies the trusted issuers, the JWKS endpoint to fetch public keys, and where to look for the token (Authorization header, query parameter, or cookie). Extracted claims are forwarded as headers for downstream use. If no JWT is present the request is still admitted — use an [AuthorizationPolicy](#authorizationpolicy) to make a valid token mandatory.

**Key use cases:** validate tokens from Keycloak, Auth0, or Google at the ingress gateway or at individual services; support multiple issuers in the same policy; extract claims for fine-grained authorisation.

### AuthorizationPolicy
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — **server side**

An **AuthorizationPolicy** provides Layer 4–7 access control (RBAC) evaluated on inbound requests after [PeerAuthentication](#peerauthentication) and [RequestAuthentication](#requestauthentication) have run. Rules can match on mTLS principal, namespace, JWT claims, HTTP method, path, headers, and ports, and result in ALLOW, DENY, or AUDIT actions.

**Key use cases:** zero-trust service-to-service access; require a valid JWT with specific claims; default-deny with selective allow; block traffic from specific namespaces; restrict HTTP methods or paths.

### DestinationRule
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — **client side**

A **DestinationRule** is a **client-side** policy applied to the outbound clusters of the sending Envoy proxy — it configures *how* the proxy connects to a destination after [VirtualService](#virtualservice) routing has already selected it. It can define named subsets (used by VirtualService for traffic splitting), set connection pool limits, configure outlier detection, and control TLS origination toward the destination.

**Key use cases:** define version subsets for canary/blue-green; set load balancing algorithm; configure circuit breaker connection pool limits; eject unhealthy hosts via outlier detection; originate mTLS or TLS toward external services.

### ServiceEntry
**Applies to:** istio-egressgateway, istio-proxy — **client side**

A **ServiceEntry** registers an external host (outside the Kubernetes cluster) in Istio's internal service registry, making it a first-class destination that sidecars and the egress gateway can route to. Once registered, all standard Istio traffic policies — retries, timeouts, circuit breaking, mTLS — can be applied to that external service.

**Key use cases:** allow egress to external APIs (e.g. `api.stripe.com`); register VMs or legacy services as mesh endpoints; define services on non-standard ports or protocols; apply Istio policies to external endpoints.

### WorkloadEntry
**Applies to:** control plane only (not translated to Envoy xDS directly)

A **WorkloadEntry** represents a non-Kubernetes endpoint — a VM, bare-metal server, or any external process — that should participate in the mesh as a first-class workload. Istiod reads it and adds the described endpoint to the EDS for matching `ServiceEntry` hosts. It does not configure any Envoy proxy directly.

**Key use cases:** onboard legacy VMs into the mesh; register bare-metal databases or external processes as mesh endpoints; enable mTLS between pods and VMs.

### WorkloadGroup
**Applies to:** control plane only (not translated to Envoy xDS directly)

A **WorkloadGroup** is a template for a logical group of VM workloads sharing the same spec — service account, labels, ports, network, and locality. It is the VM equivalent of a Kubernetes `Deployment` and is used by `istioctl x workload entry configure` to bootstrap `istio-agent` on each VM, which then auto-creates a `WorkloadEntry` on registration.

**Key use cases:** template-based auto-registration of VM fleets; consistent labelling and service account across all VMs in a group; VM autoscaling — new VMs join and leave the mesh automatically.

### ProxyConfig
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — neither server nor client side (proxy process tuning)

A **ProxyConfig** resource tunes the `istio-proxy` process itself via a workload or namespace label selector. It exposes low-level settings not available through other Istio APIs: CPU concurrency, tracing provider and sampling, environment variables, startup hold time, and drain duration.

**Key use cases:** increase concurrency for high-throughput services; set per-workload tracing configuration; configure `holdApplicationUntilProxyStarts`; inject environment variables into the sidecar container.

### Sidecar
**Applies to:** istio-proxy — **server side** (inbound listeners) and **client side** (outbound listeners)

A **Sidecar** resource scopes the xDS configuration Istiod pushes to a workload's `istio-proxy`. By default every sidecar receives the full mesh config; a Sidecar resource restricts that to only the inbound ports and outbound hosts the workload actually needs. It does not apply to gateway pods.

**Key use cases:** reduce sidecar memory in large meshes (100+ services); speed up xDS propagation by shrinking blast radius; restrict inbound ports a sidecar listens on; define fine-grained egress listener rules.

### EnvoyFilter
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — **server side** (listeners) and **client side** (clusters)

An **EnvoyFilter** directly patches the Envoy xDS configuration generated by Istiod. It is the escape hatch for capabilities not covered by higher-level APIs, able to insert, modify, or remove any filter, cluster, listener, or route in the Envoy config.

**Key use cases:** add custom HTTP filters (Lua, ext_authz, custom headers); enable local rate limiting; patch cluster TLS settings for edge cases; add or customise access log formats globally.

### Telemetry
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — **server side** and **client side**

A **Telemetry** resource controls the observability behaviour of Envoy proxies — metrics emission, distributed trace generation and sampling, and access log formatting and destination. It applies to any proxy type and can be scoped mesh-wide, per-namespace, or per-workload.

**Key use cases:** enable/disable distributed tracing per workload; set trace sampling rate (e.g. 1% prod / 100% staging); switch tracing provider (Zipkin, Jaeger, OpenTelemetry); disable access logging or specific metrics per workload.

### WasmPlugin
**Applies to:** istio-ingressgateway, istio-egressgateway, istio-proxy — **server side** and **client side**

A **WasmPlugin** extends the Envoy proxy with custom logic compiled to **WebAssembly (Wasm)**. Plugins are inserted into the filter chain at a configurable phase (AUTHN, AUTHZ, or STATS) and can inspect, modify, or block requests and responses without modifying Istiod or rebuilding Envoy.

**Key use cases:** custom request/response header transformation; custom authentication or token validation; request logging to proprietary systems; injecting tracing headers for non-standard protocols.

## Where it is applied
Definitions:
- server side: it applies in a listening port of the service/gateway
- client side: it applies to a client connection establishment

| Resource                                                | istio-ingressgateway | istio-egressgateway | istio-proxy<br>(sidecar) | server side | client side | Control Plane resource |
| ------------------------------------------------------- | -------------------- | ------------------- | ------------------------ | ----------- | ----------- | ---------------------- |
| [Gateway](#gateway)                             | ✔️                   | ✔️                  | ❌                        | ✔️          | ❌           | ❌                      |
| [VirtualService](#virtualservice)               | ✔️                   | ✔️                  | ✔️                       | ✔️          | ✔️          | ❌                      |
| [PeerAuthentication](#peerauthentication)       | ✔️                   | ✔️                  | ✔️                       | ✔️          | ❌           | ❌                      |
| [RequestAuthentication](#requestauthentication) | ✔️                   | ❌                   | ✔️                       | ✔️          | ❌           | ❌                      |
| [AuthorizationPolicy](#authorizationpolicy)     | ✔️                   | ✔️                  | ✔️                       | ✔️          | ❌           | ❌                      |
| [DestinationRule](#destinationrule)             | ✔️                   | ✔️                  | ✔️                       | ❌           | ✔️          | ❌                      |
| [ServiceEntry](#serviceentry)                   | ❌                    | ✔️                  | ✔️                       | ❌           | ✔️          | ❌                      |
| [WorkloadEntry](#workloadentry)                 | ❌                    | ❌                   | ❌                        | ❌           | ❌           | ✔️                     |
| [WorkloadGroup](#workloadgroup)                 | ❌                    | ❌                   | ❌                        | ❌           | ❌           | ✔️                     |
| [ProxyConfig](#proxyconfig)                     | ✔️                   | ✔️                  | ✔️                       | ❌           | ❌           | ❌                      |
| [Sidecar](#sidecar)                             | ❌                    | ❌                   | ✔️                       | ✔️          | ✔️          | ❌                      |
| [EnvoyFilter](#envoyfilter)                     | ✔️                   | ✔️                  | ✔️                       | ✔️          | ✔️          | ❌                      |
| [Telemetry](#telemetry)                         | ✔️                   | ✔️                  | ✔️                       | ✔️          | ✔️          | ❌                      |
| [WasmPlugin](#wasmplugin)                       | ✔️                   | ✔️                  | ✔️                       | ✔️          | ✔️          | ❌                      |
## Key Use Cases

| Resource              | Key Use Cases                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Gateway](#gateway)               | - Expose HTTP/HTTPS services to external traffic<br>- Terminate TLS at the gateway (simple or mutual)<br>- Pass through TLS to the upstream service (SNI-based routing)<br>- Control egress traffic leaving the mesh                                                                                                                                                                                   |
| [VirtualService](#virtualservice)        | - Route traffic by HTTP headers, URI, method, or weight<br>- Canary releases (e.g., 90% v1 / 10% v2)<br>- Timeouts and retries<br>- Fault injection for resilience testing<br>- Traffic mirroring (shadow traffic)<br>- Rewriting URIs or headers before forwarding                                                                                                                                    |
| [PeerAuthentication](#peerauthentication)    | - Enforce strict mTLS across the entire mesh or a single namespace<br>- Allow permissive mode during a migration (accepts both plaintext and mTLS)<br>- Disable mTLS for a specific workload (e.g., a health-check endpoint)<br>- Override mesh-wide policy for specific ports                                                                                                                         |
| [RequestAuthentication](#requestauthentication) | - Validate JWTs issued by an identity provider (Keycloak, Auth0, Google, etc.)<br>- Extract JWT claims for use in authorization rules<br>- Support multiple issuers (e.g., internal service tokens + user tokens)<br>- Apply per-workload or per-namespace JWT validation                                                                                                                              |
| [AuthorizationPolicy](#authorizationpolicy)   | - Allow only specific services to call a workload (zero-trust service-to-service)<br>- Require a valid JWT and check specific claims (e.g., `role: admin`)<br>- Deny all traffic by default, then selectively allow<br>- Block traffic from specific namespaces or external sources<br>- Restrict HTTP methods or paths (e.g., only `GET /api/public`)                                                 |
| [DestinationRule](#destinationrule)       | - Define version subsets for canary/blue-green deployments<br>- Configure load balancing algorithm per service<br>- Set connection pool limits (circuit breaker)<br>- Configure outlier detection (eject unhealthy hosts)<br>- Set client-side TLS mode toward a destination                                                                                                                           |
| [ServiceEntry](#serviceentry)          | - Allow egress traffic to external APIs (e.g., `api.stripe.com`)<br>- Register services running outside the mesh (VMs, legacy systems)<br>- Define services on non-standard ports or protocols<br>- Apply mTLS, retries, or circuit breaking to external endpoints                                                                                                                                     |
| [WorkloadEntry](#workloadentry)         | - Onboard legacy VMs into the mesh without containerising them<br>- Register bare-metal databases or external processes as mesh endpoints<br>- Enable mTLS between Kubernetes pods and VMs<br>- Apply Istio traffic policies (retries, circuit breaking) to VM-backed services                                                                                                                         |
| [WorkloadGroup](#workloadgroup)         | - Template-based auto-registration of VM fleets<br>- Consistent labelling, service account, and network config across all VMs in a group<br>- Bootstrap config for `istio-agent` on VMs (via `istioctl x workload entry configure`)<br>- VM autoscaling — new VMs automatically join and leave the mesh<br>                                                                                            |
| [ProxyConfig](#proxyconfig)           | - Increase sidecar CPU concurrency for high-throughput services<br>- Set tracing configuration (sampling, provider) per workload<br>- Override the proxy image or startup arguments<br>- Set environment variables in the sidecar container<br>- Configure the hold-up time for application startup (holdApplicationUntilProxyStarts)<br>- Tune inter-proxy connection settings (e.g., drain duration) |
| [Sidecar](#sidecar)               | - Reduce sidecar memory usage and xDS config size in large meshes (100+ services)<br>- Speed up config propagation by reducing the blast radius of service changes<br>- Restrict which ports and protocols a sidecar listens on inbound<br>- Define egress listeners for traffic leaving the mesh via specific hosts                                                                                   |
| [EnvoyFilter](#envoyfilter)           | - Add a custom HTTP filter (e.g., Lua, ext_authz, custom header manipulation)<br>- Modify connection timeouts or buffer sizes not exposed by DestinationRule<br>- Enable Envoy's `local_rate_limit` filter<br>- Patch cluster TLS settings for edge cases<br>- Add or modify access log formats globally                                                                                               |
| [Telemetry](#telemetry)             | - Enable or disable distributed tracing per workload or namespace<br>- Set sampling rate for traces (e.g., 1% in production, 100% in staging)<br>- Configure which tracing provider to use (Zipkin, Jaeger, OpenTelemetry)<br>- Customise or disable access logging per workload<br>- Disable specific metrics to reduce cardinality<br>- Add custom metric tags from request headers or attributes    |
| [WasmPlugin](#wasmplugin)            | - Custom request/response transformation (add, remove, or rewrite headers)<br>- Custom authentication or token validation logic<br>- Request logging to proprietary systems<br>- Traffic shaping or shadow logging<br>- Injecting tracing headers for non-standard protocols                                                                                                                           |
