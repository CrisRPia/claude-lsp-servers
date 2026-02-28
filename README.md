# claude-lsp-servers

LSP plugins for Claude Code. Workaround for [#15148](https://github.com/anthropics/claude-code/issues/15148).

## Prerequisites

```bash
export ENABLE_LSP_TOOL=1  # Add to shell profile
```

## Available plugins

### basedpyright-lsp

```bash
brew install basedpyright  # or: pip install basedpyright
claude plugin install basedpyright-lsp@claude-lsp-servers
```

## Install marketplace

```bash
claude plugin marketplace add CrisRPia/claude-lsp-servers
```

## Adding a new LSP

Create `plugins/<name>/.lsp.json` with the server config and add an entry to `.claude-plugin/marketplace.json`.
