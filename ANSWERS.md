# TP5 – Git and GitHub
## Answers

### Exercise 1 – Install and configure Git

**Q1. What does `--global` mean? Where is this configuration stored?**

`--global` means that the configuration applies to all Git repositories of the current user. It is stored in the `~/.gitconfig` file.

**Q2. Is a GitHub account required to make a local commit? Justify.**

No. Git works locally. A GitHub account is only needed to publish the repository online and collaborate with other developers.

---

### Exercise 2 – Create a local repository

**Q1. Why are the files listed as untracked?**

Untracked files are files that Git knows exist but does not track yet. They must be added using `git add`.

**Q2. What is the purpose of each line in `.gitignore`?**

- `.env`: ignores environment files that may contain secrets.
- `*.log`: ignores all log files.
- `__pycache__/`: ignores Python cache directories.
- `.DS_Store`: ignores macOS system files.

---

### Exercise 3 – Stage, commit and inspect

**Q1. What is the difference between the working tree, the staging area and the repository?**

- Working tree: contains the project files and local modifications.
- Staging area: contains changes prepared for the next commit.
- Repository: stores the project's commit history.

**Q2. Why can a commit contain only some of the modified files?**

Because Git allows us to select specific files using `git add` before creating a commit.

**Q3. Give one example of a good and one example of a bad commit message.**

- Good: `Update welcome message`
- Bad: `Changes`

A good commit message clearly describes the modification.

---

### Exercise 4 – Branching and merging

**Q1. Was the merge a fast-forward or a three-way merge? How can you tell from the history?**

It was a three-way merge because both `main` and `feature/registration` had different commits. The history shows a merge commit with two parent commits.

**Q2. What would have happened if you had not made the commit on main in step 2?**

Git would have performed a fast-forward merge because `main` had no new commit after the common ancestor.

**Q3. Why is it good practice to delete a feature branch after merging?**

Deleting a merged feature branch keeps the repository clean and avoids unnecessary branches.

Command:
`git branch -d feature/registration`

---

### Exercise 5 – Undoing changes

**Scenario A: Discard unstaged modifications**

```bash
git restore index.html
```

This command discards unstaged changes and restores the file to its last committed version.

**Scenario B: Unstage a file without losing edits**

```bash
git restore --staged README.md
```

This command removes the file from the staging area but keeps the modifications in the working tree.

**Scenario C: Cancel a shared commit without rewriting history**

```bash
git revert HEAD
```

This command creates a new commit that reverses the previous commit. It is safe for shared branches because it preserves history.

**Scenario D: Undo a local commit but keep the changes**

```bash
git reset --mixed HEAD~1
```

This command removes the last commit but keeps the modifications in the working tree, outside the staging area.

**Scenario E: Save unfinished work and restore it later**

```bash
git stash push -m "Save unfinished work"
git stash list
git stash pop
```

`git stash` temporarily saves unfinished changes. `git stash pop` restores them and removes the stash entry.

**Q1. What is the difference between `git revert` and `git reset`? Which one is safe on a shared branch, and why?**

`git revert` creates a new commit to reverse changes and preserves history.

`git reset` moves the current branch to an earlier commit and can rewrite local history.

`git revert` is safer on a shared branch because it does not rewrite existing history.

**Q2. What is the difference between `git reset --soft`, `--mixed` and `--hard`?**

- `--soft`: removes the last commit but keeps changes staged.
- `--mixed`: removes the last commit and keeps changes unstaged. This is the default mode.
- `--hard`: removes the last commit and discards changes from the staging area and working tree.

---

### Exercise 6 – Publish to GitHub

**Q1. What is the difference between commit and push?**

`commit` saves changes in the local repository.

`push` sends local commits to the remote repository on GitHub.

**Q2. Which authentication method did you use? Why must a token never appear in a command or a file?**

Authentication method: [Complete with the method actually used: Git Credential Manager, GitHub CLI or SSH].

A token must never appear in a command or file because it is a secret credential. Someone could steal it and access the account.

**Q3. Suppose you accidentally committed a file containing a password and pushed it. Is deleting the file in a new commit enough? What should you do?**

No. The password may still exist in the Git history. It must be revoked or changed immediately. The sensitive data must also be removed from the repository history when necessary.

---

### Exercise 7 – Pull Request and Code Review

**Q1. Why do teams protect the main branch?**

Teams protect `main` to prevent unreviewed or incorrect code from being merged. It helps maintain code quality and stability.

**Q2. Name three things a reviewer should check in a Pull Request.**

1. Code correctness and functionality.
2. Code readability and organization.
3. Possible bugs and security problems.

**Q3. How does this workflow relate to continuous integration (TP6)?**

Pull Requests allow code to be reviewed and tested before merging. Continuous Integration can automatically run tests and checks when code is pushed or a Pull Request is created.

---

### Exercise 8 – Create and resolve a conflict

**Q1. What do the markers `<<<<<<<`, `=======` and `>>>>>>>` represent?**

- `<<<<<<<`: marks the beginning of the current branch's changes.
- `=======`: separates the two versions.
- `>>>>>>>`: marks the end of the incoming branch's changes.

**Q2. Why did Git not resolve this conflict automatically?**

Because both branches modified the same line differently. Git could not determine which version was correct.

**Q3. Name two practices that reduce the number of conflicts in a team.**

1. Communicate regularly with other developers.
2. Pull and synchronize changes frequently before starting new work.

---

### Exercise 9 – Tags and releases

**Q1. What is the difference between a branch and a tag?**

A branch is a movable reference to the latest commit of a line of development. A tag identifies a specific commit, usually to mark a release.

**Q2. Explain the meaning of each number in semantic versioning (MAJOR.MINOR.PATCH). Which number would you increase after fixing a small bug?**

- MAJOR: incompatible changes.
- MINOR: new features that are backward-compatible.
- PATCH: backward-compatible bug fixes.

For a small bug fix, we increase PATCH. For example, `1.0.0` becomes `1.0.1`.

---

### Bonus – GitHub Actions

**Q1. Which event triggered the workflow, and where can you read its logs?**

The `push` event triggers the workflow. Its execution logs can be viewed in the Actions tab of the GitHub repository.
