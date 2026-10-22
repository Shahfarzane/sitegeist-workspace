# sitegeist workspace

The sitegeist fork and the two sibling repos it builds against, as submodules in the
layout the build expects (`sitegeist/../mini-lit`, `sitegeist/../pi-mono`).

| Folder | Repo | Branch | Based on |
|---|---|---|---|
| `sitegeist/` | [Shahfarzane/sitegeist](https://github.com/Shahfarzane/sitegeist) | `main` | 0xSero/sitegeist (fork of badlogic/sitegeist) |
| `mini-lit/` | [Shahfarzane/mini-lit](https://github.com/Shahfarzane/mini-lit) | `sitegeist` | badlogic/mini-lit `v0.2.1` |
| `pi-mono/` | [Shahfarzane/pi-mono](https://github.com/Shahfarzane/pi-mono) | `sitegeist` | earendil-works/pi `v0.60.0` |

All four repos are public. pi-mono must stay on v0.60.0: upstream main renamed the packages
to `@earendil-works/*` and dropped web-ui.

## Set up

```bash
git clone --recurse-submodules https://github.com/Shahfarzane/sitegeist-workspace.git
cd sitegeist-workspace/sitegeist
scripts/setup-siblings.sh
```

`setup-siblings.sh` installs every package, builds mini-lit, the pi-mono declarations and the
CLI. Build, release and bridge setup are in `sitegeist/README.md`.

## Changing a sibling

1. Edit in `mini-lit/` or `pi-mono/`, commit on `sitegeist` and push.
2. In `sitegeist/`, run `scripts/sibling-patches.sh export` and commit `patches/` (its
   pre-commit check fails while the patches and the forks differ).
3. Here, commit the moved submodule pointers: `git add mini-lit pi-mono sitegeist`.

The patches let a machine without the forks (CI) rebuild the siblings
from the public upstream tags.

To bring every submodule to the tip of its branch: `git submodule update --remote`, then
commit the pointers.
