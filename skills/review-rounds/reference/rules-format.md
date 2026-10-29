# Rules file format

A rule set is one Markdown file. It lives in the user's project, so it travels with the work and can be edited by hand. The default path is `review-rules.md` at the project root. A project can hold more than one, for example `review-rules-docs.md`, and name them in `.review-rounds.json`.

## Shape

```markdown
---
name: Plain copy
kind: copy
---

## 01 Lead with what the reader gets
Open with the outcome or the answer. Background and how it works come after.
- Before: Founded in 2014, our team of experts has developed a platform that helps you plan.
- After: Plan a month of meals in ten minutes.

## 02 One idea per sentence
...
```

- Frontmatter: `name` (shown to people) and `kind` (`copy`, `docs`, `ui` or anything the user likes).
- Each rule is a `##` heading: a two-digit number, then the rule as a short instruction in sentence case.
- Under it, one to three lines saying what the rule means and where it stops applying.
- Optional `- Before:` and `- After:` lines with one example. Examples teach the sweep more than the description does, so keep at least one per rule.
- Optional `- Source:` line saying where the rule came from, for example `Added from review, round 2, 28 Oct 2026: "we say clients, not customers"`.

Numbers are the rule ids. They never get reused or renumbered, because items in old rounds cite them. A retired rule stays in the file with `(retired)` at the end of its heading, and the sweep skips it.

## In the review page

When you seed a round, copy the rules into the page's `rules` collection: doc id `r<number>` (for example `r01`), `label` the number, `text` the heading text, `order` the number. Items cite rules by those doc ids. If a project uses two rule files, prefix the doc ids so they don't clash (`copy-r01`, `docs-r01`) and use the prefix in `label` too.

## Project config

`.review-rounds.json` at the project root remembers the review between sessions:

```json
{
  "review": "https://claude.ai/artifact/...",
  "rules": ["review-rules.md"],
  "sources": ["app/**/page.tsx", "content/**/*.mdx"]
}
```

- `review`: the review page's artifact URL. One project, one review page, many rounds.
- `rules`: the rule files to sweep against, in order.
- `sources`: where the material lives, as globs or URLs. Optional; the user can name a scope each time.

Create the file at setup. Ask before committing it; it holds no secrets, but the artifact URL is private to the owner anyway.
