# espanso

Shared Espanso config: global options in `config/default.yml`, snippets in `match/`.

[Espanso](https://espanso.org/) must be installed first. Confirm the active config folder:

```bash
espanso path config
```

Stop Espanso before replacing or moving that folder (`espanso stop` or quit the tray app), then restart when done (`espanso restart`).

## Layout

| Path in this repo | Role |
| --- | --- |
| `config/default.yml` | Global behavior (shortcuts, backends, notifications) |
| `match/base.yml` | Default snippets |
| `match/*.yml` | Extra match sets |

## macOS

Default config directory:

```text
~/Library/Application Support/espanso
```

### Use this repo as your live config

**Option A — clone into the default location**

```bash
espanso stop
# optional: backup existing config
mv "$HOME/Library/Application Support/espanso" "$HOME/Library/Application Support/espanso.bak"
git clone <repo-url> "$HOME/Library/Application Support/espanso"
espanso restart
```

**Option B — clone elsewhere and symlink**

```bash
espanso stop
git clone <repo-url> ~/code/espanso-config
mv "$HOME/Library/Application Support/espanso" "$HOME/Library/Application Support/espanso.bak" 2>/dev/null || true
ln -s ~/code/espanso-config "$HOME/Library/Application Support/espanso"
espanso restart
```

If you already have this folder checked out (for example you opened it in an editor), you only need Espanso to use that path: ensure `espanso path config` points here, or symlink this directory to `~/Library/Application Support/espanso` as in option B.

## Windows

Default config directory:

```text
%APPDATA%\espanso
```

Example: `C:\Users\<you>\AppData\Roaming\espanso`

### Use this repo as your live config

In PowerShell:

```powershell
espanso stop
# optional: backup
Rename-Item -Path "$env:APPDATA\espanso" -NewName "espanso.bak" -ErrorAction SilentlyContinue
git clone <repo-url> "$env:APPDATA\espanso"
espanso restart
```

**Symlink from another checkout** (Developer Mode or elevated shell may be required):

```powershell
espanso stop
cmd /c mklink /D "%APPDATA%\espanso" "C:\path\to\espanso-config"
espanso restart
```

## Linux

Default config directory:

```text
$XDG_CONFIG_HOME/espanso
```

Usually `~/.config/espanso`.

### Use this repo as your live config

```bash
espanso stop
# optional: backup
mv ~/.config/espanso ~/.config/espanso.bak 2>/dev/null || true
git clone <repo-url> ~/.config/espanso
espanso restart
```

**Symlink from another checkout:**

```bash
espanso stop
git clone <repo-url> ~/code/espanso-config
rm -rf ~/.config/espanso
ln -s ~/code/espanso-config ~/.config/espanso
espanso restart
```

## After setup

- Edit matches with `espanso edit` or any text editor; reload is automatic unless disabled in config.
- Pull updates where you cloned: `git pull`, then `espanso restart` if something does not pick up.

Replace `<repo-url>` with this repository’s Git remote (HTTPS or SSH).