# WezTerm configuration

Portable backup of David's current WezTerm key bindings, prepared for moving from Windows to macOS.

## What is included

- `.wezterm.lua` — the installable cross-platform configuration.
- `reference/windows-key-map.lua` — the original Windows key-map export, preserved for comparison.

The configuration keeps the current shortcuts and adapts the two machine-specific commands:

- `Cmd+,` opens the active config in the platform's text editor.
- `Ctrl+A` opens OMP through PowerShell on Windows or a login Zsh shell on macOS.

`SUPER` means the Windows key on Windows and Command on macOS.

## Install on a Mac

1. Install [WezTerm](https://wezterm.org/installation.html).
2. Install OMP separately if you want the `Ctrl+A` shortcut to work.
3. Clone this repository:

   ```sh
   git clone https://github.com/davedoodz/wezterm-config.git ~/Projects/wezterm-config
   ```

4. If `~/.wezterm.lua` already exists, inspect and preserve it before continuing.
5. Link this repository's config into the location WezTerm reads:

   ```sh
   ln -s ~/Projects/wezterm-config/.wezterm.lua ~/.wezterm.lua
   ```

6. Open WezTerm. It automatically reloads the configuration when the file changes.

A symbolic link is a pointer to the repository file, so future `git pull` updates apply without another copy step.

## Install on Windows

From PowerShell:

```powershell
Copy-Item .wezterm.lua "$HOME\.wezterm.lua"
```

## Validate changes

With WezTerm installed:

```sh
wezterm --config-file .wezterm.lua show-keys --lua
```

If the command prints the resolved key map without an error, WezTerm accepted the configuration.

## Notes

- No credentials, tokens, or private keys are stored here.
- The reference export intentionally includes WezTerm's resolved default bindings as they existed on Windows in August 2026. The installable config therefore favors exact behavioral continuity over a minimal hand-written shortcut list.
