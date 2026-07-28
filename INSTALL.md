# Installing SODL

One command. No account, no token, no extra tooling. The script detects
your platform, verifies the download against SHA256SUMS, installs to a
user directory (no admin rights), and prints the PATH line to add if
needed.

**Mac / Linux**

```
curl -fsSL https://github.com/rajsinghsisodia/sodl-releases/releases/latest/download/install.sh | sh
```

**Windows (PowerShell)**

```
irm https://github.com/rajsinghsisodia/sodl-releases/releases/latest/download/install.ps1 | iex
```

Verify: `sodl version`

Pin a version with `SODL_VERSION` (`$env:SODL_VERSION` on Windows) — it
maps to the release tag `v<version>`, and the installer then fetches from
`…/releases/download/v<version>/` instead of `…/releases/latest/download/`.

> `sodl-releases` carries binaries and installers only — the source
> repository is private and separate. You do not need access to it.

## Manual install

Browse https://github.com/rajsinghsisodia/sodl-releases/releases, or pull
your platform's zip straight down:

```
BASE=https://github.com/rajsinghsisodia/sodl-releases/releases/latest/download
V=$(curl -fsSL $BASE/VERSION)
curl -fLO $BASE/sodl-$V-linux-amd64.zip     # or your platform, from the table
curl -fLO $BASE/SHA256SUMS
```

| You have | Take |
|---|---|
| Windows | `sodl-<version>-windows-amd64.zip` |
| Mac, Apple Silicon | `sodl-<version>-darwin-arm64.zip` |
| Mac, Intel | `sodl-<version>-darwin-amd64.zip` |
| Linux | `sodl-<version>-linux-amd64.zip` |

Unzip, put `sodl` (or `sodl.exe`) on your PATH.

**Mac only** — the binary is unsigned (an internal build); un-quarantine
it once: `xattr -d com.apple.quarantine sodl && chmod +x sodl`.
**Windows** — SmartScreen may warn on a downloaded exe; "More info → Run
anyway", or use the PowerShell one-liner above (scripts install without
the mark-of-the-web on the binary).

## Other download paths (you almost certainly don't need these)

**Through the GitHub CLI.** If you already have `gh` authenticated, set
`SODL_USE_GH=1` and the installer downloads through it instead of plain
HTTP — useful if you are hitting anonymous rate limits, or if you have
been pointed at a release in a private repo (`SODL_REPO=<owner>/<repo>`):

```
gh release download --repo rajsinghsisodia/sodl-releases --pattern install.sh --output - | SODL_USE_GH=1 sh
```

**From somewhere else entirely.** `SODL_BASE_URL` overrides the download
home with any host that serves the release files by name — object
storage, an internal mirror, a local file server. Set it and the
installer never touches GitHub:

```
SODL_BASE_URL=https://files.example.internal/sodl sh install.sh
```

## VS Code (optional, recommended)

Install the bundled `sodl-vscode-<version>.vsix`: Extensions panel → `…`
→ *Install from VSIX* (or `code --install-extension <file>.vsix`). You
get diagnostics-as-you-type, hover provenance, autocomplete, and a
"▶ Run scenario" button. On Mac/Linux the extension uses the `sodl` on
your PATH.

## AI agent (optional, the fastest path)

`sodl mcp` is a Model Context Protocol server. Register it and the agent
learns SODL from the tool itself:

- Claude Code: `claude mcp add sodl -- sodl mcp -C .`
- Other harnesses: add a stdio MCP server with command `sodl`, args
  `["mcp", "-C", "<your repo>"]`.

Then just ask: *"Understand my service."*
