# Standalone browser edition

`index.html` is a single self-contained file: no Python, no build step, no dependencies.
You pick your Claude Code logs in the browser and it parses and charts them locally.

## Use it

1. Open `index.html` (or the deployed URL).
2. Click **Choose projects folder** and select `~/.claude/projects`
   (Windows: `C:\Users\<you>\.claude\projects`). The folder is hidden: `Cmd+Shift+.` on macOS, `Ctrl+H` on Linux.
3. Or drag the folder onto the page, or use **Choose .jsonl files**. **Sample data** shows the UI with synthetic data.

Files are read in the browser and never uploaded; `vercel.json` ships a CSP with `connect-src 'none'` so the page cannot send data anywhere.

## Deploy to Vercel

Import the repo, set the project **Root Directory** to `standalone`, framework preset **Other**, no build command.
Or run `npx vercel --prod` from inside `standalone/`.

## Differences from the Python dashboard

- Logs are re-read each time you load them (no SQLite cache, no live refresh).
- Prompt cost = every assistant turn after a prompt in the same session, ordered by timestamp.
- Tips use the newest 7 days *of the loaded data*, not the current date. Dismissals are kept in `localStorage`.
- No Skills tab. Days are UTC. Pricing is copied from `pricing.json`; update both if prices change.
