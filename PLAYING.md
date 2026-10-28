# Playing Git Quest

Welcome! This guide walks you through Git Quest from the very first step,
and shows how to use **Claude Code** as your coach along the way.

- [How the game works](#how-the-game-works)
- [Before you start](#before-you-start)
- [Using Claude Code as your coach](#using-claude-code-as-your-coach)
- [The quests, one by one](#the-quests-one-by-one)
- [When something goes wrong](#when-something-goes-wrong)
- [Cheat sheet](#cheat-sheet)

## How the game works

- Each quest is a **GitHub issue** in this repo, labelled `quest`. Only one
  is open at a time: that's your current quest. Its text has the goal, the
  steps and what "done" means.
- A **bot** watches what you do (pushes, pull requests, comments) and replies
  on the issue or your PR. When a quest is done, it closes that issue and
  opens the next one. Turn on notifications for the repo (**Watch → All
  Activity**) so you see its replies in your email.
- The **Quest Log** issue (labelled `quest-log`) shows your XP, rank and
  achievements.
- You talk to the bot by commenting on your **current quest issue** on GitHub:

  | Comment | What it does |
  | --- | --- |
  | `/status` | Says where you are. Also makes the bot re-check your quest if it seems to have missed something. |
  | `/hint` | Gives the next hint. Each one costs 10% of the quest's XP. |
  | `/verify <code>` | Hands in a code from `./quest` (Quests 0 and 8). |

- `main` is protected, like at work: every change goes through a branch and
  a pull request.
- Mistakes are part of the game. Some cost a little XP, none are fatal, and
  nothing you do here can break anything real.

## Before you start

You need:

- A **Mac** with **Terminal** (press `Cmd+Space`, type "Terminal").
- A **GitHub account**, with the invite to this repo accepted (check your
  email, or https://github.com/notifications).
- **VS Code** or another editor (optional; `nano` in the Terminal works too).
- **Node.js 20 or newer**, for the last quest only: https://nodejs.org.
- **Claude Code** (below).

Quest 0 walks you through git, your SSH key and cloning the repo, so you
don't need to set those up first.

### Install Claude Code

Follow https://docs.claude.com/en/docs/claude-code/setup, or in Terminal:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Then run `claude` once and sign in.

### Optional: the GitHub CLI

With the GitHub CLI (`gh`), Claude Code can read your quest issue and the
bot's comments for you. Without it, Claude Code still works; it reads them
from GitHub's public API instead. To install it with Homebrew:

```bash
brew install gh
gh auth login      # choose GitHub.com, SSH, and log in with your browser
```

## Using Claude Code as your coach

Once you've cloned the repo in Quest 0, open Claude Code **inside it**:

```bash
cd ~/code/git-quest
claude
```

Starting it there matters: the repo's `CLAUDE.md` tells Claude Code it's
your git coach for this game. It will explain each step and let **you** type
the commands, because typing them yourself is how they stick. It won't hand
you `/verify` codes or spoil later quests.

### `/quest`: where am I?

Type `/quest` in Claude Code at any time. It looks at your open quest issue,
the bot's latest comments, your pull requests and your local repo, and tells
you:

- which quest you're on, and what's done so far
- the **one next step**, with the exact command
- anything that looks off, like being on the wrong branch

You can add a question after it, like `/quest why did my push get rejected?`

### Running commands so Claude Code can see them

Type `!` before a command to run it inside Claude Code's session, so Claude
Code sees the output and can explain it:

```text
! git status
! git push
```

Or run commands in a separate Terminal window and paste anything confusing
into Claude Code.

### Good things to ask

- "What does `git add` actually do?"
- "Explain this error" (then paste it)
- "What did the bot just say on my PR?"
- "I'm in a weird state, what does `git status` mean here?"
- "Draw what my branches look like right now"

Claude Code will ask your permission before running commands. That's normal:
read what it wants to run, then approve it.

### Before you clone (Quest 0)

`CLAUDE.md` only loads once the repo is on your laptop. For Quest 0, open
Claude Code anywhere (`claude` in Terminal), paste the Quest 0 issue text in,
and ask it to walk you through it one step at a time.

## The quests, one by one

Your current quest's issue always has the full steps. Here's what to expect
from each one.

### Quest 0: Set up your tools (50 XP)

**You'll learn:** installing git, telling git who you are, SSH keys, cloning.

1. Accept the repo invite.
2. Set your name and email in git. Use an email that's **verified on your
   GitHub account** (GitHub → Settings → Emails). If it isn't, the bot can't
   tell your commits are yours in Quest 1.
3. Make an SSH key and add the **public** one (`.pub`) to GitHub.
4. Clone the repo into `~/code`.
5. Run `./quest check`. It checks everything and prints a code.
6. Comment `/verify <code>` on the Quest 0 issue.

**Ask Claude Code:** "What is an SSH key and why does GitHub want one?"

### Quest 1: Your first commit (100 XP)

**You'll learn:** branches, `git add`, `git commit`, `git push`.

Make a branch named like `feat/hello-<your-username>`, add a line to
`hello.md`, commit it and push the branch. The bot checks:

- the branch name starts with `feat/`, `fix/` or `chore/`, in lowercase
- your commit changes `hello.md`
- the commit's email is linked to your GitHub account

**Ask Claude Code:** "What's the difference between staging and committing?"

### Quest 2: Open a pull request (150 XP)

**You'll learn:** pull requests, good titles, filling in a description.

Open a PR from your branch into `main` on GitHub. The title needs 3+ words,
should start with a capital letter, and must say what changed (not "Update
hello.md"). Fill in all three sections of the description: **What**, **Why**
and **How I tested**. **Don't merge yet.** If the bot asks for changes, edit
the PR's title or description and it checks again.

**Ask Claude Code:** "Help me write a clear PR title for this change."

### Quest 3: Survive code review (150 XP)

**You'll learn:** updating a PR, replying to review comments, merging.

A reviewer asks you to add a `Fun fact:` line. Add it on the **same branch**
and push (the PR updates itself). Then reply to the review comment in the
PR's **Files changed** tab. Wait for the approval, then **Squash and merge**.
Merging before approval costs XP.

**Ask Claude Code:** "What does squash merging do to my commits?"

### Quest 4: Stay in sync (150 XP)

**You'll learn:** pulling before you branch, and what to do when a push is
rejected.

Start from a fresh `main`, add `about/<your-username>.md`, and push. A
teammate then pushes to your branch, so your next push is **rejected**.
That's the lesson: `git pull --no-edit`, then `git push`. **Never** use
`--force` to get past it (that costs XP and deletes their work). Then open a
PR and merge it.

**Ask Claude Code:** "Why was my push rejected, and what does `git pull` do here?"

### Quest 5: Resolve a merge conflict (250 XP)

**You'll learn:** what a conflict is, conflict markers, `git merge`.

Change the `favorite_editor:` line in `config/settings.md` and open a PR. A
teammate changes the same line, so your PR now has a conflict. Merge `main`
into your branch on your laptop, pick the final line, delete the
`<<<<<<<` / `=======` / `>>>>>>>` markers, commit and push. When the bot
confirms it's clean, merge. If you panic mid-merge, `git merge --abort`
undoes it.

**Ask Claude Code:** "Explain the conflict markers in this file."

### Quest 6: Undo a bad commit (200 XP)

**You'll learn:** `git revert`, and why it's safer than rewriting history.

A teammate merged a broken change. Find its commit with `git log --oneline`,
undo it on a new branch with `git revert`, and merge that through a PR.
Undoing it by hand instead costs XP.

**Ask Claude Code:** "What's the difference between `git revert` and `git reset`?"

### Quest 7: Secret leak drill (200 XP)

**You'll learn:** secret scanning, `.gitignore`, cleaning a branch's history.

You commit a **fake** API key on purpose and watch the secret scan go red.
Then you remove that commit from your branch (`git reset --soft`), add
`.env` to `.gitignore`, and `git push --force-with-lease`. That's the one
time in the game a force push is right: it's your own branch. Then merge.

**Ask Claude Code:** "Why isn't deleting the file in a new commit enough?"

### Quest 8: Local labs (200 XP)

**You'll learn:** `git restore`, `git restore --staged`, `git stash`, `git log -S`.

Four short puzzles on your laptop, in any order:

```bash
./quest lab restore          # sets up the lab in ~/git-quest-lab/restore
cd ~/git-quest-lab/restore   # fix it there with git
cd -                         # back to the quest repo
./quest verify restore       # checks it and prints a code
```

Comment each code as `/verify <code>` on the quest issue. For the detective
lab, answer with `./quest verify detective <name>`. You can restart any lab
by running `./quest lab <name>` again.

**Ask Claude Code:** "Look at my restore lab with `git -C ~/git-quest-lab/restore status` and explain what I'm seeing."

### Quest 9: Boss level (500 XP)

**You'll learn:** the real workflow: a React component, tests, CI and review.

Build `app/components/StatusBadge.tsx`, use it in `app/app/page.tsx`, and
write `app/components/StatusBadge.test.tsx`. The acceptance tests in
`app/acceptance/` define "done" (don't edit them). Check it on your laptop
first:

```bash
cd app
npm install
npm test          # all green
npm run build     # catches type errors
npm run dev       # look at it at http://localhost:3000
```

Push, open a PR, wait for **App CI** to go green and for the bot to approve,
then merge. Merging without green CI or without your own test costs XP.

**Ask Claude Code:** "Explain how `ScoreBar.tsx` and its test fit together", or
"Why is this test failing?" Write the component yourself; ask Claude Code to
review it once it's done.

## When something goes wrong

| Problem | What to do |
| --- | --- |
| The bot hasn't replied after a couple of minutes | Comment `/status` on the quest issue. It also makes the bot re-check your quest. |
| `Permission denied (publickey)` | Your SSH key isn't on GitHub. `cat ~/.ssh/id_ed25519.pub`, and check that line is under GitHub → Settings → SSH and GPG keys. |
| `./quest: permission denied` | `chmod +x quest` |
| `! [rejected] ... (fetch first)` | Someone pushed to your branch: `git pull --no-edit`, then `git push`. |
| A screen of text opened after `git pull` or `git merge` | That's the editor asking for a message. In nano: `Ctrl+O`, Enter, `Ctrl+X`. In vim: type `:wq`, then Enter. |
| "Your branch is behind" / it's started from an old `main` | `git switch main && git pull`, then `git switch -` and `git merge --no-edit main`. |
| Lost and not sure what state you're in | `git status`, then `/quest` in Claude Code. |
| Still stuck | `/hint` on the quest issue, or ask your mentor. |

## Cheat sheet

```bash
git status                     # where am I, what's changed?
git switch main && git pull    # get the latest main
git switch -c feat/my-thing    # new branch
git add <file>                 # stage a change
git commit -m "Say what changed"
git push -u origin feat/my-thing   # first push of a branch
git push                       # later pushes
git pull --no-edit             # bring in others' commits
git log --oneline -10          # recent history
git diff                       # unstaged changes
git restore <file>             # throw away changes to a file
git restore --staged <file>    # unstage a file
git stash / git stash pop      # park and bring back work
git revert <commit>            # undo a commit with a new commit
```
