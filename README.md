# Review rounds

A Claude Code plugin that sweeps your copy, docs or UI text against your house rules and lets you review every proposed change in rounds.

1. **Rules.** Your rules live in your project, in `review-rules.md`. Start from a set that ships with the plugin, bring your own, or write them with Claude.
2. **Sweep.** Claude reads the pages or files you name and proposes a change wherever a rule is clearly broken. Each change says which rule it applies and why.
3. **Review.** The changes go on a private claude.ai page. For each one you approve it, ask for changes, or keep what's there, with a comment if you want.
4. **Rounds.** Claude applies what you approved and brings everything else back in the next round, with your comment beside it. Earlier rounds stay on the page, read only.
5. **Rules learn.** When a comment is a general preference ("we never use exclamation marks"), Claude proposes it as a new rule in the next round. Approve it and it's added to your rules file, and every later sweep checks for it.

## What's in it

```
.claude-plugin/plugin.json                  the plugin
.claude-plugin/marketplace.json             a one-plugin marketplace, for installing from this folder
skills/review-rounds/SKILL.md               the steps Claude follows
skills/review-rounds/rules/copy.md          starter rules for site and marketing copy
skills/review-rounds/rules/docs.md          starter rules for documentation
skills/review-rounds/rules/ui.md            starter rules for interface text
skills/review-rounds/reference/rules-format.md   how a rules file is written
skills/review-rounds/reference/schema.md    every collection and field the review page reads
skills/review-rounds/template/review.html   the review page
```

In your project the plugin keeps two files: `review-rules.md` (your rules, edit it by hand any time) and `.review-rounds.json` (the review page's link, which rule files to use, and where your material lives).

<!-- Screen recording of one round goes here: demo.mp4 or demo.gif, about 30 seconds. -->

## Install

```bash
claude plugin marketplace add kelvinman/review-rounds
```

```bash
claude plugin install review-rounds@kelvinman
```

Restart Claude Code. To try it without installing, copy `skills/review-rounds` into `~/.claude/skills/`.

## Using it

In your project, ask in your own words:

- "Set up review rounds for the site copy." Claude asks what's being reviewed, sets up your rules and creates the review page.
- "Sweep the home and pricing pages." Claude proposes changes and opens a round.
- "They're done, what did they decide?" Claude summarises the decisions, applies the approvals and opens the next round.
- "Add a rule: we say clients, not customers." Claude edits your rules file.

Share the page with your reviewer from its Share menu, or review it yourself. Claude never writes to the reviewer's decisions.

## Your own rules

Any Markdown file in the format in `reference/rules-format.md` works: a heading per rule, a line on what it means, and a before and after example. Point Claude at it during setup. The starter sets are deliberately general; the rules that make a sweep good are the ones your reviews add.

## Needs

- Claude Code with the claude.ai artifact tools (`Artifact` and `ArtifactData`), signed in to a claude.ai account that can publish artifacts with the `db` capability.
- Reviewers need a claude.ai account the page can be shared with.

## Limits

- **Who can open it.** Review pages are claude.ai artifacts. They start private and can be shared with people in the owner's organization, or with outside guests where the owner's plan allows it. Reviewers outside the organization may not be able to open the page, and a public link, where available, is read only.
- **One decision per change.** If two people review the same page, the last save wins. For a team review, agree who decides, or make one page per reviewer.
- **Text only.** Each change shows as a word diff of two pieces of text. Screenshots and layouts aren't supported.
- **A sweep is a judgment.** Claude can miss things or flag text that's fine. The review exists for that, and rules sharpen it over time.
- **Claude does the bookkeeping.** The page has no button to open a round or apply changes. Those happen when you ask Claude.
- **Up to 50 writes per batch.** Larger rounds are seeded in several batches, and rounds over 25 changes are tiring to review.

## Status

Version 0.2.0. Tested end to end twice on made-up material: a hand-written batch over two rounds, and a sweep of a sample page with the copy starter rules, where an approved comment became rule 11. Released under the MIT licence.
