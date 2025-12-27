
# Git Flow Process for Team

This document outlines the process of working with Git Flow in our team, covering branch management, code reviews, and merging strategies.

## 1. **Branching Strategy**

We use the following branches:
- **`main`**: The stable release branch. Only production-ready code is merged here.
- **`develop`**: The integration branch for features. All new features and bug fixes are merged into `develop` before reaching `main`.

### Supporting Branches

- **Feature branches** (`feature/`): For developing new features. These are branched off `develop`.
  - **Naming convention**: `feature/feature-name`
  - **Merge into**: `develop`
  - **Deletion**: After the feature is merged into `develop`
  
- **Hotfix branches** (`hotfix/`): For urgent bug fixes in production. Branched off `main`.
  - **Naming convention**: `hotfix/issue-description`
  - **Merge into**: `main` and `develop`
  - **Deletion**: After the hotfix is merged

- **Release branches** (`release/`): Created when preparing for a new version. Branched off `develop`.
  - **Naming convention**: `release/version-number`
  - **Merge into**: `main` and `develop`
  - **Deletion**: After the release is merged into both `main` and `develop`

## 2. **Feature Branch Workflow**

1. **Branch Creation**: Developers create a new feature branch using Git Flow.
   ```bash
   git flow feature start feature-name
   ```

2. **Development**: Developers work on their features locally.

3. **Push Changes**:
   ```bash
   git add .
   git commit -m "Short description of changes"
   git push origin feature/feature-name
   ```

4. **Publishing a Feature**: If collaborating on a feature, you can publish the feature to the remote repository so other team members can access it.
   ```bash
   git flow feature publish feature-name
   ```

5. **Finish Feature**: Once a feature is completed, finish it with Git Flow.
   ```bash
   git flow feature finish feature-name
   ```

6. **Create Pull Request**: Open a PR from `develop` for review.

## 3. **Collaborating on a Feature**

1. **Getting a Published Feature**: If another user has published a feature, you can pull it to collaborate.
   ```bash
   git flow feature pull origin feature-name
   ```

2. **Tracking a Feature**: If you want to track a feature from the remote repository, you can use the following command:
   ```bash
   git flow feature track feature-name
   ```

## 4. **Code Review Process**
4. **Create Pull Request**: Once a feature is completed, create a pull request (PR) to `develop` for review.

## 3. **Code Review Process**

1. **Creating a Pull Request (PR)**:
   - PRs should contain a detailed description of the feature and the issue it resolves.
   - Assign at least two team members as reviewers.

2. **Review Guidelines**:
   - Ensure the code follows the coding standards.
   - Check for potential bugs, security issues, and optimization.
   - Review the impact of changes on other parts of the system.

3. **Approval and Feedback**:
   - Reviewers provide feedback or approve the PR.
   - Developer addresses any requested changes and updates the PR.

4. **Merging**:
   - After approval, the developer merges the feature branch into `develop` (via Git Flow feature finish).
   - Ensure there are no conflicts, and if there are, resolve them before merging.

## 5. **Release Process**

1. **Preparing a Release**:
   - When the `develop` branch is stable and ready for release, create a release branch using Git Flow.
   ```bash
   git flow release start x.x.x
   - After approval, the developer merges the feature branch into `develop`.
   - Ensure there are no conflicts, and if there are, resolve them before merging.

## 4. **Release Process**

1. **Preparing a Release**:
   - When the `develop` branch is stable and ready for release, create a release branch.
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b release/x.x.x
   ```

2. **Testing**:
   - The release branch is thoroughly tested, and any issues are fixed within the release branch.

3. **Finishing a Release**:
   - Once the release is ready, finish it using Git Flow, which merges the release into `main` and `develop` and tags it with the version number.
   ```bash
   git flow release finish x.x.x
   ```

4. **Push Changes and Tags**:
   ```bash
   git push origin main --tags
   git push origin develop
   ```

5. **Clean Up**:
   - After the release, Git Flow automatically deletes the release branch.

## 6. **Hotfix Workflow**

1. **Creating a Hotfix Branch**:
   - When a critical issue arises in production, create a hotfix branch from `main` using Git Flow.
   ```bash
   git flow hotfix start issue-description
3. **Merging**:
   - Once the release is ready, it is merged into `main` and tagged with the version number.
   ```bash
   git checkout main
   git pull origin main
   git merge release/x.x.x
   git tag -a x.x.x -m "Version x.x.x"
   git push origin main --tags
   ```
   - Merge the release back into `develop`.
   ```bash
   git checkout develop
   git merge release/x.x.x
   ```

4. **Clean Up**:
   - After the release, the release branch is deleted.

## 5. **Hotfix Workflow**

1. **Creating a Hotfix Branch**:
   - When a critical issue arises in production, create a hotfix branch from `main`.
   ```bash
   git checkout main
   git pull origin main
   git checkout -b hotfix/issue-description
   ```

2. **Development**: Fix the issue and push changes to the hotfix branch.

3. **Code Review**: Open a PR for the hotfix branch and follow the usual review process.

4. **Finishing a Hotfix**:
   - After approval, finish the hotfix using Git Flow, which merges it into both `main` and `develop`.
   ```bash
   git flow hotfix finish issue-description
   ```

5. **Push Changes and Tags**:
   ```bash
   git push origin main --tags
   git push origin develop
   ```

4. **Merging**:
   - After approval, merge the hotfix into both `main` and `develop`.

5. **Tagging**: After merging into `main`, tag the hotfix with the new version number and push the tag.
