# Claude Code Dev Container Template

A Dev Container template for running [Claude Code](https://github.com/anthropics/claude-code) in an isolated, firewall-restricted Docker environment.

Based on the official [anthropics/claude-code `.devcontainer`](https://github.com/anthropics/claude-code/tree/main/.devcontainer).

## Features

- **Claude Code CLI** pre-installed and ready to use
- **Network firewall** via `iptables` + `ipset` — restricts outbound traffic to allowed hosts only (GitHub, npm, Anthropic API, VS Code Marketplace, etc.)
- **Persistent volumes** for Claude config and shell history across rebuilds
- **VS Code extensions** pre-configured: Claude Code, ESLint, Prettier, GitLens
- **zsh** as the default shell
- Runs as non-root `node` user

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [VS Code](https://code.visualstudio.com/) with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Usage

1. Clone this repository
2. Open in VS Code
3. When prompted, click **Reopen in Container** (or run `Dev Containers: Rebuild and Reopen in Container` from the Command Palette)
4. The container will build and the firewall will be initialized automatically

The [Claude Code Superpowers](https://claude.com/plugins/superpowers) plugin is automatically installed via `postCreateCommand`. It adds skills for test-driven development, systematic debugging, brainstorming, and more — guiding Claude through complex tasks step by step. Run `/using-superpowers` in Claude Code to get started.

## Firewall

The `init-firewall.sh` script runs as `postStartCommand` and sets up an allowlist-based firewall inside the container. Outbound connections are restricted to:

- GitHub (IP ranges from the GitHub meta API)
- `registry.npmjs.org`
- `api.anthropic.com`
- `marketplace.visualstudio.com`
- `vscode.blob.core.windows.net`
- `update.code.visualstudio.com`

This prevents Claude Code from making unintended outbound connections while still allowing necessary development workflows.

## License

[MIT](LICENSE)
