# claude-lsp-servers

LSP plugins for Claude Code. Workaround for [#15148](https://github.com/anthropics/claude-code/issues/15148).

## Setup

### 1. Enable LSP tool

Add to your shell profile (`~/.zshrc`, `~/.bashrc`, etc.) and restart your shell:

```bash
export ENABLE_LSP_TOOL=1
```

### 2. Add marketplace

```bash
claude plugin marketplace add CrisRPia/claude-lsp-servers
```

### 3. Install a plugin

```bash
claude plugin install basedpyright-lsp@claude-lsp-servers
```

### 4. Restart Claude Code

## Available plugins

### basedpyright-lsp

Python type checking via [basedpyright](https://github.com/DetachHead/basedpyright). [Installation options](https://docs.basedpyright.com/latest/installation/command-line-and-language-server/).

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`, `goToImplementation`, `incomingCalls`, `outgoingCalls`.

## Adding a new LSP

1. Create `plugins/<name>/.lsp.json`:

```json
{
  "<language>": {
    "command": "<language-server-binary>",
    "args": ["--stdio"],
    "extensionToLanguage": {
      ".<ext>": "<language>"
    }
  }
}
```

2. Create `plugins/<name>/.claude-plugin/plugin.json`:

```json
{
  "name": "<name>",
  "version": "1.0.0",
  "description": "<description>"
}
```

3. Add an entry to `.claude-plugin/marketplace.json` under `plugins`.
