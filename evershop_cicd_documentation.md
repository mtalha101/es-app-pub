
# CI/CD Workflows Documentation for Evershop Flutter Project

This document provides an overview of the Continuous Integration/Continuous Deployment (CI/CD) workflows for your Flutter project hosted on GitHub. Each workflow is manually triggered via `workflow_dispatch` and is designed to streamline the process of building, testing, and deploying your app across different environments.

## Prerequisites
- Access to the GitHub repository.
- Proper environment secrets and credentials are set in GitHub Actions for Firebase and Apple Distribution (Fastlane).
- Understanding of GitHub Actions and Fastlane for managing mobile app deployments.

## Common Workflow Dispatch Instructions
All workflows can be manually triggered via the GitHub Actions tab:
1. Go to your GitHub repository.
2. Click on the **Actions** tab.
3. Select the desired workflow from the list.
4. Click on **Run workflow** in the right corner, and choose the appropriate branch or inputs if necessary.
5. Confirm the workflow run.

## Workflow Overview

### 1. `android-deploy-dev.yml`: Build and Deploy Android Staging Flutter App to Firebase App Distribution

**Use Case:**
This workflow is used to build and deploy the Android Staging version of the Flutter app (with the app ID `ai.evershop.app.dev`) to Firebase App Distribution. This workflow is mainly used for testing and internal feedback.

**Steps:**
- Pulls the latest code from the repository.
- Builds the APK for the staging environment.
- Uploads the APK to Firebase App Distribution.
- Notifies testers about the new release.
  
### Note:
For Android, please remember to manually increment the version number in the `build.gradle` file before pushing the code.

**Usage:**
Run this workflow when you need to deploy a new staging version of the Android app for testing purposes.

### 2. `android-deploy-prod.yaml`: Build and Deploy Android Production Flutter App to Firebase App Distribution

**Use Case:**
This workflow is used to build and deploy the Android Production version of the Flutter app (with the app ID `ai.evershop.app`) to Firebase App Distribution. This is helpful for internal team members before releasing the app to the Play Store.

**Steps:**
- Pulls the latest production code from the repository.
- Builds the APK for production.
- Uploads the APK to Firebase App Distribution.
- Notifies internal users about the new production build.

### Note:
For Android, please remember to manually increment the version number in the `build.gradle` file before pushing the code.


**Usage:**
Run this workflow before pushing to production when you want to share the build internally for final checks.

### 3. `android-release-prod-to-playstore.yaml`: Build and Deploy Android Production Flutter App to Google Play Store

**Use Case:**
This workflow automates the process of building and deploying the Android Production Flutter app to the Google Play Store. It finalizes the production build and pushes it live to users.

**Steps:**
- Pulls the latest production code from the repository.
- Builds the APK or AAB for production.
- Uploads the app bundle to Google Play Store.
- Optionally notifies the team once the release is complete.

### Note:
For Android, please remember to manually increment the version number in the `build.gradle` file before pushing the code.


**Usage:**
Run this workflow when you are ready to push the final production build to the Google Play Store for users.

### 4. `.ios-fastlane_dev.yaml`: Apple Release for Development

**Use Case:**
This workflow is used to build and deploy the iOS Staging version of the app (with the app ID `ai.evershop.app.dev`) using Fastlane. It pushes the app to TestFlight for internal testing.

**Steps:**
- Pulls the latest staging code from the repository.
- Uses Fastlane to build the iOS app for the staging environment.
- Uploads the app to TestFlight.
- Notifies internal testers once the build is available.

**Usage:**
Run this workflow when you need to deploy the staging version of the iOS app to TestFlight for internal testing.

### 5. `ios-fastlane_prod.yaml`: Apple Release for Production

**Use Case:**
This workflow is used to build and deploy the iOS Production version of the app (with the app ID `ai.evershop.app`) using Fastlane. It pushes the app to TestFlight or directly to the App Store.

**Steps:**
- Pulls the latest production code from the repository.
- Uses Fastlane to build the iOS app for production.
- Uploads the app to TestFlight or directly to the App Store.
- Optionally notifies the team once the release is complete.

**Usage:**
Run this workflow when you are ready to release the final production version of the iOS app to TestFlight or the App Store.

## Notes:
- Ensure that all required environment variables and credentials (like Firebase tokens, Fastlane credentials, etc.) are correctly set up in the GitHub repository secrets.
- Be cautious when deploying to production (Play Store/App Store) to ensure all testing is complete and no bugs are present.
