# Vision — performance dashboard (GitHub Pages)

Static site for Binance Copy Trading lead profile link.

## 1. Generate data

From `Desktop`:

```powershell
cd c:\Users\user\Desktop

# First time (slow — fetches APIs, ~10–20 min):
python export_vision_site.py --run-backtest --fetch-live

# Later — refresh live equity only:
python export_vision_site.py --fetch-live
```

Edit `vision_site_config.json` on Desktop — paste your **Binance Vision copy-trade URL**, then re-run export.

## 2. Preview locally

Double-click `vision_results/index.html` or:

```powershell
start c:\Users\user\Desktop\vision_results\index.html
```

## 3. Publish free on GitHub Pages

1. Create GitHub account (if needed).
2. New **public** repo, e.g. `vision-results`.
3. Upload everything inside `vision_results/` (including `data/` folder).
4. Repo → **Settings** → **Pages** → Source: **main** branch, folder **/ (root)** → Save.
5. Your URL: `https://YOUR_USERNAME.github.io/vision-results/`

Paste that URL in Binance Vision description.

## 4. Daily auto-update (Windows)

Install a scheduled task (runs every day at **12:00** local time — full backtest + refresh `data/portfolio.js`):

```powershell
cd c:\Users\user\Desktop
Set-ExecutionPolicy -Scope Process Bypass -Force
.\install_vision_site_task.ps1
```

To change the time, edit `$UpdateTime` in `install_vision_site_task.ps1` and re-run.

Test manually:

```powershell
.\run_vision_site_update.ps1
```

Logs: `vision_results\logs\site_update_*.log`

If `vision_results/` is a git clone with `origin` set (GitHub Pages), the script auto-commits and pushes `data/portfolio.js` after each successful update.

## 5. Manual update

```powershell
python export_vision_site.py --run-backtest
```

Then push updated `data/portfolio.js` to GitHub if you publish via Pages.
