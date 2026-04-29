# YWAM Château — Team Onboarding

Welcome to the YWAM Château team. This is the **one-time Mac setup** every new contributor needs to do before working on any of our projects (websites, internal tools, etc.).

Time required: **15–25 minutes total.** Most of that is downloads running in the background — your active time is ~5 minutes.

You **don't need to be a developer** to follow this. Every step is a click, a paste, or a one-line terminal command. The whole point of this setup is so you never need to touch the terminal in normal day-to-day work — you'll just talk to **Claude Code** in plain language.

---

## What you'll install

| Tool | Purpose | Cost |
|---|---|---|
| **GitHub account** | Where the code lives | Free |
| **GitHub Desktop** | Visual app for syncing code to/from GitHub | Free |
| **Node.js** | Runs websites locally on your Mac for previews | Free |
| **Claude Code** | Where the actual editing happens — talk to it in plain language | Team plan |
| **Homebrew** | Mac package manager (one-time, used to install gh CLI) | Free |
| **gh CLI** | GitHub command-line tool — lets Claude Code push your changes for you | Free |

After this is set up once, you don't reinstall anything. New project = clone the project repo + open Claude Code in that folder = ready.

---

## Step 0 · Get access (the team admin does this)

The team admin (currently Vince Licari, vl@ywamchateau.com) needs to:

1. Add you as a collaborator on the project repos you're working on (e.g., `ywamchateau/ywam-chateau-site`)
2. Invite you to the YWAM Château Anthropic team plan (so you can use Claude Code)
3. (Optional) Add you to Cloudflare so you can see deploy logs

You'll get email invites for each. **Accept them before continuing to Step 1.**

---

## Step 1 · GitHub account (~2 min)

Skip this if you already have a GitHub account.

1. Go to **https://github.com**
2. Click **Sign up**
3. Use your **work email** (whatever you use for YWAM)
4. Verify your email when GitHub sends the confirmation
5. **Send your GitHub username to the team admin** so they can add you to the repos

---

## Step 2 · GitHub Desktop (~3 min)

This is the visual app for syncing code. **You'll never need terminal git** — this app handles everything.

1. Go to **https://desktop.github.com**
2. Click **Download for macOS**
3. Open the downloaded `.zip` file, drag the **GitHub Desktop** app into your Applications folder
4. Open GitHub Desktop from Applications (or Spotlight: ⌘+Space → "GitHub Desktop")
5. Click **Sign in to GitHub.com** when prompted, follow the browser flow
6. When asked, allow GitHub Desktop to use your Mac's keychain — that lets it remember your login
7. On the "Configure Git" screen, your name and email auto-fill from your GitHub account. Confirm.

---

## Step 3 · Clone your first repo (~1 min)

"Cloning" = downloading a working copy of the project's code to your Mac.

1. In GitHub Desktop, click **File → Clone Repository...**
2. The "GitHub.com" tab should be selected. You'll see the repos you've been added to (e.g., `ywam-chateau-site`).
3. Click the one you're working on
4. **Local path:** click **Choose...** and pick `~/Documents/GitHub/`. The project folder will be created inside.
5. Click **Clone**

Cloning takes about 5 seconds.

---

## Step 4 · Install Node.js (~3 min)

Node.js is what runs the websites locally on your Mac for previews. You'll never use it directly — Claude Code runs it for you.

1. Go to **https://nodejs.org**
2. Click the big green **LTS** button (the recommended version)
3. Open the downloaded `.pkg` file
4. Walk through the installer — just click **Continue**, agree to terms, install. No choices to make.
5. Enter your Mac password when prompted
6. When it says "Installation complete," close the installer

You don't need to test anything. Claude Code will let you know if something's wrong.

---

## Step 5 · Install Claude Code (~5 min)

Claude Code is where you'll actually do work. You talk to it in plain language and it makes the changes for you.

1. Download Claude Code from **https://claude.ai/download** (or check Anthropic's docs for the current download link)
2. Drag to Applications
3. Open Claude Code
4. Sign in with the **team account** the admin shared with you
5. Inside Claude Code, **open the cloned project folder as a new project** (e.g., `~/Documents/GitHub/ywam-chateau-site`)

You should see Claude Code "knows" about the project and is ready for instructions.

---

## Step 6 · Install Homebrew + gh CLI (~7 min)

This step lets Claude Code push your changes to GitHub directly, so you don't have to click "Push" in GitHub Desktop after every edit.

It's a **one-time install.** You won't touch the terminal again after this.

### 6.1 — Install Homebrew

Open the **Terminal app** (Spotlight: ⌘+Space → "Terminal" → Enter). Paste this whole command, press Enter:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

What happens:
- It'll ask for your **Mac password**. Type it (you won't see characters — that's normal). Press Enter.
- It downloads, installs. Takes ~3 minutes.
- When it finishes, scroll up to find a "**==> Next steps:**" section near the bottom. It prints two commands you need to copy and paste back into the terminal. They look like:

