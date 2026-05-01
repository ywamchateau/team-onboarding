# YWAM Château — Team Onboarding

Welcome to the YWAM Château team. This is the **one-time Mac setup** every new contributor needs to do before working on any of our projects.

Time required: **~15 minutes total.** Most of it is downloads running in the background — your active time is ~5 minutes.

You **don't need to be a developer** to follow this. Every step is a click, a paste, or a one-line terminal command. After this is set up once, you'll never reinstall anything — new project = clone the repo + open Claude Code = ready.

---

## 🔗 Where the website lives

Bookmark these — you'll come back to them every day:

| URL | What it is |
|---|---|
| **https://ywam-chateau-site.pages.dev/** | **Production** — the live website. What the public sees. (Eventually `https://ywamchateau.com` once DNS is pointed.) |
| **https://staging.ywam-chateau-site.pages.dev/** | **Staging / test URL.** Where new changes land for review before they go to production. (Eventually `https://test.ywamchateau.com`.) |

When you ship a change with `/yc-ship` (Lane 2 — test first), it appears on staging in ~60 seconds. When you `/yc-promote`, it moves to production in another ~60 seconds.

Other useful URLs:
- **Website GitHub repo (private):** https://github.com/ywamchateau/ywam-chateau-site
- **Design system repo (public):** https://github.com/ywamchateau/design-system
- **🎨 Design system rendered (live page):** https://ywamchateau.github.io/design-system/ — colors, type, components, logos visible at a glance
- **This onboarding doc (public):** https://github.com/ywamchateau/team-onboarding
- **Cloudflare dashboard:** https://dash.cloudflare.com (ask the admin if you need access to view deploy logs)

---

## What you'll install

| Tool | Purpose | Cost |
|---|---|---|
| **GitHub account** | Where the code lives | Free |
| **Homebrew** | Mac package manager (used to install gh + Node) | Free |
| **gh CLI** | GitHub command-line tool — handles auth + lets Claude Code push for you | Free |
| **Node.js** | Runs websites locally on your Mac for previews | Free |
| **Claude Code** | Where the actual editing happens — talk to it in plain language | Team plan |

Most YWAM team members already have Claude Code installed for other work — in that case, just sign into the team account and skip the download.

Total time: **~15 min**. No GitHub Desktop, no IDE, no other tools.

---

## Step 0 · Get access (the team admin does this)

The team admin (currently Vince Licari, vl@ywamchateau.com) needs to:

1. Add you as a collaborator on the project repos you'll work on (e.g., `ywamchateau/ywam-chateau-site`)
2. Invite you to the YWAM Château Anthropic team plan (so you can use Claude Code)
3. (Optional) Add you to Cloudflare so you can see deploy logs

You'll get email invites for each. **Accept them before continuing.**

---

## Step 1 · GitHub account (~2 min)

Skip this if you already have a GitHub account.

1. Go to **https://github.com**
2. Click **Sign up**
3. Use your **work email** (whatever you use for YWAM)
4. Verify your email when GitHub sends the confirmation
5. **Send your GitHub username to the team admin** so they can add you to the repos

---

## Step 2 · Install Homebrew + gh CLI + authenticate (~7 min)

Open the **Terminal app** (Spotlight: ⌘+Space → "Terminal" → Enter). This is the only time in the whole setup you'll touch the terminal directly. Once gh CLI is installed and authenticated, Claude Code handles everything for you.

### 2.1 — Install Homebrew

Paste this whole command into Terminal, press Enter:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**What happens:**
1. It asks for your **Mac password**. Type it (you won't see any characters — that's normal). Press Enter.
2. The install runs for ~3 minutes. You'll see a lot of scrolling output.
3. When it finishes, your normal Terminal prompt returns. It usually looks like `yourname@MacBook ~ %` (the `%` symbol is the key signal).

**Stuck — how do I know it's actually done?** Look for the `%` (or `$`) at the end of the last line. If you see that and the cursor is blinking next to it, you're back at the prompt and ready for the next step.

**If you don't see a prompt and the cursor isn't blinking next to a `%`,** press **Control+C** (hold Control, tap C). That cancels whatever's running and returns you to a fresh prompt. Then continue.

