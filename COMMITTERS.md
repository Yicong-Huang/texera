# Texera Committers and PPMC Members

## Contents

- [Project Roles](#project-roles)
- [Becoming a Collaborator](#becoming-a-collaborator)
- [Becoming a Committer](#becoming-a-committer)
- [Committer Responsibilities](#committer-responsibilities)
- [New Committer Onboarding](#new-committer-onboarding)
- [PPMC Members](#ppmc-members)

This draft describes how the Texera community thinks about project roles and responsibilities. It is intended to complement [CONTRIBUTING.md](CONTRIBUTING.md), not replace it. Texera welcomes contributions of all kinds, including code, documentation, bug reports, reviews, testing, design discussion, and user support.

Texera is an Apache incubating project. Formal committer and PPMC decisions follow Apache Software Foundation and Apache Incubator rules; this document captures Texera-specific expectations and practical guidance.

Project discussions and votes happen on the [dev@texera.apache.org](mailto:dev@texera.apache.org) mailing list ([archives](https://mail-archives.apache.org/mod_mbox/texera-dev/)). Development work happens in the [apache/texera](https://github.com/apache/texera) repository; see [CONTRIBUTING.md](CONTRIBUTING.md) for the regular PR workflow. Community questions and proposals may also use [GitHub Discussions](https://github.com/apache/texera/discussions).

## Project Roles

Texera uses Apache project roles to recognize sustained contribution and make it easier for people to help the project:

| Role | Meaning | Permissions | How to Join |
| --- | --- | --- | --- |
| Contributor | Contributes to the project. | Public GitHub participation. | Start contributing; no formal process. |
| Collaborator | Helps triage issues and PRs. | GitHub Triage role; no write access. | Dev vote; added through `github.collaborators`.[^collaborator] |
| Committer | Reviews, merges, and stewards work. | Repository write access; code-change votes. | PPMC vote for sustained contributions. |
| PPMC Member | Participates in project governance. | Release, committer, PPMC, and governance votes. | PPMC vote for sustained stewardship. |

[^collaborator]: ASF Infra documents this as the GitHub [Triage role](https://infra.apache.org/github-roles.html#triage), configured through [`github.collaborators`](https://github.com/apache/infrastructure-asfyaml#assigning-the-github-triage-role-to-external-collaborators); each repository is limited to 10 active collaborators unless VP Infra grants an exception.

[^becoming-committer]: See ASF Community Development's [Becoming a committer](https://community.apache.org/contributors/becomingacommitter.html) guide and ASF's [Get Involved](https://apache.org/foundation/getinvolved.html#become-a-committer) page.

## Becoming a Collaborator

Texera does not currently have any collaborators; contributors interested in helping with triage are welcome to volunteer on the dev mailing list. Good candidates regularly triage issues, review PRs, identify duplicates, ask for missing details, and route work to the right contributors.

A collaborator is nominated after sustained triage or review help, approved by dev vote, and added through `github.collaborators`.

## Becoming a Committer

Start by following [CONTRIBUTING.md](CONTRIBUTING.md) and participating publicly in issues, pull requests, discussions, and the dev mailing list. There is no fixed checklist that automatically makes someone a committer; the PPMC looks for sustained, visible contributions that help Texera and its community over time.[^becoming-committer]

Strong candidates usually show several of the following:

| Area | Examples |
| --- | --- |
| Code contributions | High-quality PRs, clear commit messages, tests, careful handling of compatibility and migration concerns. |
| Reviews | Timely, constructive reviews that help contributors improve their work and keep PRs moving. |
| Issue triage | Reproducing bugs, narrowing root causes, labeling issues, identifying duplicates, and helping define scope. |
| Documentation | Improving user guides, developer guides, operator docs, release notes, examples, and diagrams. |
| Community support | Answering questions on GitHub issues, pull requests, mailing lists, chat channels, or community meetings. |
| Release support | Testing release candidates, reporting results, and helping resolve release blockers. |
| Project stewardship | Improving tooling, CI, dependency maintenance, security posture, or long-term technical direction. |

The PPMC values both code and non-code work. A contributor does not need to touch every subsystem, but should demonstrate good judgment, reliability, and enough context to act in the project's interest.

## Committer Responsibilities

Committers are more than people who can merge pull requests. Their main responsibility is to help Texera remain a healthy, welcoming, and sustainable Apache project.

Texera committers are expected to:

- Review pull requests in a timely and constructive way.
- Help reduce stale PRs by reviewing, requesting changes, closing superseded work, or helping contributors finish promising changes.
- Answer contributor and user questions when they have relevant context.
- Take ownership of important bugs, regressions, and project maintenance tasks, especially when no other contributor is available.
- Keep CI, tests, formatting, dependency updates, and release preparation in good shape.
- Improve project processes and tooling when repeated friction appears.
- Model respectful discussion, technical clarity, and consensus-oriented decision making.
- Watch for security, licensing, privacy, and compatibility concerns and escalate them through the appropriate Apache channels.
- Encourage new contributors by explaining project conventions and leaving actionable review feedback.

Committers should merge changes only when the code, tests, documentation, and review discussion support doing so. When a change is outside their area of confidence, they should seek another reviewer rather than merging alone.

## New Committer Onboarding

After a new committer is elected and accepts the role, they should complete the ASF and GitHub setup needed to contribute directly:

1. Confirm that their Individual Contributor License Agreement is on file.
2. Create or confirm their Apache account.
3. Link their GitHub account through Apache GitBox.
4. Accept the invitation to the Apache GitHub organization.
5. Confirm access to the Texera repository and any relevant GitHub teams.
6. Subscribe to the project development mailing list.
7. Ask another committer or PPMC member for help with merge, release, and CI conventions before using new permissions.

New committers should start by merging low-risk, well-reviewed changes and asking for a second opinion whenever project policy, releases, security, or large architectural changes are involved.

## PPMC Members

PPMC members have additional project governance responsibilities during incubation. They help guide Texera toward Apache graduation by making sure the project follows ASF policies and develops an open, sustainable community.

PPMC members are expected to:

- Vote on releases, new committers, and new PPMC members.
- Participate in governance discussions on the project mailing lists.
- Help mentors and the Incubator PMC evaluate project health.
- Support release managers and verify that releases follow Apache policy.
- Protect the project's neutrality, openness, and community-first decision making.
- Mentor committers and contributors who are growing into larger project roles.

Only current PPMC members vote on adding new committers or PPMC members, following the Apache Incubator process.
