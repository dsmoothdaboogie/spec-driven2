# Frontend Standards — Angular 18

**Stack:** Angular 18 (standalone APIs), TypeScript (strict), Tailwind CSS, ESLint, Prettier, Jest (unit), Cypress (e2e), JSDoc.  
**Browsers:** Chrome, Edge, Safari – last 2 versions.  
**Accessibility:** WCAG 2.2 AA.

## 0) Principles
- **Spec-driven, test-first:** implement from `SPEC.md` + `ACCEPTANCE.md`.  
- **Small, pure, composable:** components < 300 LOC, single responsibility, pure inputs/outputs where possible.  
- **Signals-first:** prefer Angular Signals for component state; RxJS at boundaries (HTTP, sockets, timers).  
- **Performance by default:** `OnPush` change detection and `trackBy` for lists; lazy load everything.  
- **Accessibility is a requirement, not a feature.**  
- **Security by design:** no direct DOM manipulation; sanitize untrusted content; least-privilege APIs.

## 1) Project Structure
```
src/
  app/
    core/
    shared/
    features/
      <feature-name>/
        ui/
        data/
        pages/
    app.config.ts
    app.routes.ts
  assets/
  environments/
  styles/
    tailwind.css
    globals.css
```
- Standalone components only.  
- Route per feature.  
- Dumb vs smart: presentational in `shared/`, orchestration in `pages/`.

## 2) Angular 18 Conventions
### Components
- `standalone: true`, `OnPush` change detection.
- Use `@if`, `@for`, `@switch` templates with `track`.
- Inputs readonly; Outputs emit domain events.
- Prefer Signals for local state; minimal Effects.
- Accessibility first: semantic HTML, ARIA as fallback.

### Services / Data
- HttpClient in data services only.  
- Map transport → domain errors.  
- Cache in signals/RxJS; TTL in-memory.

### Routing
- Lazy by default.  
- Guards pure; redirect via router only.

### DI
- Prefer `inject()`.

## 3) Styling: Tailwind CSS
- Utilities-first; design tokens via CSS vars.
- Minimal global CSS.  
- Responsive: mobile-first Tailwind breakpoints.  
- Dark mode via `class="dark"`.

## 4) Accessibility
- Keyboard focus; visible outline.  
- Proper roles/names/states.  
- Color contrast AA.  
- Inputs labeled; live regions for async updates.  
- Move focus on route changes.  
- Automated checks via axe (Jest + Cypress).

## 5) Coding Style & Conventions
- `strict: true`, prefer `readonly`, no `any`.  
- File names: kebab-case; suffixes: component, service, pipe, directive.  
- Comments: JSDoc for all exports.  
- Smart/page vs dumb/presentational split.

## 6) Error Handling & Validation
### Global Errors
- Custom `GlobalErrorHandler`; structured logs; safe user messaging.

### Forms
- ReactiveForms only; async validation as needed.  
- Schema validation optional via Zod.  
- a11y feedback via `aria-live`.

## 7) Testing Strategy
### Unit (Jest)
- 80%+ coverage; Testing Library; accessibility assertions via jest-axe.

### Integration
- HttpTestingController.

### E2E (Cypress)
- Critical flows only; use data-testid selectors; avoid cy.wait(ms).

## 8) ESLint & Prettier
- `.prettierrc`: `printWidth 100`, `singleQuote true`, `trailingComma all`, `semi true`, `tabWidth 2`.

### ESLint Highlights
- Extends angular-eslint, @typescript-eslint, prettier.
- No `any`, no default exports, import order enforced, no unused imports.
- Angular template lint: alt-text, click-key-events, focus support.

## 9) Jest Config (excerpt)
```ts
import type { Config } from 'jest';
const config: Config = {
  testEnvironment: 'jsdom',
  transform: { '^.+\\.(ts|mjs|js)$': ['@swc/jest'] },
  setupFilesAfterEnv: ['<rootDir>/jest.setup.ts'],
  collectCoverageFrom: ['src/**/*.ts', '!src/main.ts'],
  coverageThreshold: { global: { statements: 80 } }
};
export default config;
```

## 10) Cypress
- Structure under `cypress/e2e/<feature>/*.cy.ts`.  
- Page objects.  
- `cypress-axe` for accessibility.  
- Record screenshots on fail.

## 11) Lint & CI Hooks
- Pre-commit: eslint --fix, prettier --write.  
- CI: lint, jest, minimal cypress.  
- Conventional commits optional.

