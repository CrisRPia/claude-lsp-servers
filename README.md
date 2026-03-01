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

### rust-analyzer-lsp

Rust intelligence via [rust-analyzer](https://github.com/rust-lang/rust-analyzer). Install via `rustup component add rust-analyzer`.

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`, `workspaceSymbol`, `goToImplementation`, `prepareCallHierarchy`, `incomingCalls`, `outgoingCalls`.

### typescript-lsp

TypeScript and JavaScript intelligence via [typescript-language-server](https://github.com/typescript-language-server/typescript-language-server). Install via `npm i -g typescript-language-server typescript`.

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`, `workspaceSymbol`, `goToImplementation`, `prepareCallHierarchy`, `incomingCalls`, `outgoingCalls`.

### css-lsp

CSS, SCSS, and LESS intelligence via [vscode-css-languageservice](https://github.com/microsoft/vscode-css-languageservice). Install via `npm i -g vscode-langservers-extracted`.

Provides: `hover`, `goToDefinition`, `findReferences`, `documentSymbol`.

### html-lsp

HTML intelligence via [vscode-html-languageservice](https://github.com/microsoft/vscode-html-languageservice). Install via `npm i -g vscode-langservers-extracted`.

Provides: `hover`, `documentSymbol`.

### json-lsp

JSON language server via [vscode-json-languageservice](https://github.com/microsoft/vscode-json-languageservice). Install via `npm i -g vscode-langservers-extracted`.

Provides: `hover`, `documentSymbol`.

### tombi-lsp

TOML formatting, linting, and intelligence via [tombi](https://github.com/tombi-toml/tombi). Install via `brew install tombi`, `npm install tombi`, or `pip install tombi`.

Provides: `hover`, `documentSymbol`.

### yaml-lsp

YAML intelligence via [yaml-language-server](https://github.com/redhat-developer/yaml-language-server). Install via `npm i -g yaml-language-server`.

Provides: `hover`, `documentSymbol`.

### xml-lsp

XML intelligence via [LemMinX](https://github.com/eclipse/lemminx). [Installation](https://github.com/eclipse/lemminx#getting-started).

Provides: TODO

## Troubleshooting

### `Executable not found in $PATH`

The language server binary must be installed and available in your `$PATH` in the shell you start Claude Code from. Verify with e.g. `basedpyright-langserver --version`. If it works in your terminal but Claude Code can't find it, restart your shell after modifying `$PATH`.

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
