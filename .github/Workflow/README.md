Cheat Engine Windows Build & Release Workflow
This repository contains a GitHub Actions workflow to automatically compile Cheat Engine for Windows (32-bit and 64-bit) using Lazarus and publish a release whenever a version tag is pushed.
🚀 How It Works
The automated pipeline (.github/workflows/build-release.yml) consists of two main jobs:
 * Build (windows-latest):
   * Checks out your fork of the repository.
   * Sets up a pinned, stable version of Lazarus/Free Pascal (2.2.6).
   * Compiles both the 32-bit (Release 32-Bit) and 64-bit (Release 64-Bit) desktop application targets using lazbuild.
   * Uploads the resulting executables as workflow artifacts.
 * Release (ubuntu-latest):
   * Runs only when you push a version tag (e.g., v7.5.0).
   * Downloads the compiled .exe binaries.
   * Compresses them into a single archive (CheatEngine-Windows.zip).
   * Automatically generates release notes and publishes a new GitHub Release with the zip archive attached.
🛠️ Usage Instructions
1. Enable GitHub Actions
Ensure that GitHub Actions are enabled in your repository under Settings > Actions > General > Actions permissions (set to "Allow all actions and reusable workflows").
2. Triggering a Release
To cut an official release with binaries attached:
git tag v7.5.0
git push origin v7.5.0

3. Running Manual Builds
If you want to test the build process without creating a public release:
 * Navigate to the Actions tab in your GitHub repository.
 * Select the Build and Release Cheat Engine (Windows) workflow on the left sidebar.
 * Click Run workflow to generate and download the .exe files directly from the run summary.
⚠️ Notes & Limitations
 * User-Mode Only: This workflow builds the standard user-mode applications (cheatengine-i386.exe and cheatengine-x86_64.exe). It does not compile the kernel-mode driver (dbk64.sys) or DBVM, which require a specialized Windows Driver Kit (WDK) and an active code-signing certificate.
 * FPC Compatibility: The workflow is pinned to Lazarus 2.2.6 to guarantee compatibility with older project files. If you upgrade your fork to support newer Lazarus/FPC versions, you can adjust the lazarus-version parameter in the workflow file.
 * 
