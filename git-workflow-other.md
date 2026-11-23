# Other Git Workflows and Practices

## TOC

- [introduction](#introduction)
- [environment branches](#environment-branches)
- [stacked changes](#stacked-changes)
- [centralized workflow](#centralized-workflow)
- [mailing-list patch workflow](#mailing-list-patch-workflow)
- [merge queues and merge trains](#merge-queues-and-merge-trains)
- [release trains](#release-trains)
- [support branches](#support-branches)
- [references](#references)

## Introduction

Short notes on workflows and practices that are not documented on their own in this repository. Each entry says what it is, how it relates to the main workflows, and where to read more. They fall into three groups:

- **Alternatives to a main workflow**: [environment branches](#environment-branches), [stacked changes](#stacked-changes), [centralized workflow](#centralized-workflow), [mailing-list patches](#mailing-list-patch-workflow)
- **Tooling added to a main workflow**: [merge queues and merge trains](#merge-queues-and-merge-trains)
- **Release practices added to a main workflow**: [release trains](#release-trains), [support branches](#support-branches)

The main workflows are [feature branch](git-workflow-feature-branch-based.md), [branch-based (GitHub Flow)](git-workflow-branch-based.md), [branch-based with release branches](git-workflow-branch-with-branches-based.md), [trunk-based](git-workflow-trunk-based.md), [GitFlow](git-workflow-gitflow.md) and [forking](git-workflow-forking.md).

## Environment Branches

One long-lived branch per environment, for example `main` → `staging` → `production`. A change is promoted by merging it forward from one branch to the next, so each environment's branch shows what is deployed there.

- **Origin**: the other variant of GitLab Flow, next to release branches. GitLab's description: pre-production branches can be added as needed, for example from `main` to `test`, from `test` to `acceptance`, and from `acceptance` to `production`.
- **Fix flow**: fixes still land on `main` first and are then merged forward.
- **Compared with release branches**: environment branches model *where* a version is deployed, release branches model *which version* is maintained. Use release branches for versioned software and environment branches for software deployed to a chain of environments.
- **Cost**: promotion is a merge, and long-lived branches drift. Many teams replace them with one `main` and per-environment configuration or deployment pipelines.
- Fowler lists it as the *Environment Branch* pattern.

## Stacked Changes

A large change is split into a chain of small, dependent changes, each a branch or commit that is reviewed on its own. Review of the first change can finish while the author already works on the next, which avoids both one huge pull request and waiting for a merge before continuing.

- **Gerrit** is built around this: each commit is a change, and its documentation includes a section on developing multiple features in parallel.
- On GitHub and GitLab it is done with chains of branches, each pull request targeting the previous branch, usually with extra tooling to keep the chain rebased.
- **Relation**: it addresses the same problem as [trunk-based](git-workflow-trunk-based.md) (long-lived, large branches) without requiring feature flags. It sits on top of the feature branch or branch-based workflow.
- **Cost**: when a change early in the chain is modified, every later change must be rebased.

## Centralized Workflow

A single `main` branch to which everyone commits directly: no feature branches and no pull requests. Atlassian describes it as a good fit for teams moving from Subversion, with `main` taking the place of `trunk`.

- **Relation**: the baseline all other workflows add structure to. Without branch protection it can be called [trunk-based](git-workflow-trunk-based.md) at its smallest, but trunk-based development as defined here adds CI, small frequent commits and often review.
- **Cost**: no isolation and no review gate. It works for very small teams or personal projects.

## Mailing-List Patch Workflow

Contributors send patches by e-mail, and maintainers apply them to their own trees. The Linux kernel documents this (patches submitted inline with `git send-email`).

- **Relation**: it has the same property as the [forking workflow](git-workflow-forking.md), contributors have no write access to the official repository, with a different mechanism. Maintainers form a hierarchy and trees are merged upward; the kernel's stable trees are an example of [release branches](git-workflow-branch-with-branches-based.md) with upstream-first fixes.

## Merge Queues and Merge Trains

Tooling, not a workflow. Pull requests are queued; each is tested against the latest `main` plus the changes ahead of it, and only merged if that passes. This keeps `main` green when many pull requests are open at once.

- GitHub calls it a *merge queue*, GitLab calls it *merge trains*.
- Useful with [branch-based](git-workflow-branch-based.md) and [trunk-based](git-workflow-trunk-based.md) workflows with many contributors or slow CI.
- **Cost**: longer waits per change and more CI capacity needed.

## Release Trains

A release practice: releases leave on a fixed schedule, and a change that is ready by departure ships, otherwise it waits for the next train. It can sit on top of [trunk-based](git-workflow-trunk-based.md) or [release branches](git-workflow-branch-with-branches-based.md); Microsoft's Release Flow with a release branch per sprint is close to it. Fowler lists it as the *Release Train* pattern.

## Support Branches

A branch that keeps an old released version alive for fixes. GitFlow's `support/*` branches serve this purpose, and in [branch-based with release branches](git-workflow-branch-with-branches-based.md) it is the normal `release/x.y` branch that stays open after release. They are mentioned in [GitFlow](git-workflow-gitflow.md#when-to-use-gitflow).

## References

- [Atlassian: comparing Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) (centralized workflow)
- [GitLab Flow (2014)](https://about.gitlab.com/blog/2014/09/29/gitlab-flow/) (pre-production and production branches)
- [Martin Fowler: Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html) (Environment Branch, Release Train, Maturity Branch, Hotfix Branch)
- [Gerrit: user introduction](https://gerrit-review.googlesource.com/Documentation/intro-user.html) (change-based review, multiple features in parallel)
- [Linux kernel: Submitting patches](https://docs.kernel.org/process/submitting-patches.html)
- [GitHub Docs: Managing a merge queue](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-a-merge-queue)
- [GitLab Docs: Merge trains](https://docs.gitlab.com/ci/pipelines/merge_trains/)
