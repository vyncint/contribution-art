# contribution-art

A tracker for a [mossaic] contribution-art plan. There is no code here: one
scheduled workflow asks GitHub what has actually been contributed, compares it
against the plan, and posts the report to [issue #1](../../issues/1).

The plan being tracked:

| | |
| --- | --- |
| text | `VYNCINT` |
| year | 2026 |
| placement | from week 6, rows Mon–Fri |
| background | level 1 — the field the letters sit on |
| timezone | Asia/Ho_Chi_Minh |

**The plan is those inputs.** Changing `start-week` or `background` mid-year
compares against a *different* plan and reports nonsense confidently, so they
stay fixed until the year is over. The report prints the placement it used on
its second line; if that ever changes, so did the plan.

## How it was set up

Exactly the four steps in [mossaic's action guide][guide]:

1. A public repository — free Actions minutes, nothing else in it.
2. `.github/workflows/track.yml`, copied from [`track.example.yml`][example]
   with the `with:` block edited.
3. No secrets. The issue-comment route needs none; the Slack, Discord and
   email steps are still in the file but gated behind repository variables
   (`SLACK_ENABLED`, `DISCORD_ENABLED`, `EMAIL_ENABLED`), so turning one on is
   a switch and a secret rather than an edit.
4. Run once by hand from the Actions tab, rather than waiting for tomorrow.

The action is pinned to `vyncint/mossaic/action@v0.1.1`, not `@main`, so it
changes when I say so.

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
the way. `holed` means days inside the letters already have contributions, and
nothing takes those away — the text would read with holes in it. That last one
is not a warning to work harder; it is the year telling you it cannot be drawn
cleanly, and the report suggests a placement that would leave fewer holes.

[mossaic]: https://github.com/vyncint/mossaic
[guide]: https://github.com/vyncint/mossaic/blob/main/action/README.md
[example]: https://github.com/vyncint/mossaic/blob/main/action/track.example.yml
