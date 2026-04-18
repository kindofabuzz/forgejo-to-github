# forgejo-to-github

## Overview

**forgejo-to-github** is a Bash script designed to streamline the creation and synchronization of repositories between Forgejo and GitHub. This tool:
1. Automatically creates repositories on both Forgejo and GitHub.
2. Initializes version control locally with optional language templates.
3. Sets up mirroring between Forgejo and GitHub for seamless synchronization.

## Prerequisites

Before using the script, ensure you have the following:
- **Forgejo and GitHub Accounts**:
  - Forgejo Server URL and Forgejo user token with repository permissions.
  - GitHub user token with `repo` permissions.
- **Environment Variables**:
  - Add the following variables to your shell configuration (`~/.bashrc` or `~/.zshrc`):

```bash
export FORGEJO_URL="http://<forgejo-server-url>:<port>"
export FORGEJO_USER="<your-forgejo-username>"
export FORGEJO_TOKEN="<your-forgejo-personal-token>"
export GITHUB_USER="<your-github-username>"
export GITHUB_TOKEN="<your-github-personal-token>"
```

Make sure to reload your shell after editing the configuration:
```bash
source ~/.bashrc
```

## Usage

Execute the `git-create` script to create and initialize repositories:

```bash
./git-create [repository-name]
```

### Interactive Steps

The script guides you through the following steps interactively:
1. **Visibility Selection**: Choose whether the repository is `Private` or `Public`.
2. **Setup Language**:
   - `Go`: Initializes a Go project with `go mod init`.
   - `Python`: Creates a Python project with `uv init`.
   - `Bash`: Sets up a Bash script template.
   - `Exit`: Cancels the process.

3. **Mirroring**:
   - Mirrors changes from Forgejo to GitHub with automatic push synchronization.

### Example

#### Creating a Private Bash-Based Repository

1. Run the script:
   ```bash
   ./git-create my-private-repo
   ```
2. Select **Private** when prompted.
3. Choose **Bash** for the project language.
4. Follow on-screen instructions for initialization.

## Components & Features

### Visibility Selection
During the setup process, choose:
- `p` or `P`: For private repositories.
- Any other key: For public repositories.

### Repository Creation
The script creates repositories on:
- **GitHub** using its REST API.
- **Forgejo** using its API. Ensure the `FORGEJO_URL` is correct.

### Language Initialization
Automatically configures basic project templates:
- **Go**: Initializes `go.mod` and main function.
- **Python**: Sets up a Python script (`main.py`).
- **Bash**: Prepares a Bash script (`main.sh`) with execution permissions.

### Push Mirroring
Automatically configures push mirroring:
- Syncs changes from Forgejo to GitHub every 8 hours.
- Mirrors commits with the `forgejo` remote alias.

## Error Handling

### Missing Environment Variables
If required environment variables are unset, the script will terminate with:
```plaintext
Error: FORGEJO_TOKEN or GITHUB_TOKEN not found in environment.
```
Solution: Make sure all variables are properly set (review the **Prerequisites** section).

### Repository Already Exists
The script doesn't check if a repository already exists. Ensure the repository name is unique.

## Contributing

Feel free to submit issues or contribute to enhance the functionality of `forgejo-to-github`!

## License

This project is licensed under the MIT License.
