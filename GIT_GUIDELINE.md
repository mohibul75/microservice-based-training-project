# Git Branching Strategy for Event-Driven System

## Overview
This guideline outlines a Git branching strategy to manage the development and deployment of the Event-Driven System. The strategy ensures a clear workflow for feature development, bug fixing, and release management, promoting collaboration and maintaining code quality.

## Branch Types

1. **Main Branch**
   - **`main`**
   - The production-ready branch.
   - Only stable and thoroughly tested code is merged here.
   - Direct commits are not allowed; only pull requests that have passed code review and testing are merged.

2. **Develop Branch**
   - **`develop`**
   - The main branch for ongoing development.
   - Integrates feature branches and serves as the base for creating release branches.
   - Periodically synced with `main` to incorporate hotfixes.

3. **Feature Branches**
   - **`feature/<feature-name>`**
   - Used for developing new features or enhancements.
   - Branches off from `develop` and merges back into `develop` upon completion.
   - Naming convention: `feature/<feature-name>`.

4. **Bugfix Branches**
   - **`bugfix/<bugfix-name>`**
   - Used for fixing bugs found in the `develop` branch.
   - Branches off from `develop` and merges back into `develop` upon completion.
   - Naming convention: `bugfix/<bugfix-name>`.

5. **Release Branches**
   - **`release/<version-number>`**
   - Used to prepare a new production release.
   - Branches off from `develop` and merges into both `main` and `develop` upon release.
   - Naming convention: `release/<version-number>`.
   - Allows for final testing and bug fixes before release.

6. **Hotfix Branches**
   - **`hotfix/<hotfix-name>`**
   - Used for critical fixes that need to be applied to the `main` branch immediately.
   - Branches off from `main` and merges back into both `main` and `develop`.
   - Naming convention: `hotfix/<hotfix-name>`.

## Workflow

1. **Creating a Feature Branch**
   - Checkout from `develop`:
     ```sh
     git checkout develop
     git pull origin develop
     git checkout -b feature/<feature-name>
     ```
   - Work on the feature, commit changes, and push to remote:
     ```sh
     git add .
     git commit -m "Add <feature-name>"
     git push origin feature/<feature-name>
     ```

2. **Merging a Feature Branch**
   - Create a pull request from `feature/<feature-name>` to `develop`.
   - Ensure the pull request is reviewed and approved.
   - Merge the pull request and delete the feature branch.

3. **Creating a Bugfix Branch**
   - Checkout from `develop`:
     ```sh
     git checkout develop
     git pull origin develop
     git checkout -b bugfix/<bugfix-name>
     ```
   - Work on the bugfix, commit changes, and push to remote:
     ```sh
     git add .
     git commit -m "Fix <bugfix-name>"
     git push origin bugfix/<bugfix-name>
     ```

4. **Merging a Bugfix Branch**
   - Create a pull request from `bugfix/<bugfix-name>` to `develop`.
   - Ensure the pull request is reviewed and approved.
   - Merge the pull request and delete the bugfix branch.

5. **Creating a Release Branch**
   - Checkout from `develop`:
     ```sh
     git checkout develop
     git pull origin develop
     git checkout -b release/<version-number>
     ```
   - Perform final testing and apply any necessary fixes.
   - Merge into `main` and `develop`, then tag the release:
     ```sh
     git checkout main
     git merge release/<version-number>
     git tag -a <version-number> -m "Release <version-number>"
     git push origin main --tags

     git checkout develop
     git merge release/<version-number>
     git push origin develop
     ```

6. **Creating a Hotfix Branch**
   - Checkout from `main`:
     ```sh
     git checkout main
     git pull origin main
     git checkout -b hotfix/<hotfix-name>
     ```
   - Work on the hotfix, commit changes, and push to remote:
     ```sh
     git add .
     git commit -m "Hotfix <hotfix-name>"
     git push origin hotfix/<hotfix-name>
     ```
   - Merge into `main` and `develop`:
     ```sh
     git checkout main
     git merge hotfix/<hotfix-name>
     git push origin main

     git checkout develop
     git merge hotfix/<hotfix-name>
     git push origin develop
     ```

## Best Practices

- **Regular Commits:** Commit changes frequently with clear and descriptive messages.
- **Code Reviews:** Ensure all pull requests undergo thorough code reviews before merging.
- **Continuous Integration:** Use CI tools to automatically test and validate changes.
- **Branch Cleanup:** Delete branches after they have been merged to keep the repository clean.
- **Documentation:** Update relevant documentation whenever changes are made to the codebase.

This branching strategy ensures a structured workflow, enhances collaboration, and maintains the quality and stability of the codebase.
