# Git & GitHub --- A Beginner's Friendly Guide

> **For someone opening Git for the first time.**
>
> You do NOT need to memorize everything in this file. Start with the
> simple commands, use the examples, and come back here when you get
> stuck.

------------------------------------------------------------------------

# 1. First: What Are Git and GitHub?

This is the easiest way to think about them:

### Git

Git is a tool on your computer that keeps track of changes to your
project.

Imagine you're building a project and you reach a good point:

``` text
Heimdall works!
```

You can tell Git:

> "Save this version."

That saved version is called a **commit**.

Later, you can make more changes and, if something goes wrong, look back
at an older version.

### GitHub

GitHub is a website where you can store your Git repository online.

Think:

``` text
Git
↓
Your computer

GitHub
↓
Your online backup + collaboration place
```

------------------------------------------------------------------------

# 2. The Basic Git Flow

You will use this pattern ALL THE TIME:

``` text
You edit files
      ↓
git add
      ↓
git commit
      ↓
git push
      ↓
GitHub
```

And when you want changes from GitHub:

``` text
GitHub
   ↓
git pull
   ↓
Your computer
```

That's the basic idea.

------------------------------------------------------------------------

# 3. Check If Git Is Installed

Open CMD or PowerShell.

Run:

``` bash
git --version
```

You should get something like:

``` text
git version 2.47.1.windows.1
```

If you get:

``` text
'git' is not recognized...
```

Git is either not installed or is not available in your PATH.

------------------------------------------------------------------------

# 4. Tell Git Who You Are

Git puts your name on your commits.

Run this once:

``` bash
git config --global user.name "Your Name"
```

Example:

``` bash
git config --global user.name "Vaishnav"
```

Set your email:

``` bash
git config --global user.email "you@example.com"
```

Check it:

``` bash
git config --global --list
```

You don't normally need to do this again.

------------------------------------------------------------------------

# 5. Create a New Git Repository

Suppose you have:

``` text
MyProject/
```

Open the terminal inside that folder.

Run:

``` bash
git init
```

Git will create a hidden `.git` folder.

Your project is now a Git repository.

### Common beginner mistake

You may run:

``` bash
git status
```

and get:

``` text
fatal: not a git repository
```

This usually means you're in the wrong folder.

Check where you are:

Windows PowerShell:

``` powershell
pwd
```

Windows CMD:

``` cmd
cd
```

Then move into your project:

``` bash
cd D:\Projects\MyProject
```

Try again:

``` bash
git status
```

------------------------------------------------------------------------

# 6. Download an Existing Project

If someone gives you a GitHub repository URL, you can download it with:

``` bash
git clone https://github.com/user/project.git
```

Example:

``` bash
git clone https://github.com/itzychuu/Heimdall.git
```

Git creates a folder containing the project.

Then:

``` bash
cd Heimdall
```

------------------------------------------------------------------------

# 7. Check What Git Thinks Is Happening

This is probably the command you'll use most:

``` bash
git status
```

Example:

``` text
On branch main

Changes not staged for commit:
  modified: README.md
```

This means:

> "Hey, README.md changed, but you haven't told me to include it in the
> next commit yet."

Use `git status` whenever you're confused.

------------------------------------------------------------------------

# 8. Your First `git add`

Suppose you changed:

``` text
README.md
```

Tell Git you want to include it:

``` bash
git add README.md
```

You can add several:

``` bash
git add README.md package.json
```

Or an entire folder:

``` bash
git add src/
```

Or everything:

``` bash
git add .
```

### What does "staging" mean?

Think of staging like putting things into a box before sending it.

``` text
Your files
   ↓
git add
   ↓
"Box" = staging area
```

You are saying:

> "These are the changes I want in my next save point."

------------------------------------------------------------------------

# 9. Your First Commit

After staging:

``` bash
git commit -m "Add login page"
```

The `-m` means:

> "I'm giving Git a message explaining this commit."

Example:

``` bash
git commit -m "feat: add login page"
```

Now Git has saved a checkpoint.

------------------------------------------------------------------------

# 10. What Is a Commit?

A commit is basically a **saved checkpoint**.

Imagine:

``` text
Monday
Commit 1
↓
Project starts working

Tuesday
Commit 2
↓
Added login

Wednesday
Commit 3
↓
Added dashboard

Thursday
Commit 4
↓
Oops! Everything broke 😭
```

You can inspect the previous commits and potentially return to a working
state.

------------------------------------------------------------------------

# 11. See Your Previous Commits

