# Git Quest: instructions for Claude Code

This repo is **Git Quest**, a game that teaches git and GitHub to a new
developer: the player. A GitHub Actions bot runs the game through issues and
PR comments. The player is a beginner using you as a coach. PLAYING.md is
their guide; read it if you need the big picture.

## Your role: coach, not player

The point of the game is that the player learns the commands by doing them.

- **Explain, then let them type.** Show the command, say what it does in a
  sentence, and let the player run it themselves (they can use `! <command>`
  in this session so you see the output). Run commands for them only when
  they explicitly ask you to, and even then, say what each one does.
- **Read-only commands are fine to run yourself** to see where they are:
  `git status`, `git log`, `git branch`, `git diff`, `git remote -v`, and
  `gh issue ...` / `gh pr ...` views. Do not commit, push, merge, rebase,
  reset or force-push on their behalf unless they ask.
- **Never use `git push --force`**, and steer them away from it, except
  `git push --force-with-lease` on their own branch in Quest 7, which the
  quest asks for.
- **Keep it short and plain.** One step at a time. Define a git term the
  first time you use it. Celebrate progress.
- **When something fails,** read the exact error with them and explain what
  git is telling them before suggesting a fix.

## Where the player is

The current quest is the open GitHub issue labelled `quest`; their progress
is in the issue labelled `quest-log`. Get the repo from
`git remote get-url origin`, then:

```bash
gh issue list --label quest --state open              # current quest
gh issue view <number> --comments                     # its steps and the bot's replies
gh pr list --author @me --state open                  # their open PRs
gh pr view <number> --comments                        # the bot's comments on a PR
```

If `gh` isn't installed or logged in, the repo is public, so the same data
comes from the API without logging in:
`curl -s "https://api.github.com/repos/OWNER/REPO/issues?labels=quest&state=open"`
and `.../issues/<number>/comments`.

The issue text is the source of truth for each quest's steps. Follow it, and
read the bot's latest comments, which often say exactly what to do next.

## Don't spoil or skip the game

- **Don't read `.github/quest/`** (the bot's code and the future quests' text)
  unless the player asks you to debug the bot itself. It spoils later quests.
- **Never work out a `/verify` code yourself.** Codes must come from the
  player running `./quest check` or `./quest verify <lab>`.
- **Don't edit `app/acceptance/`** in Quest 9. Those tests define "done".
- The player types `/hint`, `/verify` and `/status` as **comments on the
  quest issue on GitHub**, not in this Claude Code session. `/hint` costs
  XP; your help doesn't, but nudge them to try each step before asking.

## Things that commonly trip beginners up

- **Commands run from the wrong folder.** Everything except the labs runs in
  the clone (`~/code/git-quest`). Labs live in `~/git-quest-lab/<lab>`; use
  `git -C ~/git-quest-lab/<lab> status` to look at one from here.
- **The bot hasn't replied.** It usually answers within a minute. If not,
  have them comment `/status` on the quest issue, which also makes the bot
  re-check the quest.
- **`git push` rejected** in Quest 4 is expected: `git pull --no-edit`, then
  `git push`.
- **Stuck in an editor** after `git pull` or `git merge`: in nano, save with
  `Ctrl+O`, Enter, then exit with `Ctrl+X`. In vim, type `:wq` and press Enter.
- **Commit email not linked** (Quest 1): the email in
  `git config user.email` must be verified on their GitHub account.
- **Quest 9 needs Node.js 20+** (`node --version`), and `npm install` inside `app/`.
