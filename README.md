# Silicon Cycle

A tower defense game about running a semiconductor portfolio through the boom-and-bust cycle. One HTML file, no dependencies, no network calls, no tracking.

**[Play it →](https://mark-florentino.github.io/silicon-cycle/)** *(update this link once Pages is live)*

---

## The idea

Bear forces walk the fab floor toward your book. You stop them by building positions across the semiconductor stack — analog, memory, fabless, foundry, lithography, equipment, EDA.

Two clocks run at once, and they disagree:

- **Short term.** The silicon cycle swings continuously between downcycle and upcycle. Positions are cheap in the trough and clears pay a premium at the peak. The oscillator forecasts the next 30 seconds, so the shape is knowable — only your timing isn't.
- **Long term.** Every wave you hold a position, it compounds damage and pays a bigger dividend. Selling for quick cash, or taking profits, resets all of it to zero.

Conviction accrues at the end of each wave and buys permanent structural edge on the thesis tree. You bank an extra point for any wave in which you didn't sell or realize anything.

Clear **wave 30** to confirm the thesis. Endless waves continue after that, and the health curve is quadratic — eventually the cycle wins.

## How to play

1. Pick a position from the desk beneath the floor, then tap an empty pad to place it.
2. Send waves in when you're ready. Going early pays a front-run bonus that scales with the speed you're running.
3. Tap a placed position to upgrade, take profits, or sell.
4. Open the **Book** to spend conviction, read the threat counters, and study the cycle.

A four-step walkthrough runs on a first game and can be skipped from the splash.

## Positions

| Ticker | Position | Cost | Role |
|---|---|---:|---|
| `ADI/TXN` | Analog & Power | $60 | Cycle-immune, chills what it hits |
| `MU/HYNIX` | Memory | $85 | Cheapest damage, swings ±65% with the cycle |
| `NVDA/AMD` | Fabless AI | $150 | Rapid fire; breaks regenerating shields |
| `TSM` | Foundry | $190 | Splash damage against clustered waves |
| `ASML` | EUV Lithography | $320 | Enormous single-target reach; the boss answer |
| `AMAT/LRCX` | WFE / Capex | $170 | Support aura: fire rate to neighbours |
| `CDNS/SNPS` | EDA & IP | $140 | Support aura: reveals cloaked threats, grants crit |

Each position picks a permanent A/B path at tier 2, and caps at tier 4.

## Threats

Every threat has a position that answers it cleanly. Entries unlock in the Threat Book the first time one appears.

| Threat | What it does | Counter |
|---|---|---|
| Retail Panic | Bulk, unclever | Anything |
| Memory Glut | Fast, fragile, enormous numbers | Foundry splash |
| Export Controls | Heavy armour blunts small hits | EUV on High-NA |
| Short Raid | Very fast, immune to slowing | Circuit Breaker |
| Gray Market | Untargetable until revealed | EDA & IP |
| Rate Hike | Shield regenerates after 3 quiet seconds | Fabless AI |
| Capex Freeze | Heals 2.2% per second | Sustained output |
| Inventory Cascade | Splits in two when it breaks | Foundry near the entrance |
| Silicon Winter | Boss; aura suppresses nearby fire rate | EUV parked outside the aura |

## Abilities

Both charge on wall-clock time, so changing speed doesn't alter how long you wait.

- **Circuit Breaker** (`Q`, 34s) — a trading halt. Every threat drops to 30% speed for 5 seconds, immunity or not.
- **Tiger Team** (`W`, 58s) — a failure-analysis crew sweeps the entire route from the core outward in 11 seconds.

Fire both so their windows overlap and you trigger a **Supercycle**: double bounty for the duration, plus conviction.

## Accessibility

Under **Book → Display**:

- Text size at three steps, scaling the interface *and* the text drawn on the floor
- High contrast, lifting dimmed labels from 2.5:1 to 6:1
- Bigger board markers, 30% larger threats and positions
- Reduce motion, stopping pulses, shake and confetti

Colour is never the only signal — costs print their shortfall, abilities read *Ready* or *Charging*, and threats carry their ticker.

## Technical notes

- **One file.** Roughly 150 KB of HTML, CSS and JavaScript. No build step, no bundler, no dependencies.
- **No network.** Zero external requests. Fonts are system stacks; the glyph atlas is generated at runtime onto a canvas.
- **No storage.** Nothing is written to `localStorage` or cookies, so nothing persists between visits — including display settings.
- **Rendering.** Custom WebGL2 renderer (falls back to WebGL1) with a single SDF shader batching every shape through one draw call. Handles a full board at wave 110+ in about 9ms of CPU per frame.
- **Two maps.** A 13×14 portrait board for phones and a 24×14 landscape board for wider screens, chosen by the device's short side. Enemy speed is normalised against route length, so both play identically.
- **Orientation.** Portrait only on phones; rotating landscape shows a prompt and holds the floor.

Tested on iOS Safari, Chrome and Firefox. Requires WebGL.

## Modifying it

Most of the balance lives in a handful of readable constants near the top of the script:

- `TOWERS` — cost, damage, rate, range, and both upgrade paths per position
- `ENEMIES` — health, speed, bounty, and the counter text shown in the Threat Book
- `WAVES` — the hand-authored first 20 waves; later ones are generated
- `waveHpMul()` — the difficulty curve. The quadratic term is what eventually ends every run.

## License

MIT — see [LICENSE](LICENSE). Copyright © 2026 Mark Florentino LLC.
