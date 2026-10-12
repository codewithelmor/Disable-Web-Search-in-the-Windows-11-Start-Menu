# Prompt Template: Update `Favorite-Chrome-Extensions.md`

Use this template whenever you want to add, refresh, edit, or remove entries in `Favorite-Chrome-Extensions.md` while keeping the format identical every time.

## How to use

1. Start a chat with Claude and **attach the current `Favorite-Chrome-Extensions.md`** (or paste its contents).
2. Copy the prompt from [The Prompt](#the-prompt), delete the actions you don't need, and fill in each `{{placeholder}}`.
3. Send it. Claude returns the full updated file.
4. Review the changes, then commit the file to your repo.

---

## The Prompt

```text
You are updating my markdown file "Favorite-Chrome-Extensions.md". I have attached the
current version. Apply the actions below and return the COMPLETE updated file as a
downloadable .md file, keeping the existing structure and formatting exactly.

TODAY'S DATE: {{YYYY-MM-DD}}

ACTIONS (delete any that don't apply):

1. ADD these extensions (one Chrome Web Store URL per line):
   - {{https://chromewebstore.google.com/detail/...}}
   - {{https://chromewebstore.google.com/detail/...}}
   Optional note about why it's a favorite: {{my own words, or leave blank}}

2. REFRESH these extensions (re-check the store page and update version, update date,
   users, rating, and any changed features):
   - {{extension name}}   (or write "ALL" to refresh every entry)

3. EDIT these entries with my own notes (use my words, don't rewrite them):
   - {{extension name}}: {{what to change or add}}

4. REMOVE these extensions:
   - {{extension name}}

5. REORDER the list by: {{my ranking / category / alphabetical / usage}}

RULES:

SOURCES AND ACCURACY
- Open each store URL and read the live page. Do not rely on memory.
- Use only facts found on the store page or the developer's own linked site.
- Never invent ratings, user counts, features, permissions, or privacy claims.
- If a field is missing or the page can't be read, write "Not listed" and tell me.
- Privacy statements must be phrased as "the developer states..." (a disclosure on the
  store listing, not an audit).
- Paraphrase the store description in your own words. Do not copy long passages.
- If an extension has been removed from the store or is unavailable, flag it instead of
  deleting it, and ask me what to do.

FORMAT (must match the existing file)
- Keep the title, the intro line with the "checked on" date, and the summary table.
- Update the "checked on" date to TODAY'S DATE.
- Summary table columns, in this order:
  Extension | Category | What it does | Users | Rating
  - Extension: link to the section anchor
  - Category: the store's category label
  - Users: as shown on the store page
  - Rating: "X.X (N ratings)"
- One numbered section per extension, separated by "---", using EXACTLY this layout:

    ## N. {{Extension name as shown in the store}}

    **Install:** [Chrome Web Store]({{store URL}})
    **Website:** [{{label}}]({{developer site URL}})      <- omit line if none listed
    **Offered by:** {{developer name}}                    <- only if shown on the page
    **Version:** {{x.y.z}} (updated {{Month D, YYYY}})
    **Works on:** {{site or scope}}                       <- only if limited to a site

    {{One or two sentence summary.}}

    ### Highlights            <- 4 to 8 bullets, most important first
    ### Privacy               <- or "Notes" when there's more to say
    ### Good for              <- one short line

- Keep the closing sections: "Installing and Managing Extensions" and "Notes".
- Keep bullet style, bold labels, and heading levels identical across all entries.
- Do not add emojis, marketing language, or personal claims I didn't provide.

OUTPUT
1. The complete updated file, created as a .md file.
2. A short CHANGE SUMMARY in chat, listing:
   - Added: ...
   - Refreshed: ... (show old -> new for version, users, rating)
   - Edited / Removed / Reordered: ...
   - Problems: anything you couldn't verify or that looks off
3. Do not change anything I didn't ask you to change.
```

---

## Reusable Entry Template

Copy this block when adding an entry by hand, or give it to Claude as the target format.

```markdown
## N. Extension Name

**Install:** [Chrome Web Store](https://chromewebstore.google.com/detail/...)
**Website:** [example.com](https://example.com)
**Offered by:** Developer Name
**Version:** 1.0.0 (updated Month D, YYYY)
**Works on:** example.com (only if scoped to a site)

One or two sentences describing what the extension does.

### Highlights

- Key feature
- Key feature
- Key feature

### Privacy

The developer states that it does not collect or use your data. (Or note the permissions
and data use disclosed on the listing.)

### Good for

Short line describing ideal use cases.

---
```

And the matching row for the summary table:

```markdown
| [Extension Name](#n-extension-name) | Category | What it does | 10,000 | 4.5 (120 ratings) |
```

> Anchor tip: GitHub builds anchors by lowercasing the heading, removing punctuation, and replacing spaces with hyphens. A heading like `## 3. SponsorBlock for YouTube - Skip Sponsorships` becomes `#3-sponsorblock-for-youtube---skip-sponsorships`.

---

## Quick Variants

Short prompts for common cases. Attach the current file with each.

**Add one extension**

```text
Add this extension to my attached Favorite-Chrome-Extensions.md using the same format
as the existing entries. Read the live store page and don't invent details. Update the
checked-on date to {{YYYY-MM-DD}}, add a summary table row, and give me a change summary.
URL: {{store URL}}
My note: {{optional}}
```

**Refresh all stats**

```text
Re-check every store page linked in my attached Favorite-Chrome-Extensions.md. Update
version, update date, users, and rating, plus any changed features. Set the checked-on
date to {{YYYY-MM-DD}}. Don't change anything else, and list old -> new values for
everything that changed. Flag any extension that is no longer available.
```

**Remove one extension**

```text
Remove "{{extension name}}" from my attached Favorite-Chrome-Extensions.md, delete its
table row, renumber the remaining sections, and fix the table anchors. Change nothing else.
```

**Audit only (no edits)**

```text
Read every store page linked in my attached Favorite-Chrome-Extensions.md and tell me
which entries are out of date or no longer match the store listing. Don't edit the file.
```

---

## Checklist Before Committing

- [ ] "Checked on" date updated
- [ ] Summary table row exists for every section, with working anchors
- [ ] Sections are numbered in order, with no gaps
- [ ] Every entry uses the same headings and field order
- [ ] Versions, users, and ratings match the live store pages
- [ ] Privacy lines say "the developer states..." and nothing stronger
- [ ] Nothing was changed that you didn't ask for
- [ ] `README.md` in the repo updated if you added or renamed files

## Why a fixed template?

- **Consistency:** every entry reads the same, so the file stays easy to scan.
- **Accuracy:** requiring live store pages and "Not listed" for missing data stops invented details.
- **Safe edits:** "change nothing else" plus a change summary makes updates easy to review.
- **Reusable:** the same prompt works months later, in any chat, without remembering the format.
