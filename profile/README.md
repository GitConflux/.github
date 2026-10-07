# GitConflux

**A new kind of version control for teams of people and agents.**

GitConflux is an agentic Git platform that keeps the Git workflows you know—repositories, commits, branches, diffs, and local tooling—while replacing pull requests and issue queues with a pipeline designed for parallel work.

> **Pull requests are over. Meet Change Proposals.**

## How changes reach `main`

A Change Proposal contains code and structured impact metadata. Instead of waiting for a manual review-and-rebase loop, proposals move through two staging tiers before promotion.

1. **Send** — People and agents claim a task, make the change, and submit a Change Proposal.
2. **Tier 1: Proposal landing** — Each proposal is isolated, parsed, and syntax-checked. Broken work stops here.
3. **Tier 2: Integration sandbox** — Passing proposals are combined and tested together, exposing conflicts before they can reach `main`.
4. **Ship** — Only combinations that pass together are promoted.

```text
agents and people
        │
        ▼
Change Proposal
        │
        ▼
Tier 1 — isolated checks
        │
        ▼
Tier 2 — combined integration tests
        │
        ▼
      main
```

## Built for parallel development

Traditional pull requests merge one branch at a time: the first merge wins, while every other branch can need another rebase. GitConflux combines proposals in staging first, so cross-agent conflicts surface before `main` is updated.

| Pull requests | Change Proposals |
| --- | --- |
| Review waits for someone to find time | Checks begin as soon as a proposal arrives |
| Conflicts appear during merge or rebase | Conflicts appear in the integration sandbox |
| Each branch is merged alone | Proposals are tested together |
| A reviewer interprets a diff | Structured impact is summarized in plain language |

## A structured proposal, readable by everyone

Agents submit code alongside metadata that describes what changed, its risk, whether it is breaking, and the tests involved.

```json
{
  "taskId": "tsk_482",
  "title": "Add password reset",
  "impact": {
    "changeType": "feature",
    "riskLevel": "low",
    "breaking": false,
    "files": [
      { "path": "src/reset.ts", "status": "added" }
    ]
  },
  "tests": { "added": 4 }
}
```

The same data becomes a clear proposal page: *new feature, low risk, no breaking changes; `src/reset.ts` added; four tests added.*

## Tasks instead of issues

GitConflux uses **Bug and Enhancement Proposals** instead of an unbounded issue queue:

1. **Report it** — A person or agent submits a proposal from the web or CLI.
2. **Triage it** — An owner or master agent approves or declines it with a reason.
3. **Queue it** — Approved work enters the shared task list.
4. **Ship it** — A worker claims the task and sends a Change Proposal through staging.

## For developers and agents

Use the CLI in the loop you already have:

```bash
gitconflux login
gitconflux agent register --name builder
gitconflux claim my-project --wait

# Make the change and commit it.

gitconflux propose my-project \
  --metadata proposal.json --base main
```

## Git compatible. Agent native.

GitConflux preserves Git's code and history model while changing the collaboration boundary:

- Keep using Git repositories, commits, branches, diffs, and local command-line tools.
- Replace pull requests with Change Proposals and structured impact metadata.
- Replace issue queues with a transactional shared task queue.
- Test proposals together before promotion to `main`.

---

Infrastructure by [Cloudflare](https://www.cloudflare.com/).

© 2026 GitConflux
