# tenebaur

Pacman repository for FynxLabs/Tenebrux packages, hosted on GitHub Pages.
Serves pre-built packages so installs and updates never depend on the AUR at
install time or a single third-party server.

## Usage

Add to `/etc/pacman.conf`:

```ini
[tenebaur]
SigLevel = Optional TrustAll
Server = https://fynxlabs.github.io/aur/$arch/
```

Then:

```bash
sudo pacman -Sy
sudo pacman -S dusk umbra ember rwr nody-greeter shikai-theme
```

## What's in the repo

| Package | Source | Why it's here |
|---------|--------|---------------|
| `dusk` | github.com/fynxlabs/dusk releases | Panel — no AUR package |
| `umbra` | github.com/fynxlabs/umbra releases | Installer — no AUR package |
| `ember` | github.com/fynxlabs/ember releases | Clipboard/notifications — no AUR package |
| `rwr` | github.com/fynxlabs/rwr releases | Config management — no AUR package |
| `nody-greeter` | AUR (rebuilt) | LightDM greeter — pre-built so installs don't need yay/AUR at install time |
| `shikai-theme` | AUR (rebuilt) | Greeter theme — same reason |
| `xlibre-*` | x11libre.net (mirrored) | X server — mirrored so x11libre.net being down doesn't break Tenebrux |

## Updating the repo

```bash
mise install          # install tools
mise run fetch        # download FynxLabs release packages
mise run fetch-aur    # build AUR packages (nody-greeter, shikai-theme)
mise run mirror-xlibre # mirror xlibre X server packages
mise run build        # regenerate repo database (repo-add)
mise run publish      # push to gh-pages branch (live site updates)
# Or all at once:
mise run update
```

## CI

The `.github/workflows/update.yml` workflow rebuilds the repo:
- **On schedule** (daily at 06:00 UTC) — catches new releases automatically
- **On repository_dispatch** — triggered by dusk/umbra/ember release workflows
- **Manually** — via GitHub Actions "Run workflow" button

## Architecture support

- `x86_64` — primary, fully supported
- `aarch64` — scaffolded; packages added as arm64 releases become available

## License

MIT — see [LICENSE](LICENSE).