Run:

``` bash
git log
```

This can show a lot of information.

For a simpler version:

``` bash
git log --oneline
```

Example:

``` text
5009962 Add project structure
a81f321 Add README
23bd921 Initial commit
```

The strange-looking text is the commit ID.

------------------------------------------------------------------------

# 12. See What You Changed

Run:

``` bash
git diff
```

Imagine you changed:

``` text
Hello Heimdall
```

to:

``` text
Hello Heimdall!
```

`git diff` shows you what changed.

This is very useful before committing.

------------------------------------------------------------------------

# 13. See What You Already Added

If you ran:

``` bash
git add .
```

use:

``` bash
git diff --staged
```

This lets you inspect what is about to be committed.

A good habit is:

``` bash
git status
git diff
git add .
git diff --staged
git commit -m "..."
```

------------------------------------------------------------------------

# 14. Push Your Project to GitHub

Suppose your GitHub repository is:

``` text
https://github.com/yourname/MyProject.git
```

Connect your local project:

``` bash
git remote add origin https://github.com/yourname/MyProject.git
```

Check:

``` bash
git remote -v
```

Then push:

``` bash
git push -u origin main
```

After that, future pushes are usually simply:

``` bash
git push
```

------------------------------------------------------------------------

# 15. What Is `origin`?

This looks scary:

``` bash
git remote add origin https://github.com/yourname/project.git
```

But it's simple.

`origin` is just a nickname.

Instead of constantly typing:

``` text
https://github.com/yourname/project.git
```

Git lets you say:

``` text
origin
```

So:

``` bash
git push origin main
```

means:

> "Push my main branch to the repository I call origin."

------------------------------------------------------------------------

# 16. Pull Changes From GitHub

Suppose your friend changed the project on GitHub.

You want those changes:

``` bash
git pull
```

Or explicitly:

``` bash
git pull origin main
```

Think:

``` text
GitHub
   ↓
git pull
   ↓
Your computer
```

------------------------------------------------------------------------

# 17. `git fetch` vs `git pull`

This confuses many beginners.

### `git fetch`

Downloads information from GitHub but doesn't immediately combine it
with your current files.

``` bash
git fetch
```

Think:

> "Show me what's happening over there."

### `git pull`

Gets the changes and integrates them into your current branch.

``` bash
git pull
```

Think:

> "Bring those changes into my project."

When you're learning, remember:

``` text
fetch = look
pull  = bring
```

------------------------------------------------------------------------

# 18. Branches --- What Are They?

This is one of the most useful Git ideas.

Imagine your project has:

``` text
main
```

Main is your stable version.

Now you want to build a scanner.

Instead of directly changing main:

``` text
main
 ↓
change everything
 ↓
😭
```

Create a separate branch:

``` text
main
  \
   feature/scanner
```

You can work safely there.

------------------------------------------------------------------------

# 19. Create a Branch

Modern Git:

``` bash
git switch -c feature/scanner
```

This creates the branch AND moves you onto it.

Check:

``` bash
git branch
```

You might see:

``` text
* feature/scanner
  main
```

The `*` means:

> "You are currently here."

------------------------------------------------------------------------

# 20. Switch Back to Main

``` bash
git switch main
```

Switch back:

``` bash
git switch feature/scanner
```

------------------------------------------------------------------------

# 21. Why Use Branches?

Suppose Heimdall is working.

``` text
main
```

You want to add:

``` text
Nmap integration
```

Create:

``` bash
git switch -c feature/nmap
```

Now:

``` text
main
     \
      feature/nmap
```

You can experiment without disturbing the stable branch.

------------------------------------------------------------------------

# 22. Merge a Branch

When the feature works:

``` bash
git switch main
```

Then:

``` bash
git merge feature/nmap
```

Now the Nmap changes are part of main.

------------------------------------------------------------------------

# 23. Delete a Finished Branch

After merging:

``` bash
git branch -d feature/nmap
```

This deletes the **local branch**, not the commits that were merged into
main.

------------------------------------------------------------------------

# 24. The Old `checkout` Command

You may see tutorials using:

``` bash
git checkout main
```

or:

``` bash
git checkout -b feature/nmap
```

These still work.

For new Git workflows, I recommend learning:

``` bash
git switch
```

instead.

------------------------------------------------------------------------

# 25. Rename a Branch

If your branch is called:

``` text
master
```

and you want:

``` text
main
```

run:

``` bash
git branch -M main
```

That's what we did with Heimdall.

