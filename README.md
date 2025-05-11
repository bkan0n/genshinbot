# genshinbot

A Discord bot built with Python, utilizing containerization for deployment and GitHub Actions for CI/CD.

## Prerequisites

- Docker and Docker Compose
- A Discord Bot Token
- Access to a server for deployment
- GitHub account with repository access
- Doppler account (for secrets management)

## Environment Variables and Secrets

### Discord Bot Token
The bot requires a Discord Bot Token to function. To obtain one:
1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create a new application
3. Navigate to the "Bot" section
4. Create a bot and copy the token

### GitHub Actions Secrets
The following secrets need to be configured in your Doppler project so it syncs with your GitHub repository secrets for deployment:

| Secret Name | Description | Example |
|------------|-------------|----------|
| `SERVER_HOST_IP` | IP address of the deployment server | `123.456.789.0` |
| `SERVER_HOST_USER` | SSH user for the deployment server | `deploy-user` |
| `SERVER_HOST_SSH_PRIVATE_KEY` | SSH private key for server authentication | `-----BEGIN RSA PRIVATE KEY-----\n...` |
| `SERVER_REPO_LOCATION` | Path where the repo will be cloned on the server | `/opt/discord-bot` |
| `REPO_BRANCH` | Branch to deploy (typically main or production) | `main` |
| `SERVER_HOST_GITHUB_PAT` | GitHub Personal Access Token for repository access | `ghp_xxxxxxxxxxxx` |
| `DOPPLER_SERVICE_TOKEN` | Doppler token for secrets management | `dp.st.xxxxxxxxxxxx` |

## Local Development

1. Clone the repository:
```bash
git clone [https://github.com/yourusername/repo-name.git](https://github.com/yourusername/repo-name.git)
``` 

2. Create a `.env` file in the root directory:
```bash
env TOKEN=your_discord_bot_token
``` 

3. Run the bot using Docker Compose:
```bash
docker compose up --build
``` 

## Code Style and Formatting

This project uses [Ruff](https://github.com/astral-sh/ruff) for code checking and formatting. Before submitting any pull request:

1. Install Ruff:
```bash
pip install ruff
``` 

2. Run Ruff check:
```bash
ruff check .
``` 

3. Run Ruff format:
```bash
ruff format .
``` 

All pull requests must pass Ruff checks before they can be merged. The GitHub Actions workflow will automatically verify this.

## Deployment Process

The project uses GitHub Actions for automated deployment. Here's how it works:

1. Create a Pull Request with your changes
2. GitHub Actions will run automated checks including Ruff
3. All checks must pass before merging is allowed
4. Upon merging to the main branch, the deployment workflow:
   - Builds the Docker image
   - Connects to the deployment server via SSH
   - Updates the repository
   - Rebuilds and restarts the Docker containers

### Deployment Requirements

1. The deployment server must have:
   - Docker installed
   - Docker Compose installed
   - Git installed
   - SSH access configured

2. Proper SSH key configuration:
   - Generate an SSH key pair for deployment
   - Add the public key to the server's `authorized_keys`
   - Add the private key to GitHub Secrets as `SERVER_HOST_SSH_PRIVATE_KEY`

## Security Notes

- Never commit sensitive information or tokens to the repository
- Always use environment variables for sensitive data
- Regularly rotate SSH keys and access tokens
- Keep the deployment server's software updated
- Monitor server and bot logs for unusual activity

## Contributing

1. Fork the repository
2. Create a new branch for your feature
3. Make your changes
4. Ensure code passes Ruff checks and formatting
5. Submit a Pull Request
6. Ensure all checks pass before requesting review

## License

This project is licensed under the MIT License.
```
MIT License
Copyright (c) 2025 Ty Lovejoy
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
``` 

## Support

For issues and feature requests, please use the GitHub Issues section of this repository.

