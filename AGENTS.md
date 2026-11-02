## Workflow

- Use Bun only for package management and repository scripts: `bun install`, `bun run <script>`, and `bunx --no-install <tool>`.
- Use `bun run test`, not `bun test`: Vitest supplies the strict reporter and per-file coverage policy and runs on Node.js.
- Work on a descriptive feature branch rather than `main`; use `.worktrees/` for isolated worktrees.
- Use focused `<type>(<scope>): <why>` commits.

## Protected tooling

Ask the user before modifying quality-gate configuration: `.dependency-cruiser.ts`, `.jscpd.json`, `biome.json`, `.semgrep.yml`, `knip.json`, `tsconfig.json`, and `vitest.*.ts`. Fix findings in code rather than weakening or bypassing checks.

## Implementation

- Write TypeScript modules; reuse existing modules before adding code.
- Make the smallest complete change and remove obsolete paths when replacing behavior.
- Include dependency rationale plus security and license impact in the PR or commit.
- Update documentation when public behavior or contributor workflows change.
- Use `YYYY-MM-DD` headings for changelog entries, not version numbers.
- Normalize unknown thrown values to `Error` at module boundaries. Keep user-facing errors safe and actionable while preserving useful developer diagnostics.
- Do not introduce dynamic code evaluation, unsafe shell execution, or hardcoded secrets.

## Verification

- Cover changed behavior, state transitions, contracts, and reachable errors.
- Run targeted verification and `bun run check` before claiming completion.
- Preserve all strict gates inherited from the PNPM template, including 90% per-file coverage and rejection of skipped/todo tests.
- Semgrep runs separately in CI; run `semgrep scan --config .semgrep.yml --error .` locally when security rules or affected code change.