------------------------------------------------------------------------

# 26. What If I Accidentally Changed a File?

Suppose you changed:

``` text
README.md
```

and you don't want your changes anymore.

You can restore it:

``` bash
git restore README.md
```

### ⚠️ Careful

This can throw away your uncommitted changes.

If you aren't sure, don't run it yet.

Ask:

> "Can I safely discard this?"

------------------------------------------------------------------------

# 27. What If I Accidentally Ran `git add`?

No problem.

Suppose:

``` bash
git add README.md
```

but you didn't want to stage it.

Run:

``` bash
git restore --staged README.md
```

Your changes are still there.

You just removed them from the staging area.

------------------------------------------------------------------------

# 28. What If I Made a Bad Commit?

If the commit has already been shared with other people, a safer option
is:

``` bash
git revert <commit-id>
```

This creates a new commit that reverses the old one.

Example:

``` bash
git revert 5009962
```

For beginners:

``` text
revert = make a new commit that undoes an old commit
```

------------------------------------------------------------------------

# 29. What Is `reset`?

`reset` is more powerful and more dangerous.

For example:

``` bash
git reset HEAD~1
```

can remove the latest commit while keeping the changes in your files.

There is also:

``` bash
git reset --hard HEAD~1
```

### ⚠️ Be careful!

`--hard` can throw away work.

As a beginner, don't use `git reset --hard` unless you know exactly what
you are trying to recover or remove.

------------------------------------------------------------------------

# 30. Stash --- "I Need to Put This Away for a Minute"

Imagine you're working on:

``` text
feature/scanner
```

but suddenly you need to switch branches.

Your work isn't finished.

You can temporarily put it aside:

``` bash
git stash
```

Now switch:

``` bash
git switch main
```

Later:

``` bash
git switch feature/scanner
git stash pop
```

Your unfinished changes come back.

Think:

``` text
stash = temporary drawer for unfinished work
```

------------------------------------------------------------------------

# 31. `.gitignore` --- Very Important

You don't want Git to upload everything.

For example, a Node.js project has:

``` text
node_modules/
```

It can contain thousands of files.

You normally don't commit it.

Create:

``` text
.gitignore
```

Example:

``` gitignore
node_modules/
dist/
.env
*.log
__pycache__/
.venv/
src-tauri/target/
```

Now Git ignores those files.

### Why?

Because files such as:

``` text
.env
```

might contain:

``` text
API_KEY=super-secret-key
```

You definitely don't want that on GitHub.

------------------------------------------------------------------------

# 32. What If Git Is Ignoring Something?

You can ask Git:

``` bash
git check-ignore -v filename
```

This tells you which `.gitignore` rule is responsible.

------------------------------------------------------------------------

# 33. Remote Repository Information

See your GitHub connection:

``` bash
git remote -v
```

You might see:

``` text
origin  https://github.com/you/Heimdall.git (fetch)
origin  https://github.com/you/Heimdall.git (push)
```

------------------------------------------------------------------------

# 34. Changing the GitHub Repository

If you accidentally connected to the wrong repository:

``` bash
git remote set-url origin https://github.com/you/correct-repo.git
```

Check:

``` bash
git remote -v
```

------------------------------------------------------------------------

# 35. Removing a Remote

If you want to disconnect the repository:

``` bash
git remote remove origin
```

This does NOT delete the GitHub repository.

It only removes the connection from your local project.

------------------------------------------------------------------------

# 36. Remote Branches

See branches that exist on GitHub:

``` bash
git branch -r
```

See everything:

``` bash
git branch -a
```

------------------------------------------------------------------------

# 37. A Very Common GitHub Error

You may try:

``` bash
git push -u origin main
```

and get:

``` text
rejected
fetch first
```

This usually means:

> "GitHub already has changes that your computer doesn't have."

Don't immediately run:

``` bash
git push --force
```

First inspect what happened:

``` bash
git fetch origin
git log --oneline --graph --decorate --all
```

Then decide how to combine the histories.

### What happened to us with Heimdall?

We accidentally pointed our local code repository at the existing
Heimdall documentation repository.

The histories were different.

That's why Git rejected the push.

The lesson:

> **Always check your remote with `git remote -v` before pushing.**

------------------------------------------------------------------------

# 38. What Is a Pull Request?

A Pull Request (PR) is mainly a GitHub feature.

Imagine:

``` text
main
  \
   feature/nmap
```

You finish the Nmap feature.

You push:

``` bash
git push -u origin feature/nmap
```