> ℹ️ Homebrew prints a "**==> Next steps:**" section telling you to manually paste 2–3 lines. **You can ignore it.** Step 2.2 below does the same thing in one paste — and it tells you when it worked.

### 2.2 — Wire Homebrew into your shell + verify it worked (1 paste)

Once you're back at the prompt (the `%` symbol), **paste this whole one-liner** into Terminal and press Enter:

```
eval "$(/opt/homebrew/bin/brew shellenv)" && (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> ~/.zprofile && echo "" && echo "✅ Homebrew is ready. $(brew --version | head -n 1)"
```

This single line:
- Activates Homebrew in your current Terminal session
- Wires it permanently into future Terminal windows (via `~/.zprofile`)
- Prints a green check + the Homebrew version so you can **see** it worked

**You should see exactly this:**

```
✅ Homebrew is ready. Homebrew 4.x.x
```

If you see that ✅ line, you're done. Skip to step 2.3.

**If you see something else (errors, `command not found`, etc.):**
- Most common cause: the Homebrew install in step 2.1 hadn't fully finished when you ran this. Wait 30 seconds, scroll up to confirm you saw `Installation successful!` earlier in the output, then try again.
- If you're on a pre-2020 Intel Mac (rare): swap `/opt/homebrew` for `/usr/local` in the command above.
- Still stuck? Screenshot your Terminal and send it to the admin.

### 2.3 — Install gh CLI

Still in Terminal:

```
brew install gh
```

Takes ~30 seconds. **You'll know it worked** when you see your `%` prompt return and the last line of output mentions `gh` (something like `==> Summary` or a sparkle icon followed by the install path). If `brew` says `command not found`, step 2.2 didn't fully take — close Terminal, reopen it, and try `brew install gh` again.

### 2.4 — Authenticate with GitHub

```
gh auth login
```

Walk through the prompts — exact answers:

1. **What account do you want to log into?** → use ↓ arrow if needed to highlight `GitHub.com`, press Enter
2. **What is your preferred protocol for Git operations on this host?** → `HTTPS`, press Enter
3. **Authenticate Git with your GitHub credentials?** → `Yes`, press Enter
4. **How would you like to authenticate GitHub CLI?** → `Login with a web browser`, press Enter
5. It shows a one-time code (something like `ABCD-1234`) — **copy that code to your clipboard** (highlight it, ⌘+C)
6. Press Enter — your default browser opens to a GitHub page
7. Paste the code (⌘+V), click **Authorize**, close the browser tab
8. Switch back to Terminal — you should see this confirmation:

```
✓ Authentication complete.
✓ Logged in as <yourgithubusername>
```

**If you see those two `✓` lines — auth is done.** Move to Step 2.5 to verify your name. (Terminal will still come up briefly in Steps 3 and 4 to clone the repo and install Node, but those are one-line pastes — no more multi-step prompts.)

**If you don't see those `✓` lines after ~30 seconds:** the browser auth probably timed out. Close Terminal, reopen it, and run `gh auth login` again.

### 2.5 — Verify your git name (1 paste)

Every commit you make will show your name in the Cloudflare deploy list and the project's git history. The website repo enforces this via a git hook — your commits will be **rejected** if your `git config user.name` is empty or looks like a GitHub handle. Best to fix it now before your first commit.

Paste this one-liner to check + get a fix command if needed:

```
NAME=$(git config user.name); echo "Current: $NAME"; FIRST=$(echo "$NAME" | awk '{print $1}'); WORDS=$(echo "$NAME" | awk '{print NF}'); if [ -z "$NAME" ] || echo "$NAME" | grep -qE "^[a-z0-9_-]+$"; then echo ""; echo "❌ This will be REJECTED by the commit hook (looks like a GitHub handle)."; echo "Fix it now:"; echo '   git config --global user.name "Your Real Name"'; elif [ "$WORDS" = "1" ] && [ "$(echo "$NAME" | wc -c)" -gt 8 ]; then echo ""; echo "⚠️  Single long word — looks smushed. Commits will work but the prefix will be ugly."; echo "Recommend setting with a space:"; echo '   git config --global user.name "First Last"'; else echo "✅ First name extracted: $FIRST — looks good. Your commits will start with \"$FIRST: ...\""; fi
```