## 12) Performance
- Signals + computed.  
- `@for trackBy`.  
- Lazy load heavy deps.  
- Avoid impure pipes.

## 13) Security
- No direct DOM; sanitize HTML.  
- Tokens in cookies/in-memory only.  
- CSP enforced; escape user input.

## 14) Docs & JSDoc
- JSDoc on exports; feature READMEs.  
- Example + edge cases.

## 15) Definition of Done
- Acceptance met; lint/test pass; a11y verified; no console errors; performance sane.

### Testing, Analytics & `data-testid` Standards

We use `data-testid` attributes as a **shared identifier** across:

- Automated tests (unit, integration, e2e)
- Product analytics (e.g., Google Analytics)
- Session replay tools (e.g., Glassbox)

These IDs must be **intentional, unique, and documented**.

#### 1. Where `data-testid` is required

Add a `data-testid` to any interactive element that:

- Can be clicked / tapped / submitted / toggled, or
- Represents a critical UX or business step we want to track.

At minimum, this includes:

- Native elements: `<button>`, `<a>`, `<input>`, `<select>`, `<textarea>`
- Elements with interactive roles: `role="button"`, `role="link"`, `role="tab"`, etc.
- Elements with handlers like `(click)`, `(keyup.enter)`, `onClick`, etc.
- Key navigation and CTAs (e.g., primary actions, filters, form submits, tab switches).

Non-interactive purely decorative elements generally **do not** need `data-testid`.

#### 2. Naming convention

`data-testid` values must be:

- **Descriptive**
- **kebab-case**
- **Feature-scoped where possible**

Recommended pattern:

> `feature-context-element-action`

Examples:

- `requests-filter-apply-button`
- `login-email-input`
- `nav-profile-menu-toggle`
- `settings-notifications-save-button`
- `profile-avatar-upload-input`

Avoid:

- Vague IDs like `submit-button`, `cta1`, `button1`, `link`, `icon`, etc.
- IDs that encode transient details (e.g., `blue-button`, `step3-button`).

#### 3. Uniqueness & Registry

- `data-testid` values must be **globally unique** across the frontend.
- We maintain a central registry at:

  `agent-os/docs/FRONTEND-TESTIDS.md`

- For each `data-testid`, the registry must track:

  - `data-testid` value  
  - File path(s) where it appears  
  - Element type (button, link, input, etc.)  
  - Short description (what the interaction represents from a user/business perspective)

This registry is the **source of truth** for:

- Test authors (what to target)
- Analytics & Glassbox instrumentation (what to track)
- Any AI agent reasoning about interactions.

#### 4. Workflow & Automation (`manage-testids`)

We use the `manage-testids` Agent-OS command to keep this consistent:

- In **review mode**:
  - Scans a file/folder/repo
  - Detects missing, duplicated, or weak `data-testid`s
  - Proposes new IDs and updates to `FRONTEND-TESTIDS.md` (no code changes)

- In **apply mode** (explicitly requested):
  - Adds/renames `data-testid`s in code according to the agreed plan
  - Writes/updates `agent-os/docs/FRONTEND-TESTIDS.md`

**Expectations:**

- New or modified interactive UI **must** either:
  - Have compliant `data-testid`s added manually, **or**
  - Be processed via `manage-testids` (review → apply).
- `FRONTEND-TESTIDS.md` should be updated in the same PR that introduces or changes `data-testid`s.

#### 5. Tests & Analytics Usage

- **Tests (Jest/Cypress)**:
  - Prefer `data-testid` selectors for stability rather than brittle CSS selectors.
  - Example: `cy.get('[data-testid="login-submit-button"]')`

- **Analytics & Glassbox**:
  - Use `data-testid` as the primary selector for event tracking and replay tagging whenever possible.
  - Do not rely on text labels or CSS classes for long-lived tracking.

By following this standard, we get:

- Stable, readable tests  
- Reliable analytics & Glassbox signals  
- A single, discoverable map of important UI interactions across the app


## Appendix A — Tailwind Example
Button: `inline-flex items-center gap-2 rounded-md px-3 py-2 text-sm font-medium`

## Appendix B — Suggested Scripts
```json
{
  "scripts": {
    "start": "ng serve",
    "build": "ng build",
    "test": "jest",
    "lint": "eslint ./src --ext .ts,.html",
    "format": "prettier --write .",
    "e2e": "cypress run"
  }
}
```
