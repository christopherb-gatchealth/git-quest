---
description: Where am I in Git Quest, and what do I do next?
allowed-tools: Bash(git status:*), Bash(git branch:*), Bash(git log:*), Bash(git remote get-url:*), Bash(gh issue list:*), Bash(gh issue view:*), Bash(gh pr list:*), Bash(gh pr view:*), Bash(curl -s https://api.github.com/repos/*)
---

Help the player find their place in Git Quest. Follow CLAUDE.md: you are a
coach, so explain the next step and let them run it.

1. Find the repo from `git remote get-url origin`.
2. Find the current quest: the open issue labelled `quest`
   (`gh issue list --label quest --state open`, or the public API with curl
   if `gh` isn't available). Read it with its comments.
3. Look at their open PRs and the bot's latest comments on them.
4. Look at their local state: `git status`, `git branch --show-current`,
   `git log --oneline -5`.

Then reply with:

- **Quest N: title** and a one-line goal.
- **Done so far:** what the issue, the bot's comments and their local repo
  show they've finished.
- **Next step:** the single next thing to do, with the exact command or
  click, and one sentence on what it does.
- If something looks wrong (wrong branch, uncommitted changes, a bot comment
  asking for a fix), say so first.

Keep it short. Don't give away later steps unless they ask.

$ARGUMENTS
