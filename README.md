# Pool Chip Tournament

A single-page web app for running a pool chip tournament.

## How the tournament works

- Each player starts with a number of chips set by the director (1–9).
- Losing a match costs one chip. A player at zero chips is out.
- The last player with chips wins.

## How matches are drawn

When a table frees up, the app fills it right away:

1. Only players who are free, still in, and not marked away can be drawn.
2. **Draw pace** limits how far ahead a player can get:
   - *Strict rounds*: everyone plays once before anyone plays again.
   - *Balanced* (default): a player can start a new match only if they are at most one match ahead of whoever has played the fewest.
   - *Fastest*: tables always refill with whoever is free.
3. The first player is the one with the fewest matches played, then the longest wait, then a random pick.
4. Their opponent is chosen the same way. The app also prefers someone they've played the fewest times, and never their last opponent.
5. If the only free pair just played each other, the table waits for another match to finish. Once only two players are left, rematches are allowed.
6. Random picks use `crypto.getRandomValues`.

The director can always tap **Start a match here anyway** to override a held table.

## Corrections

- **Swap winner** or **Remove result** on any finished match in the match log.
- **Add/remove a chip**, **Mark away**, or **Withdraw** a player from the chip count.
- **Cancel match** on a table if a pairing should not be played.

Chip counts are always recalculated from the match log, so a correction never leaves the counts out of sync. If a correction knocks out a player who is mid-match, that match is cancelled and the table is redrawn.

## Hosting

Open `index.html` in a browser, or enable GitHub Pages for this repo (Settings → Pages → deploy from the `main` branch).

When hosted outside Claude, the tournament is saved in that browser's local storage. Use one device as the director's device. Live syncing to players' phones works in the Claude-hosted version of the page.
