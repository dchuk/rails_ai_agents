# Rails Development Conventions

> Merge this into your project's `CLAUDE.md`. Sections marked with `[CUSTOMIZE]` should be adapted to your project.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Ruby | 3.3+ |
| Rails | 8.x |
| Testing | Minitest + fixtures |
| Components | ViewComponents (Lookbook for previews) |
| Authorization | Pundit (deny by default) |
| Jobs | Solid Queue |
| Frontend | Hotwire (Turbo + Stimulus) + Tailwind CSS |
| Assets | Propshaft + Import Maps |
| Linting | RuboCop (omakase) + Brakeman |

## [CUSTOMIZE] Project Overview

```
Describe your application here.
```

## Architecture Conventions

### Models First
- Business logic lives in models. Use concerns for horizontal sharing.
- Service objects ONLY for operations spanning 3+ models or external integrations.
- Query objects for complex queries that don't fit a single scope.
- Presenters (SimpleDelegator) for view-specific formatting.

### Everything-is-CRUD Routing
- Prefer creating a new resource over adding custom actions.
- `POST /posts/:id/publications` over `POST /posts/:id/publish`.
- RESTful routes only; no `member` or `collection` blocks with custom verbs.

### State as Records
- Track business state transitions as separate records (who/when/why).
- Boolean columns ONLY for technical flags (e.g., `email_verified`).
- State records: `Approval`, `Cancellation`, `Publication` — not `approved: true`.

### Authorization
- Pundit policies on every controller action: `authorize @record`.
- Deny by default: policies return `false` unless explicitly allowed.
- Use `policy_scope` for collections.

### Jobs
- Shallow jobs: call `_later` or `_now` methods on models/services.
- Jobs contain only deserialization + delegation. No business logic.
- Use Solid Queue recurring jobs for scheduled work.

### Frontend
- Turbo Frames for partial page updates.
- Turbo Streams for real-time broadcasts.
- Stimulus controllers: small, focused, one behavior each.
- Tailwind CSS utility classes; extract components for repeated patterns.
- ViewComponents for reusable UI; partials for simple one-offs.

## Testing Conventions

- **Framework:** Minitest + fixtures. NEVER use RSpec or FactoryBot.
- **Fixtures:** Meaningful names (`users(:admin)`, `posts(:published)`).
- **Test types:** Model, controller (integration), system (Capybara), component (ViewComponent).
- **TDD workflow:** Red (failing test) -> Green (minimal pass) -> Refactor.
- **Coverage:** Every model validation, scope, and public method. Every controller action. Critical user flows as system tests.

## Quality Gates

- `bin/rubocop` — zero offenses before commit.
- `bin/brakeman --no-pager` — zero warnings before merge.
- `bin/rails test` — all tests pass.
- No N+1 queries (use `includes`/`preload`).
- No hardcoded credentials (use Rails credentials or ENV).

## Security Rules

### Protected Files (NEVER read or output)
- `.env`, `.env.*`
- `config/master.key`, `config/credentials.yml.enc`
- `.kamal/secrets`
- Any `*.pem`, `*.key` files
- `storage/*.sqlite3`

### Forbidden Operations
- `git push --force` to main/master/production
- `git reset --hard` without explicit user confirmation
- `rm -rf` on root, home, or parent directories
- `chmod 777`
- Database destructive commands in production (`db:drop`, `db:reset`)
- Piping curl/wget output to shell interpreters

## Development Commands

```bash
bin/dev                     # Start dev server
bin/rails test              # Run all tests
bin/rails test:system       # Browser tests
bin/rubocop                 # Check style
bin/rubocop -a              # Auto-fix style
bin/brakeman --no-pager     # Security scan
bin/rails db:migrate        # Run migrations
bin/rails console           # Rails console
```

## Agent Catalog

These agents are available in `.claude/agents/`:

| Agent | Trigger |
|-------|---------|
| `rails-model` | Creating/modifying models, concerns, validations, scopes |
| `rails-controller` | Creating/modifying controllers, routes, CRUD actions |
| `rails-concern` | Extracting shared behavior into concerns |
| `rails-state-records` | Implementing state-as-records pattern |
| `rails-service` | Service objects for multi-model operations |
| `rails-query` | Query objects for complex database queries |
| `rails-presenter` | Presenters for view formatting logic |
| `rails-policy` | Pundit authorization policies |
| `rails-view-component` | ViewComponents with previews |
| `rails-migration` | Safe, reversible database migrations |
| `rails-test` | Writing minitest tests with fixtures |
| `rails-tdd` | TDD red-green-refactor workflow |
| `rails-job` | Background jobs with Solid Queue |
| `rails-mailer` | ActionMailer with previews |
| `rails-hotwire` | Turbo Frames/Streams + Stimulus + Tailwind |
| `rails-review` | Code review + security audit (read-only) |
| `rails-lint` | RuboCop + Brakeman fixes |
| `rails-implement` | Implementation orchestrator |

## Skill Catalog

These skills are available in `.claude/skills/`:

| Skill | Purpose |
|-------|---------|
| `rails-architecture` | Architecture decision rubric and patterns |
| `rails-model-generator` | Model generation with conventions |
| `rails-controller` | Controller patterns and integration tests |
| `rails-concern` | Concern extraction patterns |
| `rails-service-object` | Service object with Result pattern |
| `rails-query-object` | Query object patterns |
| `rails-presenter` | Presenter patterns |
| `form-object-patterns` | Form objects for complex forms |
| `viewcomponent-patterns` | ViewComponent patterns and testing |
| `authentication-flow` | Authentication implementation |
| `authorization-pundit` | Pundit policy patterns |
| `database-migrations` | Safe migration patterns |
| `caching-strategies` | Fragment, HTTP, and Russian-doll caching |
| `solid-queue-setup` | Solid Queue configuration |
| `hotwire-patterns` | Turbo + Stimulus + Tailwind patterns |
| `action-cable-patterns` | WebSocket patterns |
| `action-mailer-patterns` | Email patterns with previews |
| `api-versioning` | API versioning strategies |
| `tdd-cycle` | TDD workflow for minitest |
| `performance-optimization` | Performance tuning patterns |
| `i18n-patterns` | Internationalization patterns |
| `active-storage-setup` | Active Storage configuration |
| `install` | Install this kit into a Rails project |
