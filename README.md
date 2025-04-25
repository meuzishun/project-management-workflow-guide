# 🛠️ Git & Jira Workflow Guide (Team Practice)

A professional-style workflow for contributors and reviewers to simulate working on a dev team using Git, GitHub, and Jira.

## Table of Contents

- [Contributor Workflow](#contributor-workflow)
  - [Pick a Jira Ticket](#pick-a-jira-ticket)
  - [Sync with Remote main](#sync-with-remote-main)
  - [Create a New Branch](#create-a-new-branch)
  - [Do the Work](#do-the-work)
  - [Rebase with main OFTEN](#rebase-with-main-often)
  - [Squash Commits](#squash-commits)
  - [Push Your Branch](#push-your-branch)
  - [Handle Review Feedback](#handle-review-feedback)
  - [After Merge](#after-merge)
- [Reviewer Workflow](#reviewer-workflow)
  - [Get Assigned a PR](#get-assigned-a-pr)
  - [Pull the Branch Locally](#pull-the-branch-locally)
  - [Test the Code Locally](#test-the-code-locally)
  - [Review the PR on GitHub](#review-the-pr-on-gitHub)
  - [If Approved](#if-approved)
  - [Clean Up Locally](#clean-up-locally)

## Contributor Workflow

### Pick a Jira Ticket

- Move it to "In Progress".
- Assign it to yourself.

### Sync with Remote main

```bash
git checkout main
git pull origin main
```

### Create a New Branch

```
git checkout -b feat/ABC-123-short-description
```

- Naming format:

  - feat/ABC-123-login-form
  - bugfix/ABC-456-form-validation
  - chore/ABC-789-update-deps

### Do the Work

- Commit often with descriptive messages:

  ```
  git commit -m "ABC-123: Add login form with validation"
  ```

### Rebase with main OFTEN

Rebase keeps a linear history and avoids noisy merge commits. Perfect for clean PRs.

```
git fetch origin
git rebase origin/main
```

- If there are conflicts, Git will pause and let you fix them:

  ```
  # after fixing conflicts in your editor
  git add .
  git rebase --continue
  ```

- Or, if things go sideways:

  ```
  git rebase --abort  # bail out and go back to how things were
  ```

### Squash Commits

If you've made multiple commits while working on a feature, it's best to clean them up before merging. This keeps the project history easy to read.

#### 1. Check how many commits you’re ahead of `main`:

```bash
git log --oneline origin/main..HEAD
```

Count the number of commits listed.

#### 2. Start an interactive rebase:

Replace `4` with the number of commits you saw above.

```bash
git rebase -i HEAD~4
```

This will open your editor with a list like this:

```
pick 1a2b3c4 Add login form layout
pick 2b3c4d5 Add validation logic
pick 3c4d5e6 Fix button alignment
pick 4d5e6f7 Rename variables for clarity
```

#### 3. Change all but the first `pick` to `squash` or `s`:

```
pick 1a2b3c4 Add login form layout
squash 2b3c4d5 Add validation logic
squash 3c4d5e6 Fix button alignment
squash 4d5e6f7 Rename variables for clarity
```

This tells Git to combine all of those commits into one.

#### 4. Edit the commit message:

Git will then open a new editor window. You'll see something like this:

```
# This is a combination of 4 commits.
# The first commit's message is:
Add login form layout

# The commit message for your squash commit:
Add login form layout

# You can edit this to summarize all the changes:
```

Update it to something clear and descriptive:

```
ABC-123: Add login form with validation and cleanup
```

Save and close the editor. Git will finish squashing the commits.

#### 5. Push your changes:

If you've already pushed this branch before, you'll need to force push:

```bash
git push --force-with-lease
```

> ✅ Use `--force-with-lease` instead of `--force` — it’s safer because it prevents you from overwriting someone else’s work by accident.

### Create a Pull Request

- Link to the Jira ticket by including the ticket ID in the PR title and description, or use Jira/GitHub integration for automatic linking.

- Include:

  - Overview of changes

  - Screenshots (if visual)

  - Notes for the reviewer

- Assign yourself as the author and pick a teammate to review.

### Handle Review Feedback

- Push updates as needed.

- Rebase again if necessary.

### After Merge

```
git checkout main
git pull origin main
git branch -d feat/ABC-123-short-description
git remote prune origin
```

## Reviewer Workflow

### Get Assigned a PR

- React with excitement 😅

### Pull the Branch Locally

```
git fetch origin
git checkout feat/ABC-123-short-description
```

### Test the Code Locally

- Run it. Try it out.

### Review the PR on GitHub

- Use inline comments.
- Leave constructive feedback.
- Use GitHub review tools:
  - Approve
  - Request Changes

### If Approved

- Merge using Squash and Merge.
- Delete the remote branch.

### Clean Up Locally

```
git checkout main
git pull origin main
git branch -d feat/ABC-123-short-description
```

✅ Team Best Practices

- Always include the Jira ticket ID in branch names and commit.
- Make small, focused commits.
- Rebase often to keep your branch conflict-free.
- Use PR templates and follow code review etiquette.
- Keep your local branches clean (use --prune often).
- Learn by doing — mistakes are part of the process!

🧪 Optional Team Challenges

- Rotate who reviews PRs each sprint.
- Simulate messy PRs to practice conflict resolution.
- Appoint a rotating "Tech Lead" to assign or triage tickets.
- Do pair programming or live code walkthroughs occasionally.
- This workflow is meant for practice and team growth. Customize it to fit your crew’s vibe and goals!

---
