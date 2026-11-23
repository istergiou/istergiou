# GitFlow: Research

Research notes for [git-workflow-gitflow.md](git-workflow-gitflow.md). Researched 2026-11-20. Links marked ✔ were opened and the quoted claim checked; links marked ○ were seen only in search results.

## TOC

- [organisations and teams using it](#organisations-and-teams-using-it)
- [references in literature](#references-in-literature)
- [documentation and guides](#documentation-and-guides)
- [source quality notes](#source-quality-notes)

## Organisations and Teams Using It

I did not find large, named organisations that publicly document using GitFlow as designed. What exists is vendor documentation, plus a handful of small-team blog posts, several of them describing a *modified* GitFlow or a move away from it.

| Who | What is documented | Source |
|---|---|---|
| **Atlassian** (documents, does not claim to use it) | Describes GitFlow as the original model and now calls it a legacy workflow that "has fallen in popularity in favor of trunk-based workflows" | [Atlassian: Gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) ✔ |
| **AWS Prescriptive Guidance** (documents) | Describes GitFlow branches and positions it for versioned software with scheduled releases, GitHub Flow for continuously deployed web applications | [AWS: Gitflow branching strategy](https://docs.aws.amazon.com/prescriptive-guidance/latest/choosing-git-branch-approach/gitflow-branching-strategy.html) ✔ |
| **Small teams** (search excerpts only) | A team using a heavily modified git-flow with release branches cut from `develop` and deployed to staging then production; a team that moved to a simplified flow because git-flow was too heavy for several deploys a day; a team using `release/<number>` branches named after sprints | [Medium: Simplified Git Flow](https://medium.com/goodtogoat/simplified-git-flow-5dc37ba76ea8) ○; [One Blink: Our Git Branching Model](https://medium.com/one-blink-technology-group/our-git-branching-model-for-most-projects-3e3aca9ccdb9) ○ |

Organisations that *moved away* from or rejected GitFlow, which is evidence for when not to use it:
- **GitHub**: "At GitHub, we do not use git-flow" because it deploys all the time ([Chacon, 2011](https://scottchacon.com/2011/08/31/github-flow/) ✔).
- **CircleCI**: describes using one main branch with short-lived branches instead ([CircleCI blog](https://circleci.com/blog/you-are-what-you-git-how-your-vcs-branching-model-affects-your-delivery-cadence) ○).

## References in Literature

| Reference | Relevance |
|---|---|
| Driessen: [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) (2010-01-05) ✔ | The original article that defined the model |
| Driessen: [Note of reflection](https://nvie.com/posts/a-successful-git-branching-model/#a-note-of-reflection) (2020-03-05) ✔ | The author notes that the most popular type of software is shifting to web apps, which are continuously delivered, not rolled back, and need not support multiple versions in the wild; for those, a simpler workflow is better, while GitFlow still fits software with explicit versions |
| Atlassian: [Gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) ✔ | The most widely read tutorial; marks it as legacy |
| Chacon: [GitHub Flow](https://scottchacon.com/2011/08/31/github-flow/) ✔ | The best-known critique, arguing GitFlow is designed around "releases" |
| Forsgren, Humble, Kim: *Accelerate* (2018) ○ | Evidence favouring short-lived branches and trunk-based development over long-lived branches (see [git-workflow-trunk-based-research.md](git-workflow-trunk-based-research.md)) |

## Documentation and Guides

- [Vincent Driessen: A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) ✔
- [git-flow CLI tool (nvie/gitflow)](https://github.com/nvie/gitflow) ✔
- [Atlassian: Gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) ✔
- [AWS Prescriptive Guidance: Gitflow branching strategy](https://docs.aws.amazon.com/prescriptive-guidance/latest/choosing-git-branch-approach/gitflow-branching-strategy.html) ✔
- [Atlassian: comparing Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) ✔

## Source Quality Notes

- The "small teams" rows come from search excerpts that I did not open in full, so treat them as leads, not verified case studies.
- Absence of named large users in this research does not mean there are none. Many companies use GitFlow internally without publishing it, but I found no source to cite.
- The nvie.com post has had a 2020 reflection note added by the author; documents that quote only the 2010 text omit the author's own caveat.
