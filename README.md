# YWAM Château · Team Onboarding

One-time setup for editing **ywamchateau.com** with Claude, on a **Mac or a Windows PC**. About 15 minutes, mostly waiting for downloads. You don't need to be a developer: every step is a click or a single paste.

*Last reviewed: 2026-10-30*

---

## The two addresses you'll use

| | |
|---|---|
| **Test site** (Claude calls it *staging*) | https://staging.ywam-chateau-site.pages.dev |
| **Live site** (Claude calls it *production* or *prod*) | https://ywamchateau.com |

Your changes always go to the **test site** first. When they look right, Vince or Haeun put them on the live site.

---

## Step 1 · Get your invites

1. If you don't have a GitHub account, create one at https://github.com/signup using your work email.
2. Send Vince (vl@ywamchateau.com) your **GitHub username**.
3. Vince sends you two invitations. **Accept both** before going on:
   - **GitHub:** to join the `ywamchateau` organization. It goes to the email on your GitHub account, which may be a personal one. You can also accept it here: https://github.com/orgs/ywamchateau/invitation
   - **Claude:** to join the YWAM Château team, sent to your work email.

---

## Step 2 · Install the tools (one time only)

Follow the section for your computer: **[Mac](#on-a-mac)** or **[Windows PC](#on-a-windows-pc)**.

### On a Mac

Open **Terminal**: press ⌘ + Space, type `Terminal`, press Enter.

Paste each command below and press Enter. Wait until the last line ends in `%` again (that means it's finished) before pasting the next one.

**1 · Install Homebrew.** It asks for your Mac password (nothing appears as you type; that's normal), then pauses at *"Press RETURN to continue"*: press Enter. Takes 5 to 15 minutes, and it can sit on one line for a while. That's normal.

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

At the end it prints "Next steps" with commands to copy. **Ignore them.** The next step does it for you.

**2 · Switch Homebrew on.**

```
B=/opt/homebrew/bin/brew; [ -x $B ] || B=/usr/local/bin/brew; [ -x $B ] && eval "$($B shellenv)" && echo "eval \"\$($B shellenv)\"" >> ~/.zprofile && brew --version && echo "✅ Homebrew is ready"
```

You should see `✅ Homebrew is ready`. If you don't, scroll up: step 1 should have ended with `Installation successful!`. If it didn't, send Vince a screenshot.

**3 · Install the tools.** GitHub's tool, Node.js, and what the photo tool needs. About two minutes.

```
brew install gh node webp jpeg-turbo && python3 -m pip install --user --quiet --disable-pip-version-check Pillow && echo "✅ Tools installed"
```

**4 · Sign in to GitHub.**

```
gh auth login -h github.com -p https -w && gh auth setup-git
```

First it asks *"Authenticate Git with your GitHub credentials?"*: press Enter. Then it shows an 8-character code. Copy it, press Enter, paste the code into the browser page that opens, and click **Authorize**. You're done when you see `✓ Logged in as` and your username.

**5 · Tell git who you are.** It asks two questions. Type your real **first and last name with a space** (e.g. `Andy Kim`), not your GitHub username, then your work email. Your first name labels every change you make.

```
read "n?Your first and last name: " && read "e?Your work email: " && git config --global user.name "$n" && git config --global user.email "$e" && echo "✅ Saved as $(git config --global user.name)"
```

**6 · Download the website.** About a minute. If your Mac asks whether Terminal may access your **Documents** folder, click **Allow**. You're done when you see `✅ The website is downloaded`.

```
mkdir -p ~/Documents/GitHub && cd ~/Documents/GitHub && { [ -d ywam-chateau-site ] || gh repo clone ywamchateau/ywam-chateau-site; } && cd ywam-chateau-site && npm install --no-audit --no-fund && echo "✅ The website is downloaded"
```

That's the last Terminal step. You can close Terminal. Go to [Step 3](#step-3--open-the-website-in-claude).

### On a Windows PC

Open **PowerShell**: press the Windows key, type `PowerShell`, press Enter. To paste, right-click inside the window.

Paste each command below and press Enter. Wait until a new line starting with `PS C:\` appears (that means it's finished) before pasting the next one.

**1 · Install the tools.** Git, GitHub's tool, Node.js and Python. Takes 5 to 10 minutes. Windows may ask *"Do you want to allow this app to make changes to your device?"* several times: click **Yes** each time.

```
foreach ($id in "Git.Git","GitHub.cli","OpenJS.NodeJS.LTS","Python.Python.3.13") { winget install -e --id $id --accept-source-agreements --accept-package-agreements }
```

**2 · Close PowerShell and open a new one.** It only finds the new tools in a fresh window.

**3 · Sign in to GitHub.**

```
gh auth login -h github.com -p https -w; gh auth setup-git
```

First it asks *"Authenticate Git with your GitHub credentials?"*: press Enter. Then it shows an 8-character code. Press Enter, type that code into the browser page that opens, and click **Authorize**. You're done when you see `✓ Logged in as` and your username.

**4 · Tell git who you are.** It asks two questions. Type your real **first and last name with a space** (e.g. `Andy Kim`), not your GitHub username, then your work email. Your first name labels every change you make.

```
$n = Read-Host "Your first and last name"; $e = Read-Host "Your work email"; git config --global user.name "$n"; git config --global user.email "$e"; "Saved as: $(git config --global user.name)"
```

**5 · Download the website.** About a minute. You're done when you see `Done: the website is downloaded`.

```
New-Item -ItemType Directory -Force "$HOME\GitHub" | Out-Null; cd "$HOME\GitHub"; if (-not (Test-Path ywam-chateau-site)) { gh repo clone ywamchateau/ywam-chateau-site }; if (Test-Path ywam-chateau-site) { cd ywam-chateau-site; npm.cmd install --no-audit --no-fund; if ($LASTEXITCODE -eq 0) { "Done: the website is downloaded" } }
```

The website goes in `C:\Users\<you>\GitHub`, not in Documents, because Windows often syncs Documents to OneDrive, which interferes with project folders.

That's the last PowerShell step. You can close PowerShell.

---

## Step 3 · Open the website in Claude

1. Install the Claude app from https://claude.ai/download (skip if you already have it).
2. Sign in with your **work email**, the one your Claude invitation went to. If the app is already signed in to a personal account, sign out from the account menu first.
3. Open the **Code** tab and choose the website folder:
   - **Mac:** Documents → GitHub → ywam-chateau-site
   - **PC:** `C:\Users\<you>\GitHub\ywam-chateau-site`

---

## Step 4 · Start every session the same way

Type this and press Enter:

```
/yc-orient
```

Claude reads the project notes, checks what has changed since last time, and asks what you'd like to work on.

---

## How you'll work

Tell Claude what you want, in plain words. For example:

- *"Change the DTS start date to September 21."*
- *"Swap the photo in the community section for this one."* (drag the photo into the chat)
- *"Fix the typo on the About page."*

Claude makes the change, checks that the site still builds, shows you what changed, and sends it to the **test site**. It's there in about a minute.

- If Claude asks *"Direct to prod, or test first?"*, or stops without sending it, say **"send it to the test site"**.
- If Claude asks permission to run a command (for example `git push`, which sends your change), click **Allow**. If it wants to delete files you didn't mention, ask it why first.
- **On a PC:** swapping photos only works on a Mac for now. Send new photos to Vince.

Then look at the test site on your **phone and your computer**. When it's right, tell Vince or Haeun, and they put it on the live site.

---

## If something goes wrong

| What you see | What to do |
|---|---|
| The download step says `Could not resolve to a Repository` | Accept the GitHub invitation at https://github.com/orgs/ywamchateau/invitation, then paste the download step again. |
| No **Code** tab in the Claude app | Check you're signed in with your work email, not a personal account. If you are, ask Vince. |
| `/yc-orient` isn't recognised | Check the Code tab is open on the `ywam-chateau-site` folder, then restart the Claude app. |
| Claude says your git name looks like a username | Open Terminal (Mac) or PowerShell (PC), paste the *Tell git who you are* step again, and type your real first and last name. |
| Claude says the build failed | Ask Claude to fix it. If it can't, send Vince a screenshot. |
| Your change isn't on the test site | Wait a minute, then refresh the page. |
| GitHub sign-in has expired | Open Terminal (Mac) or PowerShell (PC) and paste the *Sign in to GitHub* step again. |
| **PC:** `winget` isn't recognised | Install **App Installer** from the Microsoft Store, then paste the install step again. |
| **PC:** `gh`, `git` or `npm` isn't recognised | Close PowerShell and open a new one. The tools need a fresh window after installing. |

Anything else: take a screenshot and send it to Vince.

---

*This guide lives at https://github.com/ywamchateau/team-onboarding. Something here out of date? Tell Vince.*
