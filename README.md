# Git Made Simple

Everyday Git commands that actually work.

---

## Table of Contents

- [Starting with a Project](#starting-with-a-project)
- [Working with Code](#working-with-code)
- [Working with Branches](#working-with-branches)
- [Fixing Your Mistakes](#fixing-your-mistakes)
- [Working with Others](#working-with-others)
- [Some Advanced Stuff](#some-advanced-stuff)
- [Oh No! Emergency Help](#oh-no-emergency-help)

---

## Starting with a Project

### I want to download a project and start working on it

Get the project link and run:

```bash
git clone <project-link>
cd <project-folder>
```

### I need to switch to a different branch

```bash
git switch <branch-name>
```

### I want to get the latest code from the team

```bash
git pull
```

---

## Working with Code

### I made some changes. How do I check what I changed?

```bash
git status
```

### I want to save my changes

```bash
git add .
git commit -m "describe what you changed"
```

### I want to send my changes to the remote repository

```bash
git push
```

### I only want to save some files, not all of them

```bash
git add file1.js file2.css
git commit -m "your message"
```

### I added a file by mistake. How do I remove it?

```bash
git restore --staged <filename>
```

---

## Working with Branches

### I want to create a new branch and work on it

```bash
git switch -c <new-branch-name>
```

Now you can make changes and commit them to this new branch.

### I want to delete a branch I don't need anymore

Delete from your computer:

```bash
git branch -d <branch-name>
```

If it doesn't let you delete, use `-D` instead:

```bash
git branch -D <branch-name>
```

Delete from remote:

```bash
git push origin --delete <branch-name>
```

### I want to rename my branch

```bash
git branch -m <new-name>
git push origin -u <new-name>
git push origin --delete <old-name>
```

---

## Fixing Your Mistakes

### I changed some files but want them back to how they were

Reset everything:

```bash
git restore .
```

Reset just one file:

```bash
git restore <filename>
```

### I made a commit but forgot to add some files

```bash
git add <forgotten-files>
git commit --amend --no-edit
```

### I want to change my last commit message

```bash
git commit --amend -m "new message"
```

### I want to undo my last commit but keep the changes

```bash
git reset --soft HEAD~1
```

### I want to undo my last commit and delete the changes too

```bash
git reset --hard HEAD~1
```

### I already pushed my commit. Can I still fix it?

Yes, but be careful:

```bash
git commit --amend
git push --force
```

**Warning:** Only do this on your own branch, not on shared branches!

---

## Working with Others

### Someone made changes. How do I get them?

```bash
git pull
```

### I made changes but someone else also made changes. Now git pull is not working

Save your work first:

```bash
git stash
```

Get the new changes:

```bash
git pull
```

Get your work back:

```bash
git stash pop
```

### I got conflicts after pulling. What do I do?

1. Open the files with conflicts
2. Look for these markers: `<<<<<<<`, `=======`, `>>>>>>>`
3. Choose which code you want to keep
4. Delete the markers
5. Save the file
6. Run:

```bash
git add <fixed-files>
git merge --continue
```

If you mess up and want to start over:

```bash
git merge --abort
```

### I need to update my branch with the main branch

```bash
git switch main
git pull
git switch <your-branch>
git merge main
```

Fix any conflicts if they appear, then:

```bash
git add .
git merge --continue
git push
```

---

## Some Advanced Stuff

### I have too many commits. Can I combine them into one?

```bash
git reset --soft HEAD~<number-of-commits>
git commit -m "combined message"
git push --force
```

### I want to copy one commit from another branch to mine

First, find the commit code (looks like `a1b2c3d`):

```bash
git log
```

Then copy it:

```bash
git cherry-pick <commit-code>
```

### Can I update my branch without creating a merge commit?

Yes, use rebase:

```bash
git pull --rebase
```

If you get conflicts:

1. Fix them
2. Run `git add <files>`
3. Run `git rebase --continue`
4. Push: `git push --force`

To cancel the rebase:

```bash
git rebase --abort
```

---

## Oh No! Emergency Help

### I pushed bad code and need to undo it right now!

```bash
git revert <commit-code>
git push
```

This creates a new commit that undoes the bad one.

### I want to make my branch exactly like another branch

```bash
git reset --hard origin/<other-branch-name>
```

**Warning:** This deletes all your changes!

### I want to completely remove my last few commits

```bash
git reset --hard HEAD~<number-of-commits>
git push --force
```

**Warning:** This deletes them permanently!

### I deleted something important. Can I get it back?

Maybe! Check your git history:

```bash
git reflog
```

Find the commit you want and:

```bash
git cherry-pick <commit-code>
```

---

## Quick Commands

```bash
# See what changed
git status

# Save changes
git add .
git commit -m "message"
git push

# Get latest code
git pull

# Make a new branch
git switch -c <branch-name>

# Change branches
git switch <branch-name>

# Undo all changes
git restore .

# Save work for later
git stash

# Get saved work back
git stash pop
```

---

## Common Problems

**"Your branch has diverged"**

```bash
git pull --rebase
```

**"Merge conflict"**

- Open the file, fix it manually
- Run `git add <file>` and `git merge --continue`

**"Permission denied"**

- Check your credentials
- Make sure you have access to the repository

---

That's it! Remember: when you're confused, `git status` is your friend.