You'll see one of:
- **`✅ First name extracted: Sarah — looks good.`** → you're set, move to Step 3.
- **`⚠️  Single long word — looks smushed.`** → your name has no space. Recommended: `git config --global user.name "First Last"` so your prefix becomes `First:` instead of `FirstLast:`.
- **`❌ This will be REJECTED by the commit hook.`** → run `git config --global user.name "Your Real Name"` (with your actual real name in quotes) and paste the verifier again.

> **Why this matters:** every commit subject in the website repo starts with the author's first name (e.g., `Sarah: copy: update DTS price`). The Cloudflare deploy dashboard shows commit subjects, so this makes it instantly clear who shipped what. The git hook lives at `.githooks/prepare-commit-msg` and runs automatically — no extra steps from you, just keep your `user.name` set to a real name and it works.

---

## Step 3 · Clone the project (~30 sec)

Still in Terminal (last time, promise). Paste this exactly — no edits needed:

```
mkdir -p ~/Documents/GitHub && cd ~/Documents/GitHub && gh repo clone ywamchateau/ywam-chateau-site
```

That downloads the website project to `~/Documents/GitHub/ywam-chateau-site`. Done.

> If you've been added to additional YWAM Château repos (e.g., a new microsite later), clone those the same way: `gh repo clone ywamchateau/<repo-name>`. Each project lives in its own folder under `~/Documents/GitHub/`.

---

## Step 4 · Install Node.js (~30 sec)

Node.js is what runs the websites locally on your Mac for previews. You'll never use it directly — Claude Code runs it for you.

Since Homebrew is already installed from Step 2, this is one command. In Terminal:

```
brew install node
```

Takes ~30 seconds. No password needed.

You don't need to test anything. Claude Code will tell you if something's wrong.

> If you'd rather use the GUI installer, you can download from https://nodejs.org instead (click the green LTS button, open the .pkg, walk through). But brew is faster.

---

## Step 5 · Open Claude Code with the team account (~2 min)

Claude Code is where you'll do all the work. You talk to it in plain language.

**If you don't have Claude Code installed yet:**
1. Download from **https://claude.ai/download** (or check Anthropic's docs for the current download link)
2. Drag to Applications

**If you already have Claude Code installed** (most YWAM team members do — used for other work), skip the download step.

**Either way, then:**

1. Open Claude Code
2. **Sign in with the YWAM Château team account** the admin shared with you. If you're already signed into a personal Claude account, you may need to switch accounts or sign in via Settings → Account → Add account.
3. Once signed into the team account, **open the cloned project folder as a new project** (e.g., `~/Documents/GitHub/ywam-chateau-site`)

---

## Step 6 · Start your first session (~2 min)

In Claude Code at the project folder, **type this and press Enter**:

```
/yc-orient
```

That's it. The `/yc-orient` command is a slash command that lives inside the project repo — it tells Claude to read `CLAUDE.md` and `WORKFLOW.md`, check recent git history, summarize the project state for you, and ask what you'd like to work on.

> **If `/yc-orient` doesn't autocomplete or work**, the slash commands haven't loaded yet. Either restart Claude Code, or paste this fallback message:
>
> ```
> Read CLAUDE.md and WORKFLOW.md, then run `git log --oneline -20`
> and `git status -b`. Tell me what you understand about the project
> and what state we're in.
> ```
>
> The slash command does the same thing — just shorter to type. **Use `/yc-orient` at the start of every new session** so Claude is fully caught up before you give it a task.

### What happens next

After Claude orients itself, it'll ask **"What would you like to work on?"**

Tell it your task in plain language. Examples:

- *"I want to build the DTS page from scratch."*
- *"Change the homepage hero copy from X to Y."*
- *"Apply this Claude Design export — here's the file."*
- *"Add this photo to the community section."*

Claude will then **recommend a model** for that task (see below) and start working.

### 🎯 Choose your model

In the top of the conversation window there's a model selector. Default for daily work:

