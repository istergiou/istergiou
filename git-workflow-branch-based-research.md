# Branch-Based Workflow (GitHub Flow): Research

Research notes for [git-workflow-branch-based.md](git-workflow-branch-based.md). Researched 2026-11-20. Links marked ✔ were opened and the quoted claim checked; links marked ○ were seen only in search results or are cited from general knowledge.

## TOC

- [organisations and teams using it](#organisations-and-teams-using-it)
- [references in literature](#references-in-literature)
- [documentation and guides](#documentation-and-guides)
- [source quality notes](#source-quality-notes)

## Organisations and Teams Using It

| Organisation | What is documented | Source |
|---|---|---|
| **GitHub** | Origin of the model. In 2011 Scott Chacon described GitHub's own process: anything in `master` is deployable, and work happens in descriptively named branches merged through pull requests, with deployment after review | [Scott Chacon: GitHub Flow (2011-08-31)](https://scottchacon.com/2011/08/31/github-flow/) ✔ |
| **GitHub** (engineering practice) | Uses a variant of the flow in which new code is deployed *from the pull request branch* and merged only after it is confirmed in production; tooling is chat-driven (Hubot) | [Deploying branches to GitHub.com (Aman Gupta, 2015-06-02)](https://github.blog/engineering/infrastructure/deploying-branches-to-github-com/) ✔ |

I could not find other named organisations that publicly document their workflow as "GitHub Flow". Many teams and open-source projects use pull-request-based development on a single `main`, but they rarely describe it by that name, so I have not listed them.

Vendors that recommend or document the model (not the same as using it):
- [GitHub Docs: GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow) ✔ — "lightweight, branch-based workflow"
- [AWS Prescriptive Guidance: GitHub Flow branching strategy](https://docs.aws.amazon.com/prescriptive-guidance/latest/choosing-git-branch-approach/git-hub-flow-branching-strategy.html) ✔

## References in Literature

| Reference | Relevance |
|---|---|
| Chacon: [GitHub Flow](https://scottchacon.com/2011/08/31/github-flow/) ✔ | The original description of the model and its rules |
| Chacon, Straub: *Pro Git*, [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) ✔ and [Distributed Workflows](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows) ✔ | Topic (feature) branches and pull-request-based collaboration in the standard Git book |
| Fowler: [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html) ✔ | Places feature branching and mainline integration among the patterns, with the trade-offs of branch lifetime |
| Atlassian: [Git feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) ✔ | Tutorial for the feature-branch-plus-pull-request model |

## Documentation and Guides

- [GitHub Docs: GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow) ✔
- [Microsoft Learn: Git branching guidance (Azure DevOps)](https://learn.microsoft.com/en-us/azure/devops/repos/git/git-branching-guidance) ✔
- [AWS Prescriptive Guidance: choosing a Git branch approach](https://docs.aws.amazon.com/prescriptive-guidance/latest/choosing-git-branch-approach/git-hub-flow-branching-strategy.html) ✔
- [Atlassian: comparing Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) ✔

## Source Quality Notes

- The strongest evidence is from GitHub itself, a single organisation with continuous deployment and a very strong deployment toolchain; the evidence says little about teams without that.
- Chacon's 2011 post is an opinion piece. It is the origin of the name but not an evaluation of the model.
- "GitHub Flow", "feature branch workflow" and "pull request workflow" are used loosely and overlap; the boundaries drawn in [git-workflow-branch-based.md](git-workflow-branch-based.md) are this repository's own.
