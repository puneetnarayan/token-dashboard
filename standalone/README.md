# Standalone browser edition

`index.html` is a single self-contained file: no Python, no build step, no dependencies.
You pick your Claude Code logs in the browser and it parses and charts them locally.

## Use it

1. Open `index.html` (or the deployed URL).
2. Click **Choose projects folder** and select `~/.claude/projects`
   (Windows: `C:\Users\<you>\.claude\projects`). The folder is hidden: `Cmd+Shift+.` on macOS, `Ctrl+H` on Linux.
3. Or drag the folder onto the page, or use **Choose .jsonl files**. **Sample data** shows the UI with synthetic data.

Files are read in the browser and never uploaded; `vercel.json` ships a CSP with `connect-src 'none'` so the page cannot send data anywhere.

## Auto-refresh (Chrome / Edge)

**Connect folder (auto-refresh)** uses the browser's folder-access API. Pick `.claude/projects` once; the page remembers the folder and
re-scans every 60 seconds while the tab is open, reading only newly appended lines. Change the interval (15 s to 5 min, or Off) with the
**Refresh** menu, or click **Scan now**. After you reopen the page the browser may ask for one click to allow access again.
A website cannot read a fixed path like `C:\Users\<you>\.claude\projects` on its own; the browser always requires you to grant the folder.
Firefox and Safari do not support this API, so use **Choose projects folder** there. **Stop live** disconnects and forgets the folder.

## Deploy to Vercel

Import the repo, set the project **Root Directory** to `standalone`, framework preset **Other**, no build command.
Or run `npx vercel --prod` from inside `standalone/`.

## Differences from the Python dashboard

- No SQLite cache: logs are re-read when you load a folder (live mode re-reads only appended bytes).
- Prompt cost = every assistant turn after a prompt in the same session, ordered by timestamp.
- Tips use the newest 7 days *of the loaded data*, not the current date. Dismissals are kept in `localStorage`.
- No Skills tab. Days are UTC. Pricing is copied from `pricing.json`; update both if prices change.
