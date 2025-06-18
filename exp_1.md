# Experiment 1: Git Version Control and Configuration

## Objective
To understand Git version control system, configure Git environment, perform basic Git operations including repository initialization, branching, merging, and remote repository management.

## Materials
- Computer with internet connection
- Git software
- GitHub account
- Text editor
- Terminal/Command Prompt

## Prerequisites
- Basic understanding of command line interface
- GitHub account created
- Internet connectivity for remote operations

## Procedure

### Step 1: Initial Configuration

#### Install Git (if not already installed)
```bash
# Ubuntu/WSL
sudo apt update
sudo apt install git -y

# Windows - Download from: https://git-scm.com/
```

### Step 2: Check GitHub Version
```bash
# Verify Git installation
git --version
```

**Expected Output:**
```
git version 2.34.1 (or similar)
```

### Step 3: Git Configuration

#### Set Global User Information
```bash
# Configure username
git config --global user.name "Your Name"

# Configure email
git config --global user.email "your.email@example.com"
```

#### Verify Configuration
```bash
# List all global configurations
git config --global --list
```

**Expected Output:**
```
user.name=Your Name
user.email=your.email@example.com
```

### Step 4: Initialize Local Repository
```bash
# Create project directory
mkdir git-demo-project
cd git-demo-project

# Initialize Git repository
git init
```

### Step 5: Create Initial Content
```bash
# Create a README file
echo "# Git Demo Project" > README.md

# Check repository status
git status
```

### Step 6: Stage and Commit Changes
```bash
# Stage files for commit
git add .

# Create initial commit
git commit -m "Initial commit"
```

### Step 7: Connect to Remote Repository

#### Add Remote Origin
```bash
# Add GitHub repository as remote origin
git remote add origin https://github.com/your-username/your-repo.git

# Verify remote repository
git remote -v
```

#### Push to Remote Repository
```bash
# Push main branch to remote
git push -u origin main
```

### Step 8: Branch Management

#### Create Feature Branch
```bash
# Create new branch
git branch feature

# Switch to feature branch
git checkout feature

# Alternative: Create and switch in one command
# git checkout -b feature
```

#### Work on Feature Branch
```bash
# Create a new file
echo "This is a feature file" > feature.txt

# Stage the new file
git add feature.txt

# Commit changes
git commit -m "Second commit"
```

#### Push Feature Branch
```bash
# Push feature branch to remote
git push origin feature
```

### Step 9: Merge Feature Branch

#### Switch to Main Branch
```bash
# Switch back to main branch
git checkout main

# Pull latest changes from remote
git pull origin main
```

#### Merge Feature Branch
```bash
# Merge feature branch into main
git merge feature

# Push merged changes to remote
git push origin main
```

### Step 10: Clean Up (Optional)
```bash
# Delete feature branch locally
git branch -d feature

# Delete feature branch on remote
git push origin --delete feature
```

## Common Git Commands Summary

### Configuration Commands
```bash
git config --global user.name "Name"        # Set username
git config --global user.email "email"      # Set email
git config --global --list                  # View config
git config --global --unset user.name       # Remove config
```

### Repository Operations
```bash
git init                    # Initialize repository
git clone <url>            # Clone remote repository
git status                 # Check repository status
git log                    # View commit history
git log --oneline          # Compact commit history
```

### Staging and Committing
```bash
git add <file>             # Stage specific file
git add .                  # Stage all changes
git commit -m "message"    # Commit with message
git commit -am "message"   # Stage and commit tracked files
```

### Branch Operations
```bash
git branch                 # List local branches
git branch <name>          # Create new branch
git checkout <branch>      # Switch to branch
git checkout -b <branch>   # Create and switch to branch
git merge <branch>         # Merge branch into current
git branch -d <branch>     # Delete branch
```

### Remote Operations
```bash
git remote add origin <url>    # Add remote repository
git remote -v                  # List remote repositories
git push origin <branch>       # Push branch to remote
git pull origin <branch>       # Pull changes from remote
git fetch                      # Fetch changes without merging
```

## Git Workflow Diagram

```
Working Directory → Staging Area → Local Repository → Remote Repository
       ↓                ↓               ↓                ↓
   git add         git commit      git push        git pull
```

## Branch Workflow

```
main branch:    A---C---E---G
                     ↘   ↗
feature branch:        B---D---F
```

Where:
- A: Initial commit
- B: Feature development starts
- C: Main branch continues
- D, F: Feature development
- E: Merge feature into main
- G: Continued development

## Expected Results

### Successful Configuration
- ✅ Git version displayed correctly
- ✅ User name and email configured globally
- ✅ Configuration values verified

### Repository Operations
- ✅ Local repository initialized
- ✅ Remote repository connected
- ✅ Files successfully committed and pushed

### Branch Management
- ✅ Feature branch created and switched
- ✅ Changes committed to feature branch
- ✅ Feature branch merged into main
- ✅ All changes synchronized with remote

## File Structure After Completion
```
git-demo-project/
├── .git/              # Git metadata (hidden)
├── README.md          # Project documentation
└── feature.txt        # Feature file (after merge)
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Git command not found | Install Git or add to PATH |
| Permission denied (publickey) | Configure SSH keys or use HTTPS |
| Merge conflicts | Resolve conflicts manually and commit |
| Branch already exists | Use different name or checkout existing |
| Remote repository not found | Verify URL and repository access |

## Best Practices

### Commit Messages
- Use present tense: "Add feature" not "Added feature"
- Keep first line under 50 characters
- Use imperative mood: "Fix bug" not "Fixes bug"

### Branch Naming
- Use descriptive names: `feature/user-authentication`
- Use hyphens for separation: `fix/login-error`
- Avoid special characters and spaces

### Workflow Tips
1. **Pull before push**: Always pull latest changes before pushing
2. **Frequent commits**: Make small, logical commits
3. **Meaningful messages**: Write clear commit messages
4. **Branch protection**: Use branches for features and fixes
5. **Code review**: Use pull requests for collaboration

## Advanced Git Commands

```bash
# View differences
git diff                    # Show unstaged changes
git diff --staged          # Show staged changes
git diff branch1 branch2   # Compare branches

# Undo operations
git reset HEAD <file>      # Unstage file
git checkout -- <file>     # Discard changes
git revert <commit>        # Revert commit

# Stashing
git stash                  # Save work temporarily
git stash pop              # Restore stashed work
git stash list             # List stashes
```

## Conclusion
This experiment demonstrates fundamental Git operations essential for version control in software development. Git enables collaborative development, tracks changes, and provides powerful branching and merging capabilities. These skills are fundamental for any software development project and form the foundation for DevOps practices including continuous integration and deployment pipelines.

Understanding Git is crucial for:
- **Collaboration**: Multiple developers working on same project
- **Version Control**: Track and manage code changes
- **Backup**: Distributed nature provides redundancy
- **Branching**: Parallel development of features
- **Integration**: Foundation for CI/CD pipelines
