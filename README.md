# Copilot Instructions Repository

This repository manages the central `copilot-instructions.md` file used to provide custom instructions and guidelines to GitHub Copilot within various projects. It also includes a GitHub Actions workflow to automatically synchronize this file across multiple target repositories.

## Core Components

1.  **`copilot-instructions/copilot-instructions.md`**:
    *   This is the main file containing the detailed instructions for GitHub Copilot.
    *   It defines project standards, coding practices, security guidelines, documentation styles, and specific command behaviors.
    *   The workflow copies this file to the `.github/` directory of target repositories for Copilot to recognize it.

2.  **`sync-repos.txt`**:
    *   A simple text file listing all the target repositories (in `owner/repo` format) where the instructions should be synced.
    *   Each line contains one repository name. The workflow reads this file to determine which repositories to update.

2.  **`.github/workflows/sync-copilot-instructions.yml`**:
    *   A GitHub Actions workflow designed to keep the `copilot-instructions.md` file consistent across different repositories.
    *   **Trigger:** Runs automatically when changes are pushed to `copilot-instructions/copilot-instructions.md` on the `main` branch. It can also be triggered manually via `workflow_dispatch`.
    *   **Action:** Uses the `cloud-sky-ops/sync-files-multi-repo@v1.0.0-2` action to copy the updated instructions file from the `copilot-instructions/` directory to the `.github/` directory in all target repositories listed in `sync-repos.txt`.

## Setup & Configuration

1.  **Target Repositories:** The workflow uses the `cloud-sky-ops/sync-files-multi-repo` action which reads the list of target repositories from the `sync-repos.txt` file in the root of this repository. Add or remove repository names (in `owner/repo` format) from this file to control where the instructions are synced.

2.  **Personal Access Token (PAT):** The workflow requires a GitHub Personal Access Token (PAT) with the `repo` scope to push changes to the target repositories.
    *   Generate a PAT in your GitHub Developer settings.
    *   Add this PAT as a repository secret named `COPILOT_INSTRUCTIONS_SYNC_TOKEN` in the **Settings > Secrets and variables > Actions** section of *this* `copilot-instructions` repository.

3.  **File Mapping:** The workflow is configured to copy files from the `copilot-instructions/` directory in this repository to the `.github/` directory in target repositories, ensuring the instructions file ends up in the correct location for GitHub Copilot to recognize it.

## Usage

*   Modify the `copilot-instructions/copilot-instructions.md` file in this repository to update the guidelines.
*   Commit and push the changes to the `main` branch.
*   The GitHub Action will automatically run and sync the updated file to the configured target repositories.
*   You can also manually trigger the workflow from the "Actions" tab of this repository if needed.

## Contributing

Updates to the core instructions should be made directly in this repository's `copilot-instructions/copilot-instructions.md` file. Ensure changes align with the overall project goals and standards.

## License

[Specify your license here, e.g., MIT License]
