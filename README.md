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

Python type checking via [basedpyright](https://github.com/DetachHead/basedpyright).

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`, `goToImplementation`, `incomingCalls`, `outgoingCalls`.

### rust-analyzer-lsp

Rust intelligence via [rust-analyzer](https://github.com/rust-lang/rust-analyzer).

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`, `workspaceSymbol`, `goToImplementation`, `prepareCallHierarchy`, `incomingCalls`, `outgoingCalls`.

### typescript-lsp

TypeScript and JavaScript intelligence via [typescript-language-server](https://github.com/typescript-language-server/typescript-language-server).

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`, `workspaceSymbol`, `goToImplementation`, `prepareCallHierarchy`, `incomingCalls`, `outgoingCalls`.

### css-lsp

CSS, SCSS, and LESS intelligence via [vscode-css-languageservice](https://github.com/microsoft/vscode-css-languageservice).

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`.

### html-lsp

HTML intelligence via [vscode-html-languageservice](https://github.com/microsoft/vscode-html-languageservice).

Provides: `hover`, `documentSymbol`.

### json-lsp

JSON language server via [vscode-json-languageservice](https://github.com/microsoft/vscode-json-languageservice).

Provides: `hover`, `documentSymbol`.

### tombi-lsp

TOML formatting, linting, and intelligence via [tombi](https://github.com/tombi-toml/tombi).

Provides: `hover`, `documentSymbol`.

### yaml-lsp

YAML intelligence via [yaml-language-server](https://github.com/redhat-developer/yaml-language-server).

Provides: `hover`, `documentSymbol`.

### xml-lsp

XML intelligence via [LemMinX](https://github.com/eclipse/lemminx).

Provides: `hover`, `goToDefinition`, `documentSymbol`.

### bash-lsp

Bash/Shell scripting intelligence via [bash-language-server](https://github.com/bash-lsp/bash-lsp).

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`.

### lua-lsp

Lua intelligence via [lua-language-server](https://github.com/LuaLS/lua-language-server).

Provides: TODO

## Limitations

### LSPs that require dynamic capability registration

Claude Code's LSP client does not support `client/registerCapability`. Language servers that rely on dynamic registration (e.g. `tailwindcss-language-server`) will connect but fail to provide any features.

### Files without extensions

`extensionToLanguage` only matches by file extension. Files like `Dockerfile` that have no extension cannot be matched, so LSPs like `dockerfile-language-server` won't activate.

## Troubleshooting

### `Executable not found in $PATH`

The language server binary must be installed and available in your `$PATH`. If you use [Mason](https://github.com/williamboman/mason.nvim) in Neovim, add its bin directory to your shell profile:

```bash
export PATH="$HOME/.local/share/nvim/mason/bin:$PATH"
```

Otherwise, install the binary manually (see each plugin's homepage). If it works in your terminal but Claude Code can't find it, restart your shell after modifying `$PATH`.

### LSP seems enabled but doesn't work

Check for conflicting built-in LSPs by running `/plugin` in a Claude Code chat. If `pyright` appears (e.g. registered by the VS Code extension), uninstall it from the plugin UI — having both active causes conflicts.

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

## Credits

Inspired by [yungweng/claude-lsp-servers](https://github.com/yungweng/claude-lsp-servers).
