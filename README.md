# SODL — releases

**Understand your service in five minutes.**

No framework. No annotations. No code changes.

Point SODL at your contracts. It builds a semantic model, shows how your system
behaves, writes an initial verification suite, and — when connected to a
deployment — proves whether reality matches the declaration.

> SODL understands your service before it writes a single test.

This repository distributes **binaries and installers only** — it carries no
source. Each release is built from a private source repository, and the release
notes name the exact source commit that produced it.

---

## Install

No account, no token, no GitHub CLI. The script detects your platform, verifies
the download against `SHA256SUMS`, installs into a user directory (no admin
rights needed), and prints the `PATH` line to add if one is missing.

**macOS / Linux**

```sh
curl -fsSL https://github.com/rajsinghsisodia/sodl-releases/releases/latest/download/install.sh | sh
```

**Windows (PowerShell)**

```powershell
irm https://github.com/rajsinghsisodia/sodl-releases/releases/latest/download/install.ps1 | iex
```

Then:

```sh
sodl version
```

Manual installation, pinning a version, and uninstalling are all in
**[INSTALL.md](INSTALL.md)**.

### Verifying a download yourself

Every release ships `SHA256SUMS`, covering every archive in it:

```sh
curl -fsSLO https://github.com/rajsinghsisodia/sodl-releases/releases/latest/download/SHA256SUMS
curl -fsSLO https://github.com/rajsinghsisodia/sodl-releases/releases/latest/download/sodl-<version>-<platform>.zip
sha256sum -c SHA256SUMS --ignore-missing
```

The installers already do this. The commands above are for when you want to
check it with your own hands.

---

## Two promises

**Promise A — unconditional.** Give SODL your contracts (gRPC protos, OpenAPI
documents, or a live reflection endpoint) and it shows you your system:
entities, lifecycles, relationships, state machines — drawn automatically, with
the things you did not know surfaced as insights. Five minutes. No credentials,
no deployment, no running services.

**Promise B — conditional.** Point it at a deployment (endpoint + credentials)
and it tells you whether reality matches what you declared — with an evidence
record behind every claim, a report page you can hand to anyone, an `explain`
that walks any failure back to the observations it rests on, and a
behavior-conformance overlay marking where the system does things its contract
does not admit.

---

## First five minutes

**With an AI agent (fastest).** Paste **[ADOPT.md](ADOPT.md)** into Claude Code,
Codex, or any MCP-capable agent opened in your service's repository. The agent
installs SODL, registers its MCP server, and follows SODL's own built-in
playbook from there. **[sample-session.md](sample-session.md)** shows what that
conversation actually looks like.

**Without an agent.**

```sh
sodl init         # writes sodl.yaml — points at your contracts
sodl analyze      # what SODL understood, and what it could not — it says so
sodl model -open  # your system, drawn
```

Once you have scenarios and a deployment:

```sh
sodl check        # is the suite valid against the contract?
sodl run          # execute it, and write an evidence record
sodl report -open # the attestation page
```

`check` and `run` default to the project's `scenarios/` directory, so they take
no arguments in the common case.

---

## What is in a release

| Asset | What it is |
| --- | --- |
| `sodl-<version>-<platform>.zip` | the `sodl` binary, plus `install.adoc` and `quickstart.adoc` |
| `sodl-vscode-<version>.vsix` | the VS Code extension — completion, hover, go-to-definition, signature help, and live diagnostics for `.sodl` files |
| `install.sh`, `install.ps1` | the installers the one-liners above invoke |
| `SHA256SUMS` | checksums for every archive in the release |
| `VERSION` | the version string on its own, for scripting |
| `README.md`, `INSTALL.md`, `ADOPT.md`, `sample-session.md` | the documents in this repository, attached so a downloaded kit is self-contained |

Platforms: `linux-amd64`, `darwin-amd64`, `darwin-arm64`, `windows-amd64`.

---

## Documentation

| Document | Read it for |
| --- | --- |
| **[INSTALL.md](INSTALL.md)** | installing, pinning a version, installing without the script, uninstalling |
| **[ADOPT.md](ADOPT.md)** | the bootstrap prompt to paste into an AI agent |
| **[sample-session.md](sample-session.md)** | what a first agent session looks like, end to end |

The binary's archive also carries `quickstart.adoc` — the five-minute path — and
`install.adoc`.

`sodl --help` lists every command; `sodl <command> -h` prints the usage, flags,
and exit codes for one.

The full manual (the authoring guide, the practices chapters, and the CLI,
format, and CI-integration references) lives with the source and is not
published here yet. Ask if you want a copy.

---

## Versions

Releases are named `0.1.0-internal.<n>` while SODL is in internal trials. **A
version number is never reused** — if you were handed `internal.34`, that build
is `internal.34` forever, and the release notes name the source commit it was
built from.

`latest` always resolves to the newest release, which is what the install
one-liners use. To pin a version, replace `latest/download` with
`download/v<version>` in any URL on this page.

---

## Reporting something

A defect, or a claim SODL made that you could not verify, is the most useful
thing you can send back. Include:

- the output of `sodl version`,
- the command you ran and what you expected instead,
- the run record from `.sodl/runs/` if there is one — it is the evidence, and it
  is what makes a report actionable.
