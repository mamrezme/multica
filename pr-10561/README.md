# Screenshots for multica-ai/multica#10561

Evidence only. This branch is not meant to be merged.

- Source commit: `0e991727b` (`fix/autopilot-run-only-queue-offline-runtime`)
- Viewport 1440×900, light theme, headless Chromium (Playwright), web app via `pnpm dev:web`, Go server built from the same commit, local PostgreSQL 18.
- Data: a throwaway local workspace, a `run_only` autopilot "Daily job search" assigned to agent "Daily Reporter". Its runtime was registered and then taken offline through `/api/daemon/deregister`.

1. `01-first-run-now.png`: first "Run now" with the runtime offline. The run is `running` and its task is `queued`.
2. `02-second-run-now.png`: second "Run now". The run is skipped with `already_active`, and only one task is in the queue.
3. `03-skipped-reason.png`: the skipped run expanded, showing its reason.
4. `04-after-reconnect.png`: the daemon re-registered and claimed the queued task. The run is now `completed`. A fixture daemon drove the claim, start and complete calls the same way `scripts/dev-fixtures.mjs` does, so no model ran.
