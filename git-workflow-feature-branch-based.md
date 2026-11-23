# Feature Branch Workflow

## TOC

- [introduction](#introduction)
- [same as branch-based](#same-as-branch-based)
- [differences](#differences)
- [what stays open](#what-stays-open)
- [when to use it](#when-to-use-it)
- [references](#references)

## Introduction

The feature branch workflow is the basic branching pattern: all work on a feature or fix happens in a dedicated branch instead of on `main`, and the branch is merged back when the work is finished, usually through a pull request.

It is **the same as the [branch-based workflow (GitHub Flow)](git-workflow-branch-based.md), with the differences listed below**. The two terms are often used as synonyms. This repository treats the feature branch workflow as the general pattern and GitHub Flow as the version of it with explicit deployment rules.

## Same as Branch-Based

Everything else is identical to [branch-based](git-workflow-branch-based.md); see that document for the diagrams, branch types, naming, commands and merge options:

- one permanent branch, `main`, and no `develop` or `release` branches
- one temporary branch per feature, fix or task, created from `main`
- merge through a pull request with peer review and CI
- delete the branch after merge
- development flow and feature developer workflow diagrams: [development flow](git-workflow-branch-based-development-flow.png), [feature developer workflow](git-workflow-branch-based-feature-developer-workflow.png)

## Differences

| | Feature branch | [Branch-based (GitHub Flow)](git-workflow-branch-based.md) |
|---|---|---|
| Scope | How changes are isolated and merged | A complete workflow, including deployment |
| `main` always deployable | not required | required |
| Deploy after merge | not defined; release when the team decides | yes, right away (or deploy from the PR branch, then merge) |
| Release step in the diagram | separate: tag `main`, deploy to test, then production | each merge is built, tested and deployed |
| Branch protection and CI | recommended | required |
| Branch lifetime | not constrained | days, not weeks |

In the development flow diagram, the only visible difference is the end of each cycle: in branch-based, every merge to `main` is followed by build, test and deploy; here, merges only trigger build and test, and a later, deliberate release (tag `main`, deploy to test, then production) ships a batch of merged features.

## What Stays Open

The pattern does not say:
- how often `main` is released
- whether branches are short-lived or long-lived (long-lived branches are its main weakness: conflicts pile up and integration is postponed; see [trunk-based](git-workflow-trunk-based.md))
- how fixes and hotfixes are handled (use a normal branch from `main`)
- how to support several released versions (see [branch-based with release branches](git-workflow-branch-with-branches-based.md))

Every other workflow in this repository uses feature branches: [trunk-based](git-workflow-trunk-based.md) (optional, hours to two days), [branch-based with release branches](git-workflow-branch-with-branches-based.md) and [GitFlow](git-workflow-gitflow.md) (from `develop`).

## When to Use It

**Use it when:**
- the team is small or new to pull requests
- releases are irregular and no deployment model has been chosen

**Consider another workflow when:**
- you deploy after every merge → [branch-based (GitHub Flow)](git-workflow-branch-based.md)
- you integrate several times a day with strong automated tests → [trunk-based](git-workflow-trunk-based.md)
- you support several released versions → [branch-based with release branches](git-workflow-branch-with-branches-based.md)
- you have scheduled, audited releases → [GitFlow](git-workflow-gitflow.md)

## References

- [Atlassian: Git feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
- [Atlassian: comparing Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Pro Git: Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows)
- [Pro Git: Distributed Workflows](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows)
- [Martin Fowler: Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)
