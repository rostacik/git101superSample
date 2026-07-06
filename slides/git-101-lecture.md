---
marp: true
theme: default
paginate: true
---

# Git 101 — Introduction to Version Control
## 1-Hour Lecture for College Students

> **Speaker notes**: This is a demo-heavy lecture. Show the terminal for every command. Keep slides minimal. The goal is to build the mental model, not to memorize flags.

---

## Slide 1: Why Git?

- You have a file. You save `paper.txt`, `paper_final.txt`, `paper_FINAL_v2.txt`.
- You work in a team. Someone else overwrites your changes.
- You break something and want to go back.

### Git is a time machine for your code.

> **Speaker notes**: Start with a relatable example (essay, project, or code). Ask who has used "Save As" with version numbers. Emphasize that Git solves the same problem, but systematically.

---

## Slide 2: Git vs GitHub

| Git | GitHub |
|-----|--------|
| Version control software | Hosting service for Git repositories |
| Runs on your computer | Runs in the cloud |
| Tracks history | Shares history with others |
| Free and open-source | Free tier for public repos |

- **Git** = the tool
- **GitHub** = the place where you store and share

> **Speaker notes**: Many students confuse Git and GitHub. Clarify immediately. Use analogy: Git is the camera, GitHub is the photo album.

---

## Slide 3: The 3-Area Model

```
Working Directory        Staging Area           Repository
    (edit)        -->    (prepare)     -->    (save)
    git add              git commit
```

1. **Working Directory** — your files on disk
2. **Staging Area** — a list of changes you want to save
3. **Repository** — the permanent history of snapshots

> **Speaker notes**: This is the most important mental model. Draw it on the board. Do not move on until students can repeat: edit → stage → commit. Everything else in Git is an extension of this idea.

---

## Slide 4: Your First Repository

```bash
# Create a folder
mkdir git-demo && cd git-demo

# Initialize Git
git init

# Check status
git status

# Create a file
echo "# My Project" > README.md

# Stage the file
git add README.md

# Commit the file
git commit -m "Initial commit: add README"

# View history
git log
```

> **Speaker notes**: Live demo from scratch. Talk out loud as you type. Explain `git status` color codes (red = modified, green = staged). Show `git log` output immediately so they see history exists.

---

## Slide 5: Making More Changes

```bash
# Edit README.md
echo "This is a demo project." >> README.md

# Check status
git status

# Stage and commit in one go for tracked files
git add README.md
git commit -m "Add project description"

# View compact history
git log --oneline
```

> **Speaker notes**: Show the difference between tracked and untracked files. Mention that `git add` does not save the file forever — it only moves it to staging. `git commit` is the permanent save.

---

## Slide 6: Branching — Working in Parallel

- A branch is a separate line of development.
- You create a branch to experiment or build a feature without touching the main code.

```
main:     A --- B --- C
                 feature:         D --- E
```

```bash
# Create and switch to a new branch
git checkout -b feature/about-me

# Make a change
echo "- Author: Student" >> README.md

# Stage and commit
git add README.md
git commit -m "Add author info"

# Switch back to main
git checkout main

# View all branches
git branch
```

> **Speaker notes**: Draw the branch diagram before running commands. Explain that `git checkout -b` is a shortcut for creating and switching. Let them see the file content change when switching branches.

---

## Slide 7: Merging

### Merge your branch back into `main`

```bash
# Make sure you are on main
git checkout main

# Merge the feature branch
git merge feature/about-me

# View history as a graph
git log --oneline --graph --all
```

### Result
- The histories of both branches are combined.
- Fast-forward merge if no conflict.

> **Speaker notes**: Explain that `main` is the default branch name. If there is a conflict, show the conflict markers briefly but tell them it will be covered in the next session. Run `git log --graph` so they see the visual merge.

---

## Slide 8: Remote Repositories

### GitHub workflow
- You have a local repository.
- You want to share it or back it up.
- You create a remote repository on GitHub and link it.

```bash
# Add a remote (GitHub URL)
git remote add origin https://github.com/yourusername/yourrepo.git

# Push local main branch to remote
git push -u origin main

# Clone an existing repo (for students)
git clone https://github.com/rostacik/git101superSample.git
```

