# YWAM Château · Team Onboarding

One-time Mac setup for editing **ywamchateau.com** with Claude. About 15 minutes, mostly waiting for downloads. You don't need to be a developer: every step is a click or a single paste.

*Last reviewed: 2026-10-30*

---

## The two addresses you'll use

| | |
|---|---|
| **Test site** (Claude calls it *staging*) | https://staging.ywam-chateau-site.pages.dev |
| **Live site** (Claude calls it *production* or *prod*) | https://ywamchateau.com |

Your changes always go to the **test site** first. When they look right, Vince or Haeun put them on the live site. If Claude suggests running `/yc-promote`, don't: that puts changes live, and it's Vince's or Haeun's job.

---

## Step 1 · Get your invites

1. If you don't have a GitHub account, create one at https://github.com/signup using your work email.
2. Send Vince (vl@ywamchateau.com) your **GitHub username**.
3. Vince sends you two invitations. **Accept both** before going on:
   - **GitHub:** to join the `ywamchateau` organization. It goes to the email on your GitHub account, which may be a personal one. You can also accept it here: https://github.com/orgs/ywamchateau/invitation
   - **Claude:** to join the YWAM Château team, sent to your work email.

---

## Step 2 · Install the tools (Terminal, one time only)

Open **Terminal**: press ⌘ + Space, type `Terminal`, press Enter.

Paste each command below and press Enter. Wait until the last line ends in `%` again (that means it's finished) before pasting the next one.

**2.1 · Install Homebrew.** It asks for your Mac password (nothing appears as you type; that's normal), then pauses at *"Press RETURN to continue"*: press Enter. Takes 5 to 15 minutes, and it can sit on one line for a while. That's normal.

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

At the end it prints "Next steps" with commands to copy. **Ignore them.** The next step does it for you.

**2.2 · Switch Homebrew on.**

```
B=/opt/homebrew/bin/brew; [ -x $B ] || B=/usr/local/bin/brew; [ -x $B ] && eval "$($B shellenv)" && echo "eval \"\$($B shellenv)\"" >> ~/.zprofile && brew --version && echo "✅ Homebrew is ready"
```

You should see `✅ Homebrew is ready`. If you don't, scroll up: step 2.1 should have ended with `Installation successful!`. If it didn't, send Vince a screenshot.

**2.3 · Install the GitHub tool, Node.js and two photo tools.** About two minutes.

```
brew install gh node webp jpeg-turbo
```

**2.4 · Sign in to GitHub.**

```
gh auth login -h github.com -p https -w && gh auth setup-git
```

First it asks *"Authenticate Git with your GitHub credentials?"*: press Enter. Then it shows an 8-character code. Copy it, press Enter, paste the code into the browser page that opens, and click **Authorize**. You're done when you see `✓ Logged in as` and your username.

**2.5 · Tell git who you are.** It asks two questions. Type your real **first and last name with a space** (e.g. `Andy Kim`), not your GitHub username, then your work email. Your first name labels every change you make.

```
read "n?Your first and last name: " && read "e?Your work email: " && git config --global user.name "$n" && git config --global user.email "$e" && echo "✅ Saved as $(git config --global user.name)"
```

**2.6 · Download the website.** About a minute. If your Mac asks whether Terminal may access your **Documents** folder, click **Allow**. You're done when you see `✅ The website is downloaded`.

```
mkdir -p ~/Documents/GitHub && cd ~/Documents/GitHub && { [ -d ywam-chateau-site ] || gh repo clone ywamchateau/ywam-chateau-site; } && cd ywam-chateau-site && npm install --no-audit --no-fund && echo "✅ The website is downloaded"
```

That's the last Terminal step. You can close Terminal.

---

## Step 3 · Open the website in Claude

1. Install the Claude app from https://claude.ai/download (skip if you already have it).
2. Sign in with your **work email**, the one your Claude invitation went to. If the app is already signed in to a personal account, sign out from the account menu first.
3. Open the **Code** tab and choose the folder **Documents → GitHub → ywam-chateau-site**.

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

Then look at the test site on your **phone and your computer**. When it's right, tell Vince or Haeun, and they put it on the live site.

---

## If something goes wrong

| What you see | What to do |
|---|---|
| Step 2.6 says `Could not resolve to a Repository` | Accept the GitHub invitation at https://github.com/orgs/ywamchateau/invitation, then paste 2.6 again. |
| No **Code** tab in the Claude app | Check you're signed in with your work email, not a personal account. If you are, ask Vince. |
| `/yc-orient` isn't recognised | Check the Code tab is open on the `ywam-chateau-site` folder, then restart the Claude app. |
| Claude says your git name looks like a username | Open Terminal, paste step 2.5 again, and type your real first and last name. |
| Claude says the build failed | Ask Claude to fix it. If it can't, send Vince a screenshot. |
| Your change isn't on the test site | Wait a minute, then refresh the page. |
| GitHub sign-in has expired | Open Terminal and paste step 2.4 again. |

Anything else: take a screenshot and send it to Vince.

---

*This guide lives at https://github.com/ywamchateau/team-onboarding. Something here out of date? Tell Vince.*
