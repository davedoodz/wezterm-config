<pre>
   ┌──┐ ┌──┐ ┌──┐        _     __        _
   │▓▓│ │  │ │▓▓│       | |__ / _|_   _ | | __
   └──┘ └──┘ └──┘       | '_ \| |_| | | || |/ /
    W     E     Z       | |_) |  _| |_| ||   <
   ╰──────┬──────╯      |_.__/|_|  \__, ||_|\_\
          │                        |___/
       [ term ]
</pre>

# wezterm-config

A cross-platform WezTerm configuration that keeps one consistent key map on both Windows and macOS.

## What it is

WezTerm's default key bindings differ slightly depending on platform conventions, and a config written for one OS doesn't always translate cleanly to the other. This repo resolves that: a single `.wezterm.lua` that detects the host platform at load time and adapts only the handful of commands that are genuinely machine-specific — opening the config file in the right editor, and launching a login shell. Everything else — tab navigation, splits, copy mode, search — stays identical across both platforms.

The `reference/` folder keeps the original, unmodified Windows key-map export alongside the portable config, so it's easy to diff the two and confirm nothing was lost in translation.

## Highlights

- **One key map, two platforms** — `SUPER` resolves to the Windows key on Windows and Command on macOS; the rest of the bindings are shared.
- **Platform-aware launch commands** — `Cmd+,` / the equivalent opens the active config in the system's default editor; a second shortcut opens a login shell.
- **Full tab, pane, and copy-mode coverage** — tab activation, splits, pane zoom, and a complete copy-mode / search-mode key set (powered by `wezterm.action`).
- **Reference export preserved as-is** — `reference/windows-key-map.lua` keeps WezTerm's resolved default bindings exactly as exported, favoring behavioral continuity over a trimmed-down rewrite.
- **No secrets** — no credentials, tokens, or private keys are stored in this repo.

## Stack

Lua, using the `wezterm` config API (`wezterm.action`, `wezterm.target_triple` for platform detection).

## Install on macOS

```sh
git clone https://github.com/davedoodz/wezterm-config.git ~/Projects/wezterm-config
# back up any existing ~/.wezterm.lua first, then:
ln -s ~/Projects/wezterm-config/.wezterm.lua ~/.wezterm.lua
```

WezTerm reloads automatically when the linked file changes, so future `git pull` updates apply without another copy step.

## Install on Windows

```powershell
Copy-Item .wezterm.lua "$HOME\.wezterm.lua"
```

## Validate changes

```sh
wezterm --config-file .wezterm.lua show-keys --lua
```

If this prints the resolved key map without error, WezTerm accepted the configuration.

## Map

```text
.
├── .wezterm.lua                  # installable, cross-platform config
└── reference/
    └── windows-key-map.lua       # original Windows export, kept for comparison
```