Then GitHub lets you create a Pull Request:

> "Hey, I made this feature. Can we review and add it to main?"

Someone can review the code.

Then the branch can be merged.

------------------------------------------------------------------------

# 39. A Simple Team Workflow

``` text
main
 ↓
create branch
 ↓
write code
 ↓
git add
 ↓
git commit
 ↓
git push
 ↓
Pull Request
 ↓
Review
 ↓
Merge
 ↓
main
```

This is a workflow you'll see everywhere in software development.

------------------------------------------------------------------------

# 40. Tags --- Mark Important Versions

Suppose Heimdall reaches version 1.0.

You can create a tag:

``` bash
git tag v1.0.0
```

Push it:

``` bash
git push origin v1.0.0
```

Now you have a named point in Git history:

``` text
v1.0.0
```

Tags are commonly used for releases.

------------------------------------------------------------------------

# 41. Looking at a Specific Commit

``` bash
git show <commit-id>
```

Example:

``` bash
git show 5009962
```

This shows what happened in that commit.

------------------------------------------------------------------------

# 42. `git reflog` --- The Emergency Tool

This one is extremely useful when you make a serious mistake.

``` bash
git reflog
```

It shows where Git's `HEAD` has been.

For example, if you accidentally reset something, the reflog may help
you find the previous commit.

Think:

``` text
reflog = Git's memory of where you were
```

------------------------------------------------------------------------

# 43. `git clean` --- Be Careful

This removes untracked files.

First preview:

``` bash
git clean -n
```

If you're absolutely sure:

``` bash
git clean -f
```

For directories too:

``` bash
git clean -fd
```

### ⚠️ Warning

This can delete files that Git isn't tracking.

Always run:

``` bash
git clean -n
```

first.

------------------------------------------------------------------------

# 44. Git Aliases

You can create shortcuts.

For example:

``` bash
git config --global alias.st status
```

Now:

``` bash
git st
```

does the same as:

``` bash
git status
```

You can create a nice log shortcut:

``` bash
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Then:

``` bash
git lg
```

------------------------------------------------------------------------

# 45. Git Help

If you forget how something works:

``` bash
git help commit
```

Or:

``` bash
git commit -h
```

Git has built-in help.

------------------------------------------------------------------------

# 46. Common Problems and What They Mean

## Problem 1: "not a git repository"

``` text
fatal: not a git repository
```

You're probably in the wrong folder.

Try:

``` bash
cd path/to/project
git status
```

Or initialize the folder:

``` bash
git init
```

Only do that if it is actually supposed to become a new Git repository.

------------------------------------------------------------------------

## Problem 2: "nothing to commit"

``` text
nothing to commit, working tree clean
```

Good!

It means Git doesn't see any new changes.

------------------------------------------------------------------------

## Problem 3: "changes not staged"

You changed something but haven't staged it.

Do:

``` bash
git add .
git commit -m "describe the change"
```

------------------------------------------------------------------------

## Problem 4: "untracked files"

Git found a new file it isn't tracking.

Example:

``` text
Untracked files:
    test.py
```

If you want it:

``` bash
git add test.py
```

If you don't want it in Git, add it to `.gitignore`.

------------------------------------------------------------------------

## Problem 5: Push rejected

Example:

``` text
rejected
fetch first
```

Don't force-push immediately.

Check:

``` bash
git fetch
git log --oneline --graph --decorate --all
```

------------------------------------------------------------------------

## Problem 6: Wrong GitHub repository

Check:

``` bash
git remote -v
```

If it's wrong:

``` bash
git remote set-url origin <correct-url>
```

------------------------------------------------------------------------

## Problem 7: Accidentally staged the wrong file

Use:

``` bash
git restore --staged filename
```

------------------------------------------------------------------------

## Problem 8: Accidentally committed something sensitive

If you committed an API key or password, **don't assume deleting the
file in a later commit makes the secret safe**.

Immediately rotate/revoke the exposed credential.

Then deal with removing the secret from Git history using an appropriate
history-rewriting method.

------------------------------------------------------------------------

# 47. What Should I Type Most of the Time?

If you're working alone on Heimdall, you'll probably use these
constantly:

``` bash
git status
git add .
git commit -m "message"
git push
git pull
git switch
git log --oneline
git diff
```

That's enough to start.

You don't need to memorize:

``` text
rebase
cherry-pick
bisect
reflog
```

on day one.

Learn them when you actually need them.

------------------------------------------------------------------------

# 48. Your First Real Development Example

Let's imagine tomorrow we build a login screen.

### Step 1

Start from main:

``` bash
git switch main
```

### Step 2

Get the latest version:

``` bash
git pull
```

### Step 3

Create a branch:

``` bash
git switch -c feature/login
```

### Step 4

Write your code.

### Step 5

Check:

``` bash
git status
```

### Step 6

See exactly what changed:

``` bash
git diff
```

### Step 7

Stage:

``` bash
git add .
```

### Step 8

Check what you're about to commit:

``` bash
git diff --staged
```

### Step 9

Commit:

``` bash
git commit -m "feat: add login screen"
```

### Step 10

Push:

``` bash
git push -u origin feature/login
```

### Step 11

Open a Pull Request on GitHub.

### Step 12

After merging:

``` bash
git switch main
git pull
```

Congratulations.

You just used a real professional Git workflow.

------------------------------------------------------------------------

# 49. Heimdall Example

For our actual Heimdall project, suppose we're adding Semgrep.

We could do:

``` bash
git switch main
git pull

