# Global Agent Rules

## 1) Communication

- Keep communication direct, concise, and execution-oriented.
- Favor minimal, root-cause fixes over broad speculative refactors.
- Remove obvious duplication and dead code when touching related areas.

## 2) GitHub Issue Language

- Use English for all GitHub issue content (title, body, comments) by default.
- Only use another language if the user explicitly asks for it in that request.

## 3) Skill Routing (Default Policy)

Apply this routing for every task:

0. Technology-match routing (mandatory, highest priority):
   - If Vue is detected in the project/task, must use Vue skill(s) (for example `vue-best-practices`, `vue`, `pinia`, `vue-router-best-practices`, `vue-testing-best-practices` as needed).
   - If React is detected in the project/task, must use React skill(s) (for example `vercel-react-best-practices` and React composition/best-practice skills as needed).
   - If TypeScript is detected in the project/task, must use TypeScript-focused skill(s) available in the environment.
   - This mapping is required whenever the corresponding technology appears in scope.

1. UI-facing work (layout/styling/visual hierarchy/copy presentation/interactions/responsive behavior):
   - Required: `frontend-design`
   - Add by intent:
     - `adapt` for responsive/device behavior
     - `harden` for overflow/edge cases/i18n resilience
     - `optimize` for rendering/loading/performance
     - `polish` for final refinement before ship

2. Logic-facing work (state/data flow/routing/business logic/component APIs):
   - Required: composition-first architecture discipline
   - Prefer composition patterns over boolean-prop expansion
   - Add: React performance best-practice skill when React performance is in scope

3. Mixed UI + logic work:
   - Apply both UI and logic routing rules in the same task.
4. Routing fallback:
   - If a required skill is unavailable or conflicts with the current context, continue with the best available equivalent and explicitly state the fallback.

## 4) Working Conventions

- Before implementation, state which skill-routing rules are being applied.
- Explicitly state detected stack signals (Vue/React/TypeScript) and the matched skills.
- If suitable third-party components/libraries exist, prefer using them to implement features instead of hand-writing everything from scratch.
- Keep behavior and copy aligned via shared config/constants when practical.
- Prefer simple, testable interfaces and avoid unnecessary compatibility layers.
- Do not expose secrets/tokens in output.
- Do not expose local absolute paths unless explicitly requested.

## 5) Quality Gate (Before Merge/Ship)

- Build must pass (`pnpm build` unless the project uses another build command).
- UI changes must be verified at both narrow and wide viewports.
- No obvious duplicate code paths or redundant props introduced.

## 6) Release/Deploy Runbook

When asked to release/deploy/ship:

1. Verification:
   - Run build and confirm success.
2. Commit:
   - Stage only intended changes.
   - Use one clear release commit message.
3. Tag:
   - Create a release tag on the shipped commit.
   - Preferred format: `release-YYYY-MM-DD-<scope>`.
4. Push order:
   - Push branch first, then push tag.
5. Post-release verification:
   - Confirm CI/deploy status is green.
   - Confirm production URL is reachable (if available).
   - Smoke-check key user paths touched in this release.
6. If verification fails:
   - Report failure clearly.
   - Provide rollback target (latest stable tag/commit).
7. Report:
   - Return commit SHA and tag in the final response.

## 7) New Project Bootstrap (Mandatory Check)

For every new project session/repo:

- Must explicitly ask the user:
  - whether to write/apply shared global agent conventions into a project-level `AGENTS.md`.
- If the user explicitly says **no**:
  - do not create or modify project-level agent rules.
  - continue work with global rules only.
- This check is mandatory and cannot be skipped.
