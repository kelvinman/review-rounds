# Review store schema

Every collection is flat: `collection/doc`. The page subscribes to all five and redraws when any row changes. Fields not listed here are ignored, so you can add your own (for example `"source": "app/page.tsx:134"`) for later reference.

## review

One document, `meta`. Optional.

| Field | Type | Meaning |
|---|---|---|
| `title` | string | Name of the review, shown at the top of the sidebar. |
| `labels.current` | string | Label over the left side. Default `Current`. |
| `labels.rewrite` | string | Label over the right side. Default `Rewrite`. |

## rounds

One document per round, id `"1"`, `"2"` and so on.

| Field | Type | Meaning |
|---|---|---|
| `n` | number | The round number. Required. |
| `title` | string | Optional label in the progress bar instead of "Round n". |
| `openedAt` | string | Date the round opened. For your records. |

The highest round number is the active round. Earlier rounds are read only.

## items

One document per proposed change.

| Field | Type | Meaning |
|---|---|---|
| `round` | number | Which round it belongs to. Required. |
| `order` | number | Sort order within the round. Items without one sort by id. |
| `group` | string | Top level in the list, such as a site, an app or a document. |
| `subgroup` | string | Second level, such as a page or a screen. Optional. |
| `title` | string | Short name of the change, shown in the list and as the heading. |
| `location` | string | Where it is, such as a section name. Becomes the link text when `link` is set. |
| `link` | string | `http` or `https` URL that shows it in place. Anything else is dropped. |
| `why` | string | Why the change is proposed, addressed to the reviewer. |
| `current` | string | What is there now, exactly. Empty means new content. Newlines are kept. |
| `rewrite` | string | The proposed replacement, exactly. Empty means remove. |
| `rules` | string[] | Ids of `rules` documents this change applies. |
| `question` | string | A fact you need from the reviewer. Shown above the comment box. |
| `note` | string | Any other context, shown under the diff. |
| `source` | string | Where the text lives, such as `app/page.tsx:42`. Not shown; used when applying. |
| `kind` | string | `rule` for a proposed new or changed rule. Not shown; used when applying. |
| `follows` | string | Id of the item in an earlier round that this one continues. |
| `thread` | string | Optional explicit thread key. Normally derived from `follows`. |

## rules

The house rules the changes cite. Optional; the sidebar hides the section when there are none.

| Field | Type | Meaning |
|---|---|---|
| `label` | string | Short tag shown on items, such as `01`. Defaults to the id. |
| `text` | string | The rule, shown in the sidebar and on hover. |
| `order` | number | Sort order. |

## decisions

Written by the reviewer's page only. Id is the item's id. Never write here.

| Field | Type | Meaning |
|---|---|---|
| `status` | string | `approve`, `reject` (request changes), `keep` (keep current), or empty for undecided. |
| `comment` | string | The reviewer's comment or answer. |
| `round` | number | The item's round, so you can query one round. |
| `at` | string | ISO time of the last save. |

## Access rules

Declared at publish:

```json
{"db": {"rules": [
  {"path": "", "read": "view", "write": "admin"},
  {"path": "decisions", "read": "view", "write": "interact"}
]}}
```

The owner and editors write everything. Anyone with use access writes `decisions`. View-only people can read but not decide.
