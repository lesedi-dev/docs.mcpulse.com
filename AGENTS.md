# Documentation project instructions

## About this project

- This is the MCPulse documentation site, built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Run `mint dev` to preview locally
- Run `mint broken-links` to check links

## Sources of truth

Nothing here should be written from memory. The product it documents lives in
four places, and every number, default and threshold on these pages came from
one of them:

| Source | What it settles |
|---|---|
| `mcpulse/CLAUDE.md` | The product spec, the data model, and the reasoning behind both |
| `mcpulse/apps/api/src/services/` | Every metric, every threshold, every rule |
| `mcpulse/apps/dashboard/src/` | What each screen actually shows |
| `mcpulse-sdk/src/` | The wire format, the options, and the buffering behaviour |

When a threshold moves in `services/insights.ts` or an option changes in
`options.ts`, the page quoting it is stale. Prefer naming the file over
restating a constant where the constant is likely to move.

## Terminology

- An **MCP** is one tracked server. It is what the dashboard lists and what a
  key belongs to — never "project", never "workspace".
- A **tool** is one registered MCP tool on that server.
- A **call** is one `tools/call`. A **session** is one client connection, which
  may hold many calls.
- **Outcome** is one of `ok`, `bad_args`, `tool_error`, `crashed`. Use those
  exact spellings; "failure" is not an outcome.
- **First-call success** — never "success rate", which conflates it with `ok`.
- **The nightly pass** is the 02:00 UTC job. Say "nightly pass", not "cron".
- Say **member**, **admin**, **owner** for roles, matching the API.

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, tool names, and outcomes
- Every metric page says what the number is, how it is computed, and what to do
  when it looks wrong. A metric page without the third part is unfinished.

## Content boundaries

- Never document a way to recover a raw API key. There isn't one, and implying
  there is undermines the thing that makes keys safe.
- Never suggest the SDK can be configured to send arguments or results. It
  cannot, deliberately, and that guarantee is only worth something if the docs
  never hint at an escape hatch.
- Don't document Supabase internals, RLS policies, or the service-role key.
  Those are ours, not the customer's.
