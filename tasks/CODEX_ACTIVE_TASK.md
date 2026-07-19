# Codex Active Task — Bootstrap `market-events`

## Mission

Create a new private GitHub repository and the first runnable version of a real iOS app named **Market Events**.

This is the first small vertical slice of a product intended for eventual App Store release. Keep the implementation deliberately simple. Do not build a backend, authentication, subscriptions, AI analysis, portfolio features, or trading functionality in this task.

## Repository

- GitHub owner: `GoMaaars`
- Repository name: `market-events`
- Visibility: private
- Description: `Capital market event calendar with historical data and advance reminders.`
- Default branch: `main`

Before creating it, verify that `GoMaaars/market-events` does not already exist.

If GitHub CLI is authenticated, create and clone it with the equivalent of:

```bash
gh repo create GoMaaars/market-events \
  --private \
  --description "Capital market event calendar with historical data and advance reminders." \
  --clone
```

If the repository already exists, clone it and inspect its state instead of overwriting anything.

## Product boundary

The app provides only:

- upcoming capital-market events;
- event dates and source metadata;
- advance reminders;
- historical occurrence rows;
- descriptive historical statistics.

The app must not contain:

- investment advice;
- buy/sell recommendations;
- price forecasts;
- stock recommendations;
- claims that an event causes the market to rise or fall;
- brokerage integration or automated trading.

All copy must remain factual and neutral.

## Technical baseline

Create the application with the current official Expo default template and TypeScript. Use Expo Router.

Preferred bootstrap command at the time of this task:

```bash
npx create-expo-app@latest . --template default@sdk-57
```

Use npm unless the machine already has a clearly established package-manager standard.

Configure:

- application name: `Market Events`;
- slug: `market-events`;
- iOS bundle identifier placeholder: `com.gomaaars.marketevents`;
- TypeScript strict mode;
- Expo Router typed routes where supported;
- light and dark appearance support;
- local notifications through `expo-notifications`;
- local persistence for user reminder preferences.

Do not add a server or database in this task.

## V0.1 functional scope

Implement four primary screens.

### 1. Upcoming

Show the next several events as cards ordered by date.

Each card displays:

- event name;
- category;
- date;
- days remaining;
- market or venue;
- whether reminders are enabled.

Initial event types:

- China stock-index futures expiration;
- broad-based ETF options expiration;
- FTSE China A50 futures settlement.

### 2. Calendar

Provide a simple month view or grouped date list. Prioritize reliability and readability over building a complex custom calendar component.

### 3. Event detail

Display:

- event description;
- event date;
- market/venue;
- source name and source URL field;
- reminder controls for T-7, T-3, T-1, and event day;
- historical summary metrics;
- a table/list of historical occurrences.

Required historical summary fields:

- sample count;
- up count;
- down count;
- flat count;
- average return;
- median return;
- average absolute return;
- average intraday range;
- maximum gain;
- maximum decline.

### 4. Settings

Include:

- default reminder offsets;
- notification-permission status;
- data methodology entry;
- disclaimer entry;
- app version placeholder.

## Data approach for this first task

Use a typed local seed dataset so the app is fully runnable offline.

Requirements:

- Put seed data in a dedicated data module, not inline in components.
- Clearly label it as development/sample data in code and in the UI.
- Include at least six upcoming sample events and at least twelve historical occurrence rows across the supported event types.
- Keep source fields in the schema even when a sample source URL is used.
- Create a clean interface so local data can later be replaced by an API without rewriting screens.

Do not present invented sample numbers as verified market facts. A visible `Sample data` badge is required until authoritative production data is connected.

## Notification behavior

Implement local notification scheduling only.

The user can enable or disable T-7, T-3, T-1, and event-day reminders for an event. The app must:

- request permission only after an explicit user action;
- schedule or cancel local notifications consistently;
- persist the preference locally;
- handle dates already in the past without crashing;
- explain that reminder delivery depends on device notification settings.

Remote push notifications are out of scope.

## Design direction

Use a clean, native-feeling financial utility design:

- high information density without visual clutter;
- strong typography and spacing;
- accessible touch targets and contrast;
- neutral colors for factual data;
- do not imply positive/negative trading signals through decorative red/green styling;
- support small and large iPhone layouts;
- avoid generic dashboard gradients and excessive cards.

## Repository documentation

Create:

- `README.md` — setup, run, test, architecture summary and current limitations;
- `AGENTS.md` — concise instructions for future Codex tasks;
- `docs/PRODUCT_SCOPE.md` — V0.1 boundaries and non-goals;
- `docs/DATA_CONTRACT.md` — TypeScript event and historical-statistics model;
- `docs/APP_STORE_READINESS.md` — checklist for later privacy policy, support URL, screenshots, metadata, TestFlight and review;
- `docs/NEXT_STEPS.md` — prioritized next milestones;
- `.env.example` only if an environment variable is genuinely required; otherwise do not create one.

## Engineering quality

Add and configure:

- ESLint;
- formatting using the project’s standard tooling;
- type checking;
- a small test suite covering the statistics calculator and notification-date calculation;
- GitHub Actions CI for install, lint, typecheck and tests;
- sensible `.gitignore`;
- no secrets or machine-specific paths.

Write a pure statistics utility that calculates summary metrics from historical rows. Do not hard-code summary values separately from the rows.

## Verification

Before finishing, run and record the results of:

```bash
npm install
npm run lint
npm run typecheck
npm test -- --runInBand
npx expo export --platform web
```

Adapt commands only when the generated template uses different script names. Do not claim success for checks that were not actually run.

## Git workflow

1. Create the repository and make a minimal bootstrap commit on `main`.
2. Create branch `feat/v0.1-app-shell`.
3. Implement the task on that branch.
4. Commit in coherent steps.
5. Push the branch.
6. Open a draft pull request to `main` titled:

   `feat: bootstrap Market Events v0.1 app shell`

The pull request body must include:

- implemented scope;
- screenshots or instructions for producing them;
- verification commands and results;
- known limitations;
- next recommended milestone.

Do not merge the pull request.

## Completion report

Write `tasks/CODEX_RESULT.md` in this task-hub repository with:

- new repository URL;
- branch name;
- draft PR URL;
- main implementation decisions;
- commands run and outcomes;
- blockers or manual actions still required;
- exact local command for the user to launch the app.

Commit and push that result file to `GoMaaars/codex-test`.

## Acceptance criteria

The task is complete only when:

- `GoMaaars/market-events` exists as a private repository;
- the Expo app launches;
- the four screens are navigable;
- sample events and historical rows are visible and explicitly marked as sample data;
- reminder preferences persist and local notification scheduling is implemented;
- statistics are calculated from occurrence rows;
- lint, typecheck, tests and web export complete successfully, or any failures are honestly documented;
- CI exists;
- a draft PR is open;
- `tasks/CODEX_RESULT.md` is pushed to this task-hub repository.
