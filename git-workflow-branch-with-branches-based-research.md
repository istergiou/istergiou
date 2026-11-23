# Branch-Based Workflow with Release Branches (GitLab Flow): Research

Research notes for [git-workflow-branch-with-branches-based.md](git-workflow-branch-with-branches-based.md). Researched 2026-11-20. Links marked ✔ were opened and the quoted claim checked; links marked ○ were seen only in search results.

## TOC

- [organisations and teams using it](#organisations-and-teams-using-it)
- [references in literature](#references-in-literature)
- [documentation and guides](#documentation-and-guides)
- [source quality notes](#source-quality-notes)

## Organisations and Teams Using It

Few organisations describe their process as "branch-based with release branches". The table lists organisations whose published process matches the pattern: development on `main`, release branches cut from it, and fixes landing on `main` first and then being cherry-picked to release branches ("upstream first").

| Organisation | What is documented | Source |
|---|---|---|
| **GitLab** | Defines GitLab Flow, "often used with release branches": teams that must maintain several versions (e.g. a public API) keep a `v1` and a `v2` branch that are maintained individually. Older GitLab docs (archived versions, search excerpts only) describe one branch per minor version such as `2-3-stable`, with fixes cherry-picked from `main` rather than committed to the stable branch | [GitLab Flow blog (2014)](https://about.gitlab.com/blog/2014/09/29/gitlab-flow/) ✔; [GitLab Docs: branching strategies](https://docs.gitlab.com/user/project/repository/branches/strategies/) ✔ (lists long-lived release branches as a strategy); [archived GitLab Flow docs](https://archives.docs.gitlab.com/16.0/ee/topics/gitlab_flow.html) ○ |
| **Microsoft** (Azure DevOps / VSTS team) | "Release Flow": trunk-based development on `master`, a release branch per sprint, hotfixes cherry-picked from `master` into the release branch | [Release Flow: How we do branching on the VSTS team (2018)](https://devblogs.microsoft.com/devops/release-flow-how-we-do-branching-on-the-vsts-team/) ✔ |
| **Kubernetes** | Release branches are maintained for the most recent minor releases; fixes are cherry-picked from `master`, with a cherry-pick process and deadlines before each patch release | [Kubernetes patch releases](https://kubernetes.io/releases/patch-releases/) ✔ (cherry-pick process); "three most recent minor releases" from search excerpts ○ |
| **Chromium** | Main-first: fixes land on `main`, then are merged (cherry-picked) to release branches through a merge request process with stricter criteria as the stable release date nears | [Chromium: Merge Request Process](https://chromium.googlesource.com/chromium/src.git/+/refs/heads/main/docs/process/merge_request.md) ✔ |
| **Linux kernel** (stable trees) | "Upstream first": a fix must already be in mainline before it is accepted into a stable tree, normally via a `Cc: stable` tag | [Linux kernel: stable kernel rules](https://docs.kernel.org/process/stable-kernel-rules.html) ✔ |
| **Meta (Facebook)**, until 2016 | `master` plus a weekly release branch with cherry-picks into daily pushes; later replaced by pushing from `master` | [Rapid release at massive scale](https://engineering.fb.com/2017/08/31/web/rapid-release-at-massive-scale/) ✔ |

These projects use the same fix-flow but differ in tooling and scale (Kubernetes, Chromium and the kernel have dedicated release teams), so they show that the pattern works, not that GitLab Flow was adopted by name.

## References in Literature

| Reference | Relevance |
|---|---|
| [GitLab Flow](https://about.gitlab.com/blog/2014/09/29/gitlab-flow/) ✔ | The origin of release branches (and environment branches) as an extension of GitHub Flow; the cherry-pick-from-`main` rule appears in older GitLab docs rather than in the current pages |
| Fowler: [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html) ✔ | Describes the Release Branch pattern and its relationship to Mainline Integration |
| [trunkbaseddevelopment.com: branch for release](https://trunkbaseddevelopment.com/branch-for-release/) ✔ | Describes release branches cut from trunk with fixes made on trunk first, the same fix-flow as this model |
| Driessen: [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) ✔ | The alternative model, with `develop` and back-merges, which this workflow avoids |

## Documentation and Guides

- [GitLab Docs: branching strategies](https://docs.gitlab.com/user/project/repository/branches/strategies/) ✔
- [GitLab: What is GitLab Flow?](https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/) ✔
- [Kubernetes: patch releases and cherry picks](https://kubernetes.io/releases/patch-releases/) ✔
- [Chromium: Merge Request Process](https://chromium.googlesource.com/chromium/src.git/+/refs/heads/main/docs/process/merge_request.md) ✔
- [Linux kernel: stable kernel rules](https://docs.kernel.org/process/stable-kernel-rules.html) ✔
- [Atlassian: comparing Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) ✔

## Source Quality Notes

- GitLab's own docs were reorganised; the older `docs.gitlab.com/ee/topics/gitlab_flow.html` URL now returns 404, so the branching-strategies page and the 2014 blog are cited instead.
- The mapping of Kubernetes, Chromium, the Linux kernel and Microsoft to this model is my interpretation of their published processes; none of them call it "GitLab Flow".
- GitLab Flow also has an *environment branches* variant (`staging`, `production`). It is not covered by [git-workflow-branch-with-branches-based.md](git-workflow-branch-with-branches-based.md), which only describes release branches.
