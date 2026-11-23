# Trunk-Based Development: Research

Research notes for [git-workflow-trunk-based.md](git-workflow-trunk-based.md). Researched 2026-11-20. Links marked ✔ were opened and the quoted claim checked; links marked ○ were seen only in search results or are cited from general knowledge.

## TOC

- [organisations and teams using it](#organisations-and-teams-using-it)
- [references in literature](#references-in-literature)
- [documentation and guides](#documentation-and-guides)
- [source quality notes](#source-quality-notes)

## Organisations and Teams Using It

| Organisation | What is documented | Source |
|---|---|---|
| **Google** | Single monorepo, trunk-based; virtually no branches apart from a few release branches; all new code goes to the trunk | [Potvin & Levenberg, "Why Google Stores Billions of Lines of Code in a Single Repository", CACM 59(7), 2016](https://dl.acm.org/doi/10.1145/2854146) ○ (link blocks automated checks); [Software Engineering at Google, ch. 16 "Version Control and Branch Management"](https://abseil.io/resources/swe-book/html/ch16) ✔ |
| **Meta (Facebook)** | For years: `master` plus a weekly release branch, with 500–700 cherry-picks per day into three daily pushes. By 2016 this reached its limit (>1,000 diffs/day), so the web site moved to "push from master" in April 2016; 100% of production web servers ran code deployed directly from `master` by April 2017 | [Facebook Engineering: "Rapid release at massive scale" (2017-08-31)](https://engineering.fb.com/2017/08/31/web/rapid-release-at-massive-scale/) ✔; [Paul Hammant on Facebook TBD (2013)](https://paulhammant.com/2013/03/04/facebook-tbd/) ✔ |
| **Microsoft** | Uses a trunk-based branching strategy across products. The Azure DevOps (VSTS) team calls its variant **Release Flow**: work on `master`, but master is not continuously deployed; a release branch per sprint, hotfixes cherry-picked from `master` | [How Microsoft develops with DevOps](https://learn.microsoft.com/en-us/devops/develop/how-microsoft-develops-devops) ✔; [Release Flow: How we do branching on the VSTS team (2018)](https://devblogs.microsoft.com/devops/release-flow-how-we-do-branching-on-the-vsts-team/) ✔ |
| **DORA research population** | Trunk-based development is one of the measured technical capabilities that predict software delivery performance, across thousands of surveyed teams (not named organisations) | [DORA: trunk-based development capability](https://dora.dev/capabilities/trunk-based-development/) ✔ |

Release Flow and Meta's pre-2016 model are trunk-based with release branches, the variant described in [git-workflow-branch-with-branches-based-research.md](git-workflow-branch-with-branches-based-research.md).

## References in Literature

| Reference | Relevance |
|---|---|
| Forsgren, Humble, Kim: *Accelerate: The Science of Lean Software and DevOps* (IT Revolution, 2018) ○ | Presents trunk-based development as one of the continuous delivery capabilities correlated with high delivery performance (few active branches, short-lived branches, rare code freezes) |
| Humble, Farley: *Continuous Delivery* (Addison-Wesley, 2010) ○ | Foundational book for continuous integration to a single mainline and the deployment pipeline (cited from general knowledge, not fetched) |
| Winters, Manshreck, Wright: *Software Engineering at Google* (O'Reilly, 2020), [ch. 16](https://abseil.io/resources/swe-book/html/ch16) ✔ | Google's argument for one-version, trunk-based development at scale |
| Fowler: [Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html) ✔ | Integrating into mainline at least daily; the reasoning behind short-lived branches |
| Fowler: [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html) ✔ | Catalogue of branching patterns; includes Mainline Integration, Trunk-Based and Release Branch |
| DORA: [Trunk-based development](https://dora.dev/capabilities/trunk-based-development/) ✔ | States trunk-based development is a required practice for continuous integration, and stresses small batches and synchronous code review |

## Documentation and Guides

- [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/) ✔ — reference site by Paul Hammant; includes [branch for release](https://trunkbaseddevelopment.com/branch-for-release/) ✔
- [Atlassian: trunk-based development](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development) ✔
- [Martin Fowler: feature flags](https://martinfowler.com/articles/feature-toggles.html) ✔
- [Atlassian: comparing Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) ✔

## Source Quality Notes

- trunkbaseddevelopment.com is advocacy material. Its case studies (including the claimed number of Google developers on the trunk) were not independently verified here.
- The Google CACM article is a vendor's own account. Google's trunk-based model relies on its monorepo, its tooling (e.g. cloud workspaces, large-scale testing) and automated large-scale changes, which most teams do not have.
- Meta's current setup (continuous push from `master`) is documented only up to the 2017 post and later conference talks; details may have changed.
