# GitHub Beginner's Guide for Fusion

Welcome! This guide will help you get started with GitHub and contribute to the Fusion project. Don't worry if you're new to this - we'll walk through everything step by step.

## Table of Contents
1. [What is GitHub?](#what-is-github)
2. [Key Terms You Need to Know](#key-terms-you-need-to-know)
3. [Setting Up Your GitHub Account](#setting-up-your-github-account)
4. [Step-by-Step: Your First Contribution](#step-by-step-your-first-contribution)
5. [Understanding the Workflow](#understanding-the-workflow)
6. [Common Commands Cheat Sheet](#common-commands-cheat-sheet)
7. [Troubleshooting Common Issues](#troubleshooting-common-issues)
8. [Getting Help](#getting-help)

## What is GitHub?

**GitHub** is a platform where developers can store, share, and collaborate on code. Think of it as a social network for programmers, where instead of sharing photos, you share and collaborate on code.

**Git** is the tool that tracks changes in your code, while **GitHub** is the online platform where you can store your Git repositories and collaborate with others.

### Why We Use GitHub for Fusion
- **Version Control**: Track every change made to the code
- **Collaboration**: Multiple developers can work together
- **Code Review**: Team members can review and suggest improvements
- **Issue Tracking**: Report bugs and request features
- **Documentation**: Keep all project information in one place

## Key Terms You Need to Know

Before we dive in, let's understand some important terms:

### Repository (Repo)
A repository is like a project folder that contains all your code files, documentation, and the history of all changes made to them.

### Fork
Creating your own copy of someone else's repository. You can make changes to your fork without affecting the original project.

### Clone
Downloading a repository from GitHub to your local computer so you can work on it.

### Branch
A separate version of your code where you can make changes without affecting the main code. Think of it like a parallel universe for your code.

### Commit
Saving your changes with a descriptive message. It's like a checkpoint in a video game - you can always come back to it.

### Pull Request (PR)
A request to merge your changes into the main project. This is how you submit your contributions for review.

### Push
Uploading your local changes to GitHub.

### Pull
Downloading changes from GitHub to your local computer.

### Merge
Combining changes from one branch into another.

### Remote
The version of the repository stored on GitHub (as opposed to your local copy).

## Setting Up Your GitHub Account

### Step 1: Create a GitHub Account
1. Go to [github.com](https://github.com)
2. Click "Sign up" in the top right corner
3. Follow the prompts to create your account
4. Verify your email address

### Step 2: Install Git on Your Computer

**On Ubuntu/Linux:**
```bash
sudo apt-get update
sudo apt-get install git
```

**On Windows:**
1. Download Git from [git-scm.com](https://git-scm.com/download/win)
2. Run the installer
3. Use the default settings (they work fine for beginners)

**On Mac:**
```bash
brew install git
# OR download from git-scm.com
```

### Step 3: Configure Git
Open your terminal (Command Prompt on Windows, Terminal on Mac/Linux) and run:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Replace "Your Name" and "your.email@example.com" with your actual name and email.

## Step-by-Step: Your First Contribution

### Step 1: Fork the Fusion Repository
1. Go to [https://github.com/FusionIIIT/Fusion](https://github.com/FusionIIIT/Fusion)
2. Click the **Fork** button in the top right corner
3. GitHub will create a copy of the repository under your account
4. You'll be redirected to your fork at `https://github.com/<your-username>/Fusion`

### Step 2: Clone Your Fork to Your Computer
1. On your fork's page, click the green **Code** button
2. Copy the URL (it should look like `https://github.com/<your-username>/Fusion.git`)
3. Open your terminal and navigate to where you want to store the project:
   ```bash
   cd ~/Documents  # or wherever you want
   ```
4. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/Fusion.git
   ```
5. Enter the project directory:
   ```bash
   cd Fusion
   ```

### Step 3: Set Up the Original Repository as "Upstream"
This lets you get updates from the main Fusion repository:

```bash
git remote add upstream https://github.com/FusionIIIT/Fusion.git
```

To verify it worked:
```bash
git remote -v
```

You should see both `origin` (your fork) and `upstream` (the original repo).

### Step 4: Create a New Branch for Your Work
Never work directly on the `master` branch! Always create a new branch:

```bash
git checkout -b my-first-contribution
```

Replace `my-first-contribution` with a descriptive name for what you're working on (e.g., `fix-login-bug` or `add-user-profile`).

### Step 5: Make Your Changes
1. Open the project in your favorite text editor
2. Make your changes to the files
3. Save your work

### Step 6: Check What You've Changed
```bash
git status
```

This shows you which files you've modified.

To see the actual changes:
```bash
git diff
```

### Step 7: Stage Your Changes
Add the files you want to commit:

```bash
git add .  # adds all changed files
# OR
git add filename.py  # adds a specific file
```

### Step 8: Commit Your Changes
```bash
git commit -m "Brief description of what you changed"
```

Example:
```bash
git commit -m "Fix login button alignment on homepage"
```

**Tips for good commit messages:**
- Be clear and concise
- Start with a verb (Fix, Add, Update, Remove)
- Keep it under 50 characters if possible

### Step 9: Push Your Changes to GitHub
```bash
git push origin my-first-contribution
```

Replace `my-first-contribution` with the name of your branch.

### Step 10: Create a Pull Request
1. Go to your fork on GitHub (`https://github.com/<your-username>/Fusion`)
2. You'll see a banner suggesting you create a pull request - click **Compare & pull request**
3. Make sure the "base repository" is `FusionIIIT/Fusion` and "base" is the correct target branch
4. Make sure the "head repository" is your fork and "compare" is your branch
5. Fill in the title and description:
   - Title format: `<module_name> : <week_no> : <PR_Title>`
   - Describe what you changed and why
6. Click **Create pull request**

Congratulations! 🎉 You've just made your first pull request!

### Step 11: Wait for Review
- The project maintainers will review your changes
- They might ask you to make some modifications
- If changes are requested, make them on your local branch, commit, and push - the PR will update automatically

## Understanding the Workflow

Here's a visual representation of the contribution workflow:

```
1. Fork the repo on GitHub
   FusionIIIT/Fusion → YourUsername/Fusion

2. Clone your fork to your computer
   GitHub → Your Computer

3. Create a branch
   master → your-feature-branch

4. Make changes and commit
   Edit files → git add → git commit

5. Push to your fork
   Your Computer → GitHub (your fork)

6. Create Pull Request
   Your fork → Original repo (FusionIIIT/Fusion)

7. Review and Merge
   Maintainers review → Merge into main repo
```

## Common Commands Cheat Sheet

### Basic Commands
```bash
# Check repository status
git status

# View your branches
git branch

# Switch to a different branch
git checkout branch-name

# Create and switch to a new branch
git checkout -b new-branch-name

# View commit history
git log

# View commit history (compact)
git log --oneline

# View changes before staging
git diff
```

### Syncing with Upstream
```bash
# Get the latest changes from upstream
git fetch upstream

# Merge upstream changes into your current branch
git merge upstream/master

# Or do both in one command
git pull upstream master
```

### Undoing Changes
```bash
# Discard changes in a specific file (before staging)
git checkout -- filename

# Unstage a file (keep the changes)
git reset HEAD filename

# View the last commit
git show
```

## Troubleshooting Common Issues

### Issue 1: "Permission denied (publickey)" Error

**Problem**: Git can't access GitHub because SSH keys aren't set up.

**Solution**: Use HTTPS URLs instead, or set up SSH keys following [GitHub's guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

### Issue 2: Merge Conflicts

**Problem**: Your changes conflict with changes made by someone else.

**Solution**:
1. Pull the latest changes: `git pull upstream master`
2. Git will mark the conflicts in your files
3. Open the conflicted files and look for markers like `<<<<<<<`, `=======`, `>>>>>>>`
4. Edit the file to resolve the conflict
5. Remove the conflict markers
6. Save the file
7. Stage and commit: `git add filename`, then `git commit -m "Resolve merge conflict"`

### Issue 3: Accidentally Committed to Master Branch

**Problem**: You made changes directly on master instead of a feature branch.

**Solution**:
```bash
# Create a new branch with your current changes
git checkout -b my-new-branch

# Switch back to master
git checkout master

# Reset master to match upstream
git reset --hard upstream/master
```

### Issue 4: Forgot to Pull Before Making Changes

**Problem**: Your local branch is behind the remote.

**Solution**:
```bash
# Save your changes temporarily
git stash

# Pull the latest changes
git pull upstream master

# Reapply your changes
git stash pop
```

### Issue 5: Want to Undo Last Commit

**Problem**: You committed something by mistake.

**Solution**:
```bash
# Undo the last commit but keep the changes
git reset --soft HEAD~1

# Undo the last commit and discard the changes (careful!)
git reset --hard HEAD~1
```

## Getting Help

### Resources
- **Project Documentation**: Read [README.md](README.md) and [CONTRIBUTING.md](CONTRIBUTING.md)
- **GitHub Docs**: [docs.github.com](https://docs.github.com)
- **Git Tutorial**: [git-scm.com/doc](https://git-scm.com/doc)
- **Interactive Git Tutorial**: [learngitbranching.js.org](https://learngitbranching.js.org)

### When You're Stuck
1. **Search for the error message**: Most common issues have been solved by others
2. **Check the project's existing issues**: Someone might have had the same question
3. **Ask for help**: Create an issue or reach out to the community
4. **Be specific**: Include error messages, what you tried, and what you expected to happen

### GitHub-Specific Help
- [GitHub Quickstart](https://docs.github.com/en/get-started/quickstart)
- [About Pull Requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)
- [Forking Projects](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

## Next Steps

Now that you understand the basics:

1. **Practice**: The best way to learn is by doing
2. **Read the Code**: Explore the Fusion codebase to understand how it works
3. **Start Small**: Look for issues labeled "good first issue" or "beginner-friendly"
4. **Ask Questions**: Don't hesitate to ask when you're unsure
5. **Review Others' Code**: Learn by reading other people's pull requests

Remember: Everyone was a beginner once. Don't be afraid to make mistakes - that's how we learn! The community is here to help you.

---

**Ready to contribute?** Head over to [CONTRIBUTING.md](CONTRIBUTING.md) for project-specific contribution guidelines!

**Need setup help?** Check out [README.md](README.md) for detailed installation instructions.
