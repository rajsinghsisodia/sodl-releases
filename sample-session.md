# What a first session looks like

A real shape of the conversation after pasting [`ADOPT.md`](ADOPT.md)
into an MCP-capable agent in your service's repo. (Condensed; your
system's names will differ. Every claim the agent makes below traces to
SODL output — that's one of the rules the prompt sets.)

---

**You:** *(paste ADOPT.md)*

**Agent:** Installed `sodl 0.1.0-internal.21`. Registered the MCP server.
Following SODL's playbook — analyzing your contracts now.

Your system, as SODL derived it (model page opened in your browser —
the state machines are drawn from your protos, nothing else):

Things you may not know about your own system:
1. **Nothing ever reaches `CANCELLED`** — the Order lifecycle declares it,
   but no declared transition arrives there.
2. **`Job` declares states but no transition graph** — as declared,
   `RUNNING` is terminal.
3. **Three entities have no lifecycle at all** (`ApiKey`, `Webhook`,
   `AuditEntry`) — observable, never state-tracked.
4. **`Tenant` has 17 operations**, more than the next three entities
   combined.
5. **Two operations are not observable** — nothing in the contract lets
   anyone read back what they did.

Would you like to understand your system first, or verify a running
deployment?

---

**You:** Verify. Staging is at `staging.internal:9090`, admin password is
in `$STAGING_ADMIN_PW`.

**Agent:** Wrote `environments/staging.yaml` (credential rides the
environment variable, never a file). Authored a starter suite from the
coverage queue — 14 scenarios across your 5 entities; `sodl check` is
green; coverage says 31 of 34 operations exercised.

Running… **12 pass, 2 fail** — and the failures are findings, not test
bugs:

- `order_refund` — `INVALID_ARGUMENT: refund exceeds captured amount` on
  a value your own contract's example declares valid. *(report page +
  `sodl explain` walk attached)*
- `job_lifecycle` — the run's evidence shows `RUNNING → SUCCEEDED`, and
  the model page's behavior-conformance overlay now marks it
  **CONTRADICTED**: your contract admits no exit from `RUNNING`. Either
  the contract under-declares or the system misbehaves — that
  adjudication is yours; the evidence for both sides is in the record.

Everything above is reproducible: the run wrote an evidence record, and
`sodl report -open` renders it.

---

That's the whole product in one conversation: **understanding first,
insights you didn't have, then verification as proof — with evidence
behind every sentence.**