```
echo >> /Users/<your-name>/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<your-name>/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**Copy those exact 3 commands and paste them into the terminal** (one at a time or all at once). They wire Homebrew into your shell so the next step works.

### 6.2 — Install gh CLI

Still in Terminal, run:

```
brew install gh
```

Takes ~30 seconds. No password needed.

### 6.3 — Authenticate with GitHub

Run:

```
gh auth login
```

Walk through the prompts — exact answers:

1. **What account?** → `GitHub.com`
2. **Preferred protocol for Git?** → `HTTPS`
3. **Authenticate Git with your GitHub credentials?** → `Yes`
4. **How would you like to authenticate?** → `Login with a web browser`
5. It'll show a one-time code (like `ABCD-1234`) — **copy it**
6. Press Enter — your browser opens
7. Paste the code, click **Authorize**, close the browser tab
8. Back in Terminal you should see `✓ Authentication complete` and `Logged in as <yourusername>`

**Close Terminal. Restart Claude Code** (close window, reopen) so it picks up the new `gh` tool.

---

## Step 7 · Tell Claude Code about the project (~2 min)

Open Claude Code at the project folder you cloned in Step 3. Paste this exact message as your first chat:

```
Read CLAUDE.md and WORKFLOW.md, then run `git log --oneline -20`
and `git status -b`. Tell me what you understand about the project
and what state we're in.
```

Claude Code will read the project's documentation files (which are version-controlled in the repo) and orient itself. You'll see a summary of what the project is, what's been done recently, and what state it's in.

**You're done with setup.** From here, normal work is just talking to Claude Code in plain language. Examples:

- *"Change the price on the DTS page from $8,990 to $9,200."*
- *"Add this photo to the homepage hero."* (drag the photo into the chat)
- *"What does the apply page look like right now?"*
- *"I want to start designing the DBS page."*

---

## How daily work feels (after setup)

| What you do | What Claude Code does |
|---|---|
| Open Claude Code at the project folder | Loads CLAUDE.md context automatically |
| Tell Claude what to change | Edits the right files, runs the build, shows you the diff |
| Confirm | Commits, pushes to GitHub via gh CLI |
| Wait ~60 seconds | Cloudflare auto-deploys, change is live |

**You never need to:**
- Touch the terminal directly
- Click "Push" in GitHub Desktop (Claude does it)
- Edit code by hand
- Configure deploy infrastructure

You just need to **say what you want changed in plain English** and confirm when Claude shows you the diff.

---

## When you're stuck

| Problem | What to do |
|---|---|
| "Claude says my build failed" | Paste the error to Claude — it usually fixes itself in one round. If not, ping the team admin. |
| "GitHub Desktop won't let me push" | Click **Fetch origin** at the top, then try again. Or just ask Claude to push for you (gh CLI). |
| "My changes aren't on the website" | Wait ~60 seconds (Cloudflare deploys take that long). If still missing, ask Claude to check the latest deploys. |
| "Claude Code can't find the repo" | In Claude Code, point the project at the correct cloned folder (e.g., `~/Documents/GitHub/<project-name>`). |
| "I broke something in production" | Tell Claude *"revert the last commit on main"* — fix is live in ~2 minutes. Or use Cloudflare's dashboard to roll back. |

---

## What's tied to your machine vs. what's shared

This setup runs on YOUR Mac. The setup itself doesn't sync to other machines — every team member runs through this guide once on their own laptop.

**What IS shared automatically (via the project repo):**

- All workflow rules and decisions (in `CLAUDE.md`, `WORKFLOW.md` of each project)
- Slash commands (`/ship`, `/promote`) — they live inside the repo
- Permission allowlist for routine commands

**What stays per-machine:**

- Your GitHub login (handled by GitHub Desktop)
- Your Claude Code session
- Homebrew + gh CLI installations
- Local clone of the repo

---

## Optional but useful

### Cloudflare account

If you'll be debugging deploy issues, ask the admin to add you to the YWAM Château Cloudflare account. With dashboard access you can:

- Watch builds in real time
- Read deploy logs when something fails
- Roll back a bad deploy in 30 seconds

### Claude Design

For visual work (designing new pages, choosing photo placement), the team uses **Claude Design** at https://claude.ai/design. It's a separate product from Claude Code, **not integrated**. You'd:

1. Iterate visually in Claude Design
2. Export the result
3. Hand the export to Claude Code, say *"apply this to staging"*
4. Claude Code does a "merge gate" to safely apply the changes

Each project's `WORKFLOW.md` explains when to use Claude Design vs Claude Code. Default to Claude Code unless you're making a real visual decision.

---

## The repos and what's in them

| Repo | What it contains |
|---|---|
| **`ywamchateau/ywam-chateau-site`** | The marketing website (this is the active project right now) |
| **`ywamchateau/team-onboarding`** | This setup guide (you're reading it) |

When you're added as a collaborator on a project repo, the project's own `CLAUDE.md` and `WORKFLOW.md` files will tell you everything specific to that project.

---

## Maintaining this guide

Found a step that doesn't work, or a new tool we should add? Edit this README and submit a Pull Request, or just message the team admin.

This is a **living document** — when something changes (new tool, new policy, OS update breaks something), we update this so the next person doesn't hit the same wall.