🎯 **Claude Sonnet 4.6 — medium effort**

Sonnet is fast, capable, and stretches the team's quota furthest. For most of what you'll do — copy edits, photo additions, page tweaks, /yc-ship and /yc-promote flows — Sonnet handles it perfectly while keeping turns snappy.

> **If your model selector shows a newer Sonnet** (4.7, 5.0, etc. — Anthropic rolls versions forward periodically), use that one. The principle stays the same: current Sonnet for routine work, current Opus for complex tasks.

**Switch to Claude Opus 4.6 — high effort** when the task is genuinely complex:
- Applying a Claude Design export with the merge gate (especially with new photos or structural changes)
- Multi-file refactors
- Designing a new page from scratch
- Debugging an unexpected build error

You can switch mid-conversation if the complexity changes. Just click the model selector at the top.

**Why not Opus all the time?** Opus burns through quota ~3–5× faster than Sonnet and turns are noticeably slower. For routine work guided by `CLAUDE.md` (which the project already has), Sonnet is plenty. Save Opus for when you actually need its extra reasoning.

Claude will recommend the right one based on your task. You can override if you want.

### Bookmark these URLs

You'll be checking these throughout the day after every `/yc-ship` and `/yc-promote`:

- **Production:** https://ywam-chateau-site.pages.dev/ — the live site
- **Staging:** https://staging.ywam-chateau-site.pages.dev/ — where new changes go for review

### You're done with setup

From here, normal work is just talking to Claude Code in plain language. **Always start a new session with `/yc-orient`** so context is loaded the same way every time. Sonnet sessions tend to be shorter than Opus, so you'll likely run `/yc-orient` several times a day — that's fine, it's fast.

---

## How daily work feels (after setup)

Examples of what you'd say:

- *"Change the price on the DTS page from $8,990 to $9,200."*
- *"Add this photo to the homepage hero."* (drag a photo into the chat)
- *"What does the apply page look like right now?"*
- *"I want to start designing the DBS page."*

What Claude Code does in response:

| You | Claude Code |
|---|---|
| Tell Claude in plain language what to change | Edits the right files, runs the build, shows you the diff |
| Confirm | Commits + pushes via gh CLI (no extra step from you) |
| Wait ~60 seconds | Cloudflare auto-deploys to **staging.ywam-chateau-site.pages.dev** (Lane 2) or **ywam-chateau-site.pages.dev** (Lane 1, direct to prod) |
| Refresh the URL | See your change live |

**You never need to:**
- Touch the terminal directly (after setup)
- Run git commands manually
- Edit code by hand
- Configure deploy infrastructure

You just need to **say what you want changed in plain English** and confirm when Claude shows you the diff.

---

## When you're stuck

| Problem | What to do |
|---|---|
| "Claude says my build failed" | Paste the error to Claude — usually fixes itself in one round. If not, ping the team admin. |
| "My push got rejected" | Tell Claude *"pull origin first then push"* — usually a sync issue, fixes itself. |
| "My changes aren't on the website" | Wait ~60 seconds (Cloudflare deploys take that long). Still missing? Ask Claude to check the latest deploys. |
| "Claude Code can't find the repo" | In Claude Code, point the project at the correct cloned folder (e.g., `~/Documents/GitHub/<project-name>`). |
| "I broke something in production" | Tell Claude *"revert the last commit on main"* — fix is live in ~2 min. Or use Cloudflare's dashboard to roll back. |
| "gh auth expired" | Run `gh auth login` in Terminal again, walk through the same prompts. |

---

## What's tied to your machine vs. what's shared

This setup runs on YOUR Mac. The setup itself doesn't sync to other machines — every team member runs through this guide once on their own laptop.

**What IS shared automatically (via the project repo):**

- All workflow rules and decisions (in `CLAUDE.md`, `WORKFLOW.md` of each project)
- Slash commands (`/yc-orient`, `/yc-ship`, `/yc-promote`, `/yc-export-for-design`) — they live inside the repo
- Permission allowlist for routine commands

**What stays per-machine:**

