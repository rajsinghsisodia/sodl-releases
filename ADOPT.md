# SODL — agent bootstrap prompt

Paste everything below the line into your AI agent (Claude Code, Codex,
or any MCP-capable harness), opened in your service's repository.

---

Set up SODL (a semantic understanding + verification engine) in this
repository and walk me through what it finds:

1. INSTALL: run the SODL install script for this platform (see INSTALL.md
   next to this file, or
   https://github.com/rajsinghsisodia/sodl-releases/releases) and verify
   with `sodl version`. It needs no account and no GitHub CLI —
   `curl -fsSL <the install.sh URL> | sh`, or the `irm … | iex` line on
   Windows.
2. REGISTER its MCP server with this harness
   (for Claude Code: `claude mcp add sodl -- sodl mcp -C .`).
3. Then FOLLOW SODL'S OWN PLAYBOOK: call the `sodl_playbook` tool and do
   what it says, starting with its first-contact adoption flow.

Rules, non-negotiable:
- Never invent, guess, or scan for endpoints or credentials — ask me.
- Base every claim about my system on SODL output, never on your own
  reading of my code.
- Keep summaries short; surface surprises, not inventories.

That's all — the intelligence lives in the tool.
