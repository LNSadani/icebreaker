---
description: Generate README with screenshot, commit everything, and push to GitHub
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, mcp__playwright__browser_navigate, mcp__playwright__browser_resize, mcp__playwright__browser_take_screenshot, mcp__playwright__browser_close
---

Do the following, in order:

1. **Capture a screenshot with Playwright.**
   - Detect the app's entry file (prefer `index.html`, else the first `*.html` at repo root).
   - Start a local static server in the background (e.g. `npx --yes http-server -p 8765 -s`) and wait until it responds.
   - Resize the browser to 1280x800, navigate to `http://127.0.0.1:8765/`, take a full-page PNG screenshot, and save it as `screenshot.png` at the repo root (overwrite if exists).
   - Close the browser and stop the background server task when done.

2. **Create or update `README.md`.**
   - If `README.md` is missing, generate one with: project title (from the `<title>` tag or folder name), one-paragraph description (inferred from the app's HTML/JS), a `![screenshot](screenshot.png)` embed, a "Running locally" section with the exact `npx http-server -p 8765` command, and a "Tech" line listing the stack actually in use.
   - If `README.md` exists but does not reference `screenshot.png`, insert the image embed right after the first heading.
   - Do not invent features that aren't in the code.

3. **Commit and push.**
   - Run `git status` to see what changed.
   - Stage only: `README.md`, `screenshot.png`, and any app source files (HTML/CSS/JS) at the repo root. Do **not** stage `.claude/`, `.playwright-mcp/`, or unrelated images.
   - Commit with a message that reflects what actually changed (new README vs. refreshed screenshot vs. both).
   - `git push` to the current branch's upstream. If there is no upstream, push with `-u origin <branch>`.
   - Report the resulting commit SHA and the pushed branch.

Stop and ask the user if: no HTML entry point is found, the repo has no git remote, or the working tree has unrelated staged changes you'd be about to bundle in.
