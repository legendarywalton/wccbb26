# WCC Baseball Tournament 2026 — Bracket Tracker

Live-updating bracket for the 2026 West Coast Conference baseball tournament,
with running tournament stats for Pacific's JT (#27).

## Deploy

This is a single static HTML file. Drop it on GitHub Pages and it just works.

```bash
git push origin main
```

Then enable Pages on the repo: **Settings → Pages → Source: Deploy from a branch → main / root**.

If the repo is named `legendarywalton.github.io`, it'll publish at the root domain.
If it's named anything else (e.g. `WCCBB26.github.io`), it'll publish at
`https://legendarywalton.github.io/<repo-name>/`.

## How it works

- **Bracket**: static markup, hand-updated as games complete.
- **Stat cards** (AVG / R / RBI / HR / OBP / OPS): pulled live from ESPN's
  undocumented college-baseball API. Falls back through public CORS proxies
  (`corsproxy.io`, `allorigins.win`) if direct ESPN calls hit CORS blocks.
- **Persistence**: per-game raw counters (AB, H, R, RBI, HR, BB, HBP, SF, TB)
  stored in browser `localStorage` and recomputed from raw counters on each
  render — never sums rate stats across games.
- **Manual entry fallback**: collapsible diagnostics panel below the stat cards
  has a form to enter a box-score line by hand if ESPN's feed is unavailable.

## Player binding

JT is matched by jersey number, not name — change the `JERSEY` constant near the
top of the inline `<script>` to bind a different player.

## Troubleshooting

Expand the "Diagnostics & manual entry" panel to see the live sync log.
Each fetch attempt logs which tier (direct ESPN / corsproxy.io / allorigins)
succeeded or failed, what teams the scoreboard returned, and whether the
box-score parser found jersey #27 in Pacific's batting order.

Add `?reset=1` to the URL to wipe stored game data.
