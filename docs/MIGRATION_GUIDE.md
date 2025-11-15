# Migration Guide for Pending Features

This guide summarizes the pending changes from currently open pull requests and provides notes to help adoption and integration.

## PR #53 — 【Feat】Automate Docker Image Builds with GitHub Actions

- Summary of changes:
  - Adds a new GitHub Actions workflow to automate Docker image builds on push events.
  - Based on standard Docker build templates for reliability and maintainability.
  - Ensures a fresh Docker image is built whenever the branch is updated.
- New configuration or environment variables:
  - None explicitly specified in the PR description.
  - If the workflow pushes images to a registry, you may need repository secrets (e.g., REGISTRY, REGISTRY_USERNAME, REGISTRY_TOKEN) — verify in the workflow file.
- Installation/usage instructions:
  - No local installation needed; CI runs automatically on push.
  - To test locally: push a commit to the branch and check the Actions tab for a successful Docker build.
  - If publishing images, configure repository secrets for your registry.

## PR #52 — feat: add shell completions (bash, zsh, fish)

- Summary of changes:
  - Introduces static completion scripts for Bash, Zsh, and Fish under `shell-completions/`:
    - `claude-completions.bash`
    - `claude-completions.zsh`
    - `claude-completions.fish`
  - Upstream integrated completions via the binary are not available; scripts provide tab-autocomplete via shell sourcing.
- New configuration or environment variables:
  - None required.
- Installation/usage instructions:
  - Bash:
    - Add to `~/.bashrc` or `~/.bash_profile`:
      - `source /path/to/repo/shell-completions/claude-completions.bash`
  - Zsh:
    - Add to `~/.zshrc`:
      - `source /path/to/repo/shell-completions/claude-completions.zsh`
  - Fish:
    - Copy `claude-completions.fish` to `~/.config/fish/completions/claude.fish` or source in `config.fish`.
  - After sourcing, restart your shell or run `source ~/.zshrc` / `source ~/.bashrc` / `source ~/.config/fish/config.fish`.
  - Note: Terminal themes with aggressive prompt/ANSI handling (e.g., PowerLevel10k) may affect CLI behavior; see Issue #12 for related context.

## PR #51 — Enhance Statsig event logging in GitHub workflows

- Summary of changes:
  - Adds additional logging for issue management events in GitHub workflows (e.g., when issues are closed as duplicates, when duplicate comments are added).
  - Aligns with existing logging patterns for consistency.
- New configuration or environment variables:
  - None mentioned. If Statsig or analytics require secrets (e.g., API keys), ensure they are configured in repository secrets or workflow env.
- Installation/usage instructions:
  - No local changes required; CI workflows will log additional events after merge.
  - Review the Actions tab to verify new event logs appear as intended.
