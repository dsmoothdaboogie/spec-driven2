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