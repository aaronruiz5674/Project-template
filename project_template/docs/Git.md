# Git – Gitflow, Branch Naming, and Commit Messages

## What is Gitflow?
**Gitflow** is a branching model designed for projects requiring structured collaboration and predictable release cycles. It organizes work into **branches with specific roles**, helping teams avoid conflicts and maintain a stable codebase.

### Main Branches
- **main**: Contains production-ready, stable code.
- **develop**: Integration branch for features ready for the next release.

### Support Branches
- **feature/**: For new features, branched from `develop` and merged back when complete.
- **release/**: Prepares a stable version for production, allowing minor bug fixes or tweaks before merging into `main` and `develop`.
- **hotfix/**: For urgent fixes to production issues, branched from `main` and merged back into `main` and `develop`.

### Gitflow Workflow
1. Create a `feature/` branch from `develop` for new work.
2. Commit changes to the `feature/` branch.
3. Merge the completed `feature/` branch back into `develop`.
4. When ready for production, create a `release/` branch from `develop`.
5. Test and apply minor fixes in the `release/` branch, then merge into `main` and `develop`. Tag the release in `main` (e.g., `git tag v1.0.0`).
6. For urgent production fixes, create a `hotfix/` branch from `main`, apply fixes, and merge back into `main` and `develop`.

### Branch Roles Table
| Branch       | Purpose                              | Source   | Merged Into         |
|--------------|--------------------------------------|----------|---------------------|
| main         | Production-ready code                | -        | -                   |
| develop      | Integration of new features          | -        | main                |
| feature/     | New feature development              | develop  | develop             |
| release/     | Prepare for production release       | develop  | main, develop       |
| hotfix/      | Urgent production fixes              | main     | main, develop       |

## Branch Naming Conventions
Consistent and descriptive branch names improve collaboration, readability, and compatibility with automation tools like CI/CD pipelines. Use lowercase letters and hyphens for clarity.

- **feature/**: For new features.  
  - `feature/add-dataloader`  
  - `feature/JIRA-123-implement-mlflow-tracking`  
- **release/**: For release preparation.  
  - `release/v1.0.0`  
- **hotfix/**: For urgent production fixes.  
  - `hotfix/critical-security-patch`  
  - `hotfix/v1.0.1-login-fix`  

**Notes**:
- Include issue/ticket numbers if applicable (e.g., `feature/JIRA-123-add-dataloader`).
- Some teams use `bugfix/` for non-production fixes (e.g., `bugfix/torch-device-error`), but this is not standard in Gitflow.
- Avoid spaces or special characters in branch names.

## Git Commit Messages
Effective commit messages are concise, descriptive, and follow a consistent format. They should explain **what** changed and **why**, using present-tense verbs (e.g., "add", "fix").

### Recommended Style: Conventional Commits
Use the format: `<type>(<scope>): <short description>`

- **Types**:  
  - `feat`: New feature  
  - `fix`: Bug fix  
  - `docs`: Documentation changes  
  - `style`: Code style/formatting (no logic changes)  
  - `refactor`: Code restructuring without changing functionality  
  - `test`: Adding or fixing tests  
  - `chore`: Miscellaneous tasks (e.g., configs, dependencies)  

- **Structure**:  
  - Summary: 50–70 characters, starting with type and scope.  
  - Optional description: Detailed explanation, wrapped at 72 characters.  
  - Optional issue reference: e.g., `Fixes #123`.

 
### Examples
- `feat(data): add MNIST dataloader`  
- `fix(train): correct tensor shape mismatch`  
- `docs(mlflow): add usage examples to README`  
- `refactor(model): simplify forward pass`  
- `chore: update .gitignore to exclude mlruns/`  
- Multi-line example:  
```plaintext
feat(auth): add JWT-based user authentication

Implement JSON Web Token authentication for secure user login.
Add middleware to protect routes and handle token validation.
Fixes #456
```
  
## Resources
- [Gitflow Workflow – Atlassian Guide](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow): Detailed guide to implementing Gitflow.
- [Conventional Commits](https://www.conventionalcommits.org/): Standard for structured commit messages.