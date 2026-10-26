# Scout for pi

This repository is the pi extension for Scout. It is public. It adds the
`scout_send`, `scout_ask`, `scout_who`, and `scout_work_update` tools and the
`/scout` command to pi.

## Where work goes

- The extension reaches the runtime through its local socket, with HTTP as the
  fallback. It uses the `@openscout/protocol` types and carries no runtime
  code.
- Behavior that every harness needs goes to the core repository,
  `openscout-app/scout`. Land it there first, then use it here.
- Behavior specific to pi goes here: the tools, the command, and the
  interface.

| Path | Holds |
| --- | --- |
| `index.ts` | The extension entry point |
| `tools/` | The four Scout tools |
| `broker/client.ts`, `runtime.ts`, `target.ts` | The runtime client and target resolution |
| `ui/` | The agent picker and message views |
| `config.ts` | Optional user configuration |
| `scripts/setup-host-mcp.mjs` | Registers `scout mcp` with Codex and Claude Code at install |
| `skills/scout-coordination.md` | The coordination skill |

## Rules

- The extension stays inert until the user invokes a Scout action.
- A runtime rejection must show as a clean error. It must not crash the
  extension.
- The install script must respect `PI_SCOUT_SKIP_HOST_MCP_SETUP=1`.
- Scout is for high-trust local developer use. Do not claim enterprise,
  compliance, or multi-tenant readiness.
- This repository is public. Do not commit local paths, host names,
  credentials, or private source.

## Checks

There is no test suite. Link your checkout as a pi extension, then run each
tool that you change against a local runtime.

## Commits and pull requests

- Commit subjects use gitmoji: `🐛 Show a runtime rejection as an error`.
- Do not add AI co-author trailers or "Generated with" lines.
- Push a branch to `openscout-app/pi-scout` and open a pull request into
  `main`.

<!-- scout:begin -->
## Scout

- Work for another agent, or on another machine, goes through Scout: `scout ask` (MCP `ask`).
- Another machine: `scout ask --on <host> --project <path on that host> --harness <claude|codex>`; `scout hosts` lists machines and their projects. Don't ssh in to launch agents.
- Syntax: `scout ask --help`, `scout help --detail`. Added by `scout setup agents-md`; `scout setup agents-md --remove` takes it out.
<!-- scout:end -->