> **Speaker notes**: This is the collaboration section. If time is short, focus on `clone` and `push`. Explain that after `-u origin main`, future pushes can be just `git push`. Show the sample repo as a real-world example.

---

## Slide 9: Collaboration Exercise

1. Clone the sample repo:
   ```bash
   git clone https://github.com/rostacik/git101superSample.git
   cd git101superSample
   ```
2. Create a branch:
   ```bash
   git checkout -b feature/my-first-change
   ```
3. Edit a file (e.g., add your name to a list).
4. Commit:
   ```bash
   git add .
   git commit -m "Add my name to contributors"
   ```
5. Push:
   ```bash
   git push -u origin feature/my-first-change
   ```

> **Speaker notes**: Walk around the room. Most errors will be: not saving the file, not staging before commit, or typing the wrong branch name. Let them help each other.

---

## Slide 10: What is a Pull Request?

- A **Pull Request** is a request to merge your branch into `main`.
- It happens on GitHub (not in the terminal).
- It allows code review before merging.

### Workflow
```
Push branch → Open PR on GitHub → Review → Merge
```

> **Speaker notes**: Show the GitHub interface briefly. Explain that in real teams, nobody pushes directly to `main`. The PR is the standard gate for quality.

---

## Slide 11: The Golden Rules

1. **Commit often** — small commits are easier to understand.
2. **Write meaningful messages** — `git commit -m "Fix login bug"` is better than `git commit -m "update"`.
3. **Pull before you push** — always sync before sharing your work.
4. **Create a branch for every feature** — keep `main` stable.
5. **Use `.gitignore`** — never commit secrets, build files, or dependencies.

```bash
# Example .gitignore
node_modules/
*.exe
.env
```

> **Speaker notes**: These are the habits that separate beginners from professionals. Mention that `.gitignore` is a simple text file that tells Git what to skip.

---

## Slide 12: Common Beginner Mistakes

| Mistake | Why it happens | How to fix |
|---------|---------------|------------|
| `git commit` without `git add` | Forgetting the staging area | Run `git add` first, then commit |
| Pushing to `main` directly | Not understanding branch workflow | Create a feature branch first |
| Merge panic | Seeing conflict markers for the first time | Read the markers, edit file, add, commit |
| Forgetting `-m` | Git opens a text editor | Configure a default editor or always use `-m` |

> **Speaker notes**: Reassure them that everyone makes these mistakes. Git is safe — you rarely lose committed work.

---

## Slide 13: What We Skipped (On Purpose)

- `git rebase` — rewriting history
- `git stash` — temporary shelving
- `git cherry-pick` — copying commits
- `git reflog` — recovery commands
- SSH key setup (use HTTPS for now)

> **Speaker notes**: Acknowledge these exist. Tell them they are powerful but not needed for the first week. If they understand the 3-area model and branching, they can learn these later.

---

## Slide 14: Summary & Homework

- The 3-area model (working → staging → repository)
- Local workflow: `init`, `add`, `commit`, `log`
- Branching: `checkout -b`, `merge`
- Remote basics: `clone`, `push`
- The concept of a Pull Request

### Homework
1. Create a new repo for a personal project.
2. Make 3 commits on `main`.
3. Create a branch, add a feature, merge it back.
4. Push to GitHub.
5. Explore the repo history on GitHub.

> **Speaker notes**: Encourage them to try it alone. If they can do the homework without slides, they understood the core idea.

---

## Appendix: Cheat Sheet

```bash
# Setup
git init                         # Create a new repo
git clone <url>                  # Copy a remote repo

# Daily workflow
git status                       # See what changed
git add <file>                   # Stage a file
git add .                        # Stage all changes
git commit -m "message"          # Save staged changes
git log --oneline                # View history

# Branching
git branch                       # List branches
git checkout -b <name>          # Create and switch
git checkout <name>              # Switch branch
git merge <name>                 # Merge branch into current

# Remote
git remote add origin <url>     # Link remote
git push -u origin main         # Push branch
git pull                         # Download and merge changes
```

---

## Sample Repo Reference

**Repository:** [https://github.com/rostacik/git101superSample](https://github.com/rostacik/git101superSample)

Use this repo as the collaboration target for the exercise in Slide 9.

> **Speaker notes**: Make sure the repo is public and has a simple README. Consider adding a `CONTRIBUTORS.md` file so students have a clear target to edit.
