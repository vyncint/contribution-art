# contribution-art

A tracker for a [mossaic] contribution-art plan. There is no code here: one
scheduled workflow asks GitHub what has actually been contributed, compares it
against the plan, and posts the report to [issue #1](../../issues/1).

The plan being tracked:

| | |
| --- | --- |
| picture | [`heart.art`](heart.art) — 7 rows × 11 columns |
| year | 2026 |
| placement | from week 35: Sunday 30 August to 14 November |
| shades | 0 and 2 — empty, and a mid green |
| timezone | Asia/Ho_Chi_Minh |

```
·████·████·
███████████
███████████
███████████
·█████████·
···█████···
·····█·····
```

56 days at 35 contributions each — **1,960 in total** — and 21 days inside the
picture that have to stay dark. The last one falls on **11 November**, which
leaves fifty days of slack before the year does: a plan that lands on
31 December has no room for a week of illness.

It does **not** start in the week this plan was made. That week already had
contributions on it, and the picture's top-left corner is dark, so starting
there would have opened with a hole that nothing takes away. The first column
a picture can have is the first one still entirely in the future.

**The plan is those inputs.** Changing `start-week` mid-year compares against a
*different* plan and reports nonsense confidently, so it stays fixed until the
year is over. The report prints the placement it used on its second line; if
that ever changes, so did the plan.

### Why a picture and not text

A letter is five rows on Mon–Fri, two shades, and it has to fit the 5×5 font.
This is seven rows — the weekend included — thirteen columns, and any of
GitHub's shades per day. `matrix:` points the action at the `.art` file in this
repository, which is why the workflow now checks out the repo before running.

### Why two shades and not five

GitHub's five greens are not evenly spaced. Every *adjacent* pair is 9–20 ΔE
apart in the worst palette it ships, which is close enough to read as one
colour — so a picture using all five puts near-identical greens side by side
however carefully it is drawn. Level 0 against level 2 is ΔE 50: unmistakable.

It is also what makes this affordable. This graph's 2026 peak is 137, so a
level-4 day costs 110 contributions and a level-2 day costs 37. The same heart
in bright green would owe about 4,400 contributions instead of 1,960 — four
times this account's existing daily pace rather than roughly matching it.

## How it was set up

Exactly the four steps in [mossaic's action guide][guide]:

1. A public repository — free Actions minutes, nothing else in it.
2. `.github/workflows/track.yml`, copied from [`track.example.yml`][example]
   with the `with:` block edited.
3. No secrets. The issue-comment route needs none; the Slack, Discord,
   email and auto-commit steps are in the file but gated behind repository
   variables (`SLACK_ENABLED`, `DISCORD_ENABLED`, `EMAIL_ENABLED`,
   `AUTO_COMMIT_ENABLED`), so turning one on is a switch rather than an edit.
4. Run once by hand from the Actions tab (with optional `auto_commit` checkbox),
   rather than waiting for tomorrow.

The action is pinned to `vyncint/mossaic/action@v0.6.0`, not `@main`, so it
changes when I say so. `matrix:` arrived in 0.6.0.

## Two things GitHub does that will bite you

- **A scheduled workflow in a public repository is disabled after 60 days
  without commits.** GitHub emails first. A repository whose only job is a
  daily cron will hit this; push something occasionally, or re-enable it from
  the Actions tab.
- **`cron` is UTC, always.** `0 1 * * *` is 08:00 in UTC+7. That is why
  `timezone:` is set — otherwise the day the report calls "today" disagrees
  with the day the graph shades.

## Reading the report

`drawn` means finished. `reachable` means there is work left but nothing in
the way. `holed` means days inside the picture are already brighter than it
wants, and nothing takes a contribution away — the heart would read with holes
in it.

For a picture that is two kinds of damage rather than one: a day meant to stay
**dark** that has any contribution at all, and a day meant to be **level 2**
that has crept past 73 and would render as level 4. Both are permanent. The
plan starts today precisely so that neither has had a chance to happen yet —
every day it covers is still in the future.

[mossaic]: https://github.com/vyncint/mossaic
[guide]: https://github.com/vyncint/mossaic/blob/main/action/README.md
[example]: https://github.com/vyncint/mossaic/blob/main/action/track.example.yml
