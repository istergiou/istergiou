# Forking Workflow: Research

Research notes for [git-workflow-forking.md](git-workflow-forking.md). Researched 2026-11-23. Links marked ✔ were opened and the quoted claim checked; links marked ○ were seen only in search results or are cited from general knowledge.

## TOC

- [organisations and teams using it](#organisations-and-teams-using-it)
- [references in literature](#references-in-literature)
- [documentation and guides](#documentation-and-guides)
- [source quality notes](#source-quality-notes)

## Organisations and Teams Using It

The forking workflow is the default contribution model of open source projects hosted on GitHub and GitLab. The projects below document it in their own contributor guides.

| Organisation / project | What is documented | Source |
|---|---|---|
| **Kubernetes** | Contributors fork `kubernetes/kubernetes` ("Fork in the cloud"), clone the fork, add `upstream` as a remote with the push URL disabled (`no_push`), create a working branch, keep it in sync with `upstream`, push to the fork and open a pull request | [Kubernetes: GitHub workflow](https://www.kubernetes.dev/docs/guide/github-workflow/) ✔ |
| **Rust** | The compiler contributor guide assumes you have forked `rust-lang/rust` and cloned your fork, which is then `origin` | [rustc-dev-guide: Using Git](https://rustc-dev-guide.rust-lang.org/git.html) ✔ |
| **Django** | Contributors fork Django's GitHub repository, clone the fork and add `https://github.com/django/django.git` as the `upstream` remote | [Django: Working with Git and GitHub](https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/working-with-git/) ✔ |
| **Homebrew** | Contributors set up a fork of Homebrew's Git repository on GitHub, create a branch and open a pull request | [Homebrew: How to open a pull request](https://docs.brew.sh/How-To-Open-a-Homebrew-Pull-Request) ✔ |
| **GitLab** (as a product and as a project) | Documents forks: without write access, fork the project, change it in your fork and submit a merge request to the upstream project; with write access, use branches instead of a fork | [GitLab Docs: Forks](https://docs.gitlab.com/user/project/repository/forking_workflow/) ✔ |
| **GitHub** (as a platform) | Defines a fork as a repository that starts as a copy of an *upstream* repository and stays connected to it, with its own branches, members, issues and pull requests | [GitHub Docs: About forks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks) ✔ |

**Counter-example: the Linux kernel.** It is a very large open source project, but it does not use forks and pull requests as its contribution path. The kernel's patch submission guide says patches should be submitted by e-mail inline, and recommends `git send-email` ([Linux kernel: Submitting patches](https://docs.kernel.org/process/submitting-patches.html) ✔). So "open source" does not always mean "forking workflow"; the equivalent there is the mailing-list patch workflow, which has the same property (contributors have no write access) with a different mechanism.

The table lists projects whose contributor guides describe the workflow; it does not say anything about how many contributors use it or how it performs.

## References in Literature

| Reference | Relevance |
|---|---|
| [Atlassian: Forking workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow) ✔ | Defines the workflow: each developer has a server-side repository; "most often seen in public open source projects"; only the maintainer can push to the official repository; "typically follows a branching model based on the Gitflow Workflow" |
| Chacon, Straub: *Pro Git*, [Distributed Workflows](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows) ✔ | Describes the integration-manager workflow: each developer has write access to their own public repository and read access to everyone else's, with a canonical repository that represents the official project; this is the model forking implements |
| Chacon, Straub: *Pro Git*, [Contributing to a Project (GitHub)](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project) ✔ | Step-by-step fork and pull request flow: "if you want to contribute to an existing project to which you don't have push access, you can fork the project" |
| Fowler: [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html) ✔ | Discusses feature branching and integration patterns on which the forking workflow is layered (cited from the other research files; it does not cover forking in detail) |

## Documentation and Guides

- [Atlassian: Forking workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow) ✔
- [Atlassian: comparing Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) ✔
- [GitHub Docs: About forks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks) ✔
- [GitHub Docs: Syncing a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) ✔ (web UI *Sync fork* and `gh repo sync`)
- [GitHub Docs: Contributing to a project](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project) ○ (page opened, content not checked)
- [GitLab Docs: Forks](https://docs.gitlab.com/user/project/repository/forking_workflow/) ✔
- [Kubernetes: GitHub workflow](https://www.kubernetes.dev/docs/guide/github-workflow/) ✔

## Source Quality Notes

- All the organisation sources are contributor guides, so they show what each project asks contributors to do, not how many do it or how well it works.
- I did not find an independent study of the forking workflow comparable to the DORA material for trunk-based development, so there is no evidence here about its effect on delivery performance.
- The forking workflow is an access-control and repository layout choice, not a branching model. Sources use "forking workflow" for the repository layout and "feature branch workflow" for what happens inside the fork, so the combination in [git-workflow-forking.md](git-workflow-forking.md) is this repository's own framing, supported by Atlassian's and GitLab's text but not stated as such by them.
- The claim that forking is rare inside companies is my own observation and has no source here; GitLab's guidance (use branches if you have write access) is the closest supporting text.
- Naming differs between hosts: GitHub says *pull request*, GitLab says *merge request*, and Git itself calls the relation between a fork and its source `upstream` only by convention.
- Kubernetes' guide shows `master` in places and mentions the rename to `main`; the commands in the workflow document use `main`.