- Your GitHub login (handled by gh CLI)
- Your Claude Code session
- Homebrew + gh CLI installations
- Local clone of each project repo

---

## Optional but useful

### GitHub Desktop (visual git fallback)

Most days you won't need it — Claude Code handles git via gh CLI. But for one-off situations where you want to *visually* review a complicated diff, see branch state, or resolve a merge conflict, the GitHub Desktop app is the friendliest tool.

If you want it:
1. https://desktop.github.com → Download for macOS
2. Drag to Applications, sign in with GitHub
3. **File → Add Local Repository...** → point at your already-cloned project folder

It'll just work — no separate auth, no re-cloning. It uses the same gh CLI credentials you set up in Step 2.

### Cloudflare account

If you'll be debugging deploy issues, ask the admin to add you to the YWAM Château Cloudflare account. Lets you watch builds in real time, read deploy logs, and roll back a bad deploy in 30 seconds.

### Claude Design

For visual design work (new pages, photo placement), the team uses **Claude Design** at https://claude.ai/design. It's a separate product from Claude Code (not integrated) — the two don't share files automatically, so the round trip is manual.

**The full round trip:**

1. **Export the current page from Claude Code using the `/yc-export-for-design` slash command.** In your Claude Code session, type:
   ```
   /yc-export-for-design
   ```

   That bundles the homepage to `~/Downloads/homepage.bundled.html`. To bundle a different page, pass it as an argument:
   ```
   /yc-export-for-design dts
   ```
   Valid pages: `homepage` (default), `dts`, `dbs`, `spl`, `apply`, `about`.

   The skill builds the site, inlines the CSS, and rewrites every photo and font path to point at the live staging deployment so Claude Design renders the page correctly when uploaded. Output is ~120 KB.

   > ⚠️ **Don't try to do this by hand or with a freeform prompt.** A naive "save the page as HTML" produces a broken file — Astro's photo and font paths are root-relative and 404 outside a webserver. The slash command is the only correct way; it exists because the manual approach has bitten the team before.

2. **Upload that file to Claude Design** at https://claude.ai/design as the starting point. Claude Design now sees the real, current state of the live page — not a blank canvas.

3. **Iterate visually in Claude Design.** Move things, swap photos, try copy variants — whatever the visual decision is.

4. **Export the result from Claude Design** (download the updated HTML).

5. **Hand the export back to Claude Code**, say *"apply this to staging"* and attach (or paste the path to) the exported file.

6. **Claude Code runs the "merge gate"** — it diffs the export against the current repo, surfaces what changed (text, photos, structure, tokens), and applies only the visual decisions while preserving the tokenized design system. You review the diff, then `/yc-ship` to staging.

> ⚠️ **Always export from Claude Code first** (step 1) before opening Claude Design. If you start from scratch in Claude Design, the merge gate has nothing to diff against and you'll lose the tokenized styles. Round-tripping the current page in keeps the design system intact.

Each project's `WORKFLOW.md` explains when to use Claude Design vs Claude Code. Default to Claude Code unless you're making a real visual decision.

---

## The repos

| Repo | Visibility | What it contains |
|---|---|---|
| **`ywamchateau/team-onboarding`** | Public | This setup guide (you're reading it) |
| **`ywamchateau/design-system`** | Public | Canonical design system: tokens, fonts, logos, brand voice. Project repos snapshot from here. |
| **`ywamchateau/ywam-chateau-site`** | Private | The marketing website (the active project right now) |

When you're added as a collaborator on a project repo, that project's own `CLAUDE.md` and `WORKFLOW.md` files will tell you everything specific to it.

**You don't need to manually clone the design system** — but if a Claude Code session ever needs to reference it (e.g., "what's the latest token for `--gold-deep`?"), you can ask Claude to fetch it via `gh repo clone ywamchateau/design-system /tmp/design-system`. Claude can also use `gh api` to grab a single file without cloning the full 33 MB.

---

## Maintaining this guide

Found a step that doesn't work, or a new tool we should add? Edit this README and submit a Pull Request, or just message the team admin.

This is a **living document** — when something changes (new tool, new policy, OS update breaks something), we update this so the next person doesn't hit the same wall.
