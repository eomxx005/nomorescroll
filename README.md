# nomorescroll

Calm board games for kids 5-10. No ads (currently). No sign-up. No tracking. Global, multilingual.

## Languages

English (default) · 한국어 · 中文 · 日本語

Language selector at top right of every page. Choice is saved in `localStorage`. URL parameter `?lang=en|ko|zh|ja` also works on game pages.

## 8 Games

| # | File | Game | Age | Languages |
|---|------|------|-----|-----------|
| 1 | `games/tictactoe.html` | Tic-Tac-Toe / 삼목 / 井字棋 / 三目並べ | 5+ | en/ko/zh/ja |
| 2 | `games/nim.html` | Nim | 5+ | en/ko/zh (in-game toggle) |
| 3 | `games/connect4.html` | Connect Four / 커넥트 포 / 四子棋 / コネクトフォー | 6+ | en/ko/zh/ja |
| 4 | `games/gomoku.html` | Gomoku / 오목 / 五子棋 / 五目並べ | 6+ | en/ko/zh (in-game toggle) |
| 5 | `games/chess.html` | Chess / 체스 / 国际象棋 / チェス | 6+ | en/ko/zh (in-game toggle) |
| 6 | `games/reversi.html` | Reversi / 리버시 / 黑白棋 / リバーシ | 8+ | en/ko/zh/ja |
| 7 | `games/go.html` | Go / 바둑 / 围棋 / 囲碁 | 7+ | en/ko/zh (in-game toggle) |
| 8 | `games/baduk.html` | Baduk Class 바둑 교실 | 7+ | **Korean only** |

The 5 original games (Nim, Gomoku, Chess, Go, Baduk) keep their built-in language toggles. The 3 new games (Tic-Tac-Toe, Connect Four, Reversi) use the same i18n system as the home page.

The Korean-only Baduk Class card is automatically disabled when the home page is in en/zh/ja (with a "KO ONLY" badge).

## Folder Structure

```
nomorescroll/
  index.html              Home — game grid + language selector + parent gate
  about.html              For-parents page (4 langs)
  games/
    tictactoe.html        New (en/ko/zh/ja)
    connect4.html         New (en/ko/zh/ja)
    reversi.html          New (en/ko/zh/ja)
    nim.html              Original (en/ko/zh)
    gomoku.html           Original (en/ko/zh)
    chess.html            Original (en/ko/zh)
    go.html               Original (en/ko/zh)
    baduk.html            Original (Korean only)
  README.md
```

## Run Locally

No server required:

```bash
open index.html
```

Or with a tiny static server:

```bash
cd nomorescroll
python3 -m http.server 8000
# → http://localhost:8000
```

## Deploy to Vercel

1. Push to GitHub:
   ```bash
   git init && git add . && git commit -m "Initial nomorescroll"
   git branch -M main
   git remote add origin <your-repo>
   git push -u origin main
   ```
2. https://vercel.com → New Project → import repo
3. Framework Preset: **Other** (static, no build step)
4. Output Directory: `.`
5. Deploy

Default URL: `nomorescroll-xxx.vercel.app`. Custom domain in Settings → Domains.

Cost: $0 (Vercel Hobby plan).

## Parent Gate

A two-digit + two-digit addition (e.g. 17 + 28) appears before every game. New problem each time — no caching. Difficulty in `index.html` `generateProblem()`:

```js
const a = Math.floor(Math.random() * 80) + 11; // 11-90
const b = Math.floor(Math.random() * 80) + 11;
```

## Adding a Game

1. Drop the HTML in `games/` (e.g. `games/checkers.html`)
2. In `index.html`, add a card:
   ```html
   <button class="game-card" data-game="checkers">
     <span class="emoji">🎮</span>
     <h2 data-i18n="game_checkers_name">Checkers</h2>
     <p class="meta" data-i18n="game_checkers_meta">Age 7+ · 10 min</p>
   </button>
   ```
3. Add 4 translations in the `I18N` object: `game_checkers_name`, `game_checkers_meta`
4. (Optional) make the new game support `?lang=en|ko|zh|ja` URL param so language carries over

## Future: Ads

Currently no ads. If we add them later:
- Only quiet, non-tracking placements (e.g. EthicalAds, Carbon Ads, or a self-served sponsor strip)
- Never between game cards or inside game pages — only fixed slots (e.g. footer)
- The `about.html` promise text will be updated honestly

The codebase has no ad slots currently. Adding one later means a single block in `index.html` footer + one entry in the i18n dictionary.

## License

Game code: original authors. Site code: free to reuse.
