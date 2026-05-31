# copilot-vsix-releases

Nightly builds of the GitHub Copilot Chat extension as a standalone VSIX, for use in [VSCodium](https://vscodium.com).

A GitHub Action checks every night for new [VS Code releases](https://github.com/microsoft/vscode/releases), builds the bundled `extensions/copilot` at that tag, and publishes the VSIX as a GitHub release.

## Install

1. Go to [Releases](../../releases) and download the VSIX matching your VSCodium version.

   VSCodium version → VS Code tag mapping: `1.121.03429` → `1.121.0` (drop the last segment).

2. Install:
   ```bash
   codium --install-extension copilot-chat-X.Y.Z.vsix
   ```

3. Sign in with your GitHub account when prompted. A [GitHub Copilot subscription](https://github.com/features/copilot) is required.

## How it works

The workflow (`build.yml`) runs nightly and:

1. Fetches the 20 most recent releases from `microsoft/vscode`
2. Compares against releases already published in this repo
3. For each new version: shallow-clones the VS Code repo at that tag, runs `npm install && npm run build` inside `extensions/copilot`, packages with `vsce`, and creates a GitHub release with the VSIX attached