git switch -c feature/semgrep-adapter
```

Work on:

``` text
engine/tools/
engine/adapters/
engine/parsers/
tests/fixtures/semgrep/
```

Then:

``` bash
git status
git diff

git add .

git diff --staged

git commit -m "feat: add Semgrep tool adapter"

git push -u origin feature/semgrep-adapter
```

Create the Pull Request.

After merging:

``` bash
git switch main
git pull
```

That's exactly the kind of workflow we'll use throughout Heimdall.

------------------------------------------------------------------------

# 50. The 10 Commands I Want You to Learn First

Don't worry about all the other commands yet.

Memorize these:

### 1. Check status

``` bash
git status
```

### 2. Add changes

``` bash
git add .
```

### 3. Commit

``` bash
git commit -m "message"
```

### 4. Upload

``` bash
git push
```

### 5. Download updates

``` bash
git pull
```

### 6. See history

``` bash
git log --oneline
```

### 7. See changes

``` bash
git diff
```

### 8. Create a branch

``` bash
git switch -c feature/name
```

### 9. Switch branches

``` bash
git switch main
```

### 10. See GitHub connection

``` bash
git remote -v
```

If you understand these ten, you're already capable of working on a real
Git project.

------------------------------------------------------------------------

# 51. A Tiny Cheat Sheet

When you are confused:

``` bash
git status
```

When you finished coding:

``` bash
git add .
git commit -m "what I changed"
git push
```

Before starting work:

``` bash
git pull
```

Want to make a feature?

``` bash
git switch -c feature/name
```

Want to see what changed?

``` bash
git diff
```

Want to see old commits?

``` bash
git log --oneline
```

Want to know where GitHub is?

``` bash
git remote -v
```

------------------------------------------------------------------------

# 52. One Last Thing

You do **not** need to be afraid of Git.

At first it looks like:

``` text
add
commit
push
pull
fetch
merge
rebase
stash
reset
revert
HEAD
origin
branch
remote
...
```

It feels like a completely different language.

But start with this:

``` text
EDIT
  ↓
git status
  ↓
git add .
  ↓
git commit -m "..."
  ↓
git push
```

That's your core loop.

Then gradually learn the other commands when a real problem gives you a
reason to use them.

------------------------------------------------------------------------

# Quick Reference Table

  Command         Simple meaning
  --------------- -----------------------------------
  `git init`      Start Git in this folder
  `git clone`     Download a Git project
  `git status`    What is happening?
  `git add`       Prepare changes
  `git commit`    Save a checkpoint
  `git log`       See old checkpoints
  `git diff`      See what changed
  `git push`      Send changes to GitHub
  `git pull`      Get changes from GitHub
  `git fetch`     Check/download remote updates
  `git branch`    See/manage branches
  `git switch`    Move to another branch
  `git merge`     Combine branches
  `git restore`   Undo local file changes
  `git revert`    Safely undo a shared commit
  `git reset`     Move/reset Git history or staging
  `git stash`     Temporarily hide unfinished work
  `git remote`    Manage GitHub connection
  `git tag`       Mark a version
  `git reflog`    Find where Git was previously
  `git clean`     Delete untracked files
  `git help`      Ask Git for help

------------------------------------------------------------------------

## You got this ❤️

Nobody learns Git by memorizing 50 commands.

You learn it by **using it, breaking something, seeing the error,
understanding what happened, and trying again**.

That's exactly how we're going to learn it while building Heimdall.
