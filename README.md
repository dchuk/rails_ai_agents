# Rails Claude Kit

A zero-configuration, opinionated set of Claude Code agents, skills, and commands for modern Rails development. Install once, start building immediately.

## Philosophy

This kit follows a **hybrid Rails philosophy** — combining the best of 37signals' "vanilla Rails" approach with modern patterns:

- **Rich models first** — Business logic lives in models with concerns for sharing
- **Services when needed** — Service objects only for 3+ model orchestration or external APIs
- **Everything-is-CRUD routing** — New resources over custom actions
- **State as records** — Track business state with who/when/why, not booleans
- **Minitest + fixtures** — Fast, simple, Rails-native testing
- **ViewComponents** — Reusable UI with encapsulated logic
- **Hotwire** — Turbo + Stimulus for modern frontend without SPAs
- **Pundit** — Convention-based authorization (deny by default)
- **Solid Queue** — Database-backed background jobs

## Installation

### Option 1: Tell Claude Code to install it

```
Install rails development agents from /path/to/rails_ai_agents
```

Or use the install skill after manual setup:

```
/install
```

### Option 2: Manual installation

```bash
# Clone or copy the repo
git clone <repo-url> /tmp/rails-claude-kit

# Copy .claude/ directory into your Rails project
cp -r /tmp/rails-claude-kit/.claude/ /path/to/your-rails-project/.claude/

# Copy the conventions template
cp /tmp/rails-claude-kit/CLAUDE_TEMPLATE.md /path/to/your-rails-project/

# Merge CLAUDE_TEMPLATE.md into your existing CLAUDE.md
# (or rename it to CLAUDE.md if you don't have one)
```

## What's Included

### 18 Agents

Specialized agents for every aspect of Rails development:

| Agent | Purpose |
|-------|---------|
| `rails-model` | Rich models with concerns, validations, scopes |
| `rails-controller` | CRUD-everything RESTful controllers with Pundit |
| `rails-concern` | Model/controller concerns for code sharing |
| `rails-state-records` | State-as-records pattern (not booleans) |
| `rails-service` | Service objects with Result pattern |
| `rails-query` | Query objects for complex database queries |
| `rails-presenter` | SimpleDelegator presenters for view formatting |
| `rails-policy` | Pundit authorization policies |
| `rails-view-component` | ViewComponents with Lookbook previews |
| `rails-migration` | Safe, reversible database migrations |
| `rails-test` | Comprehensive minitest tests with fixtures |
| `rails-tdd` | Red-Green-Refactor TDD workflow |
| `rails-job` | Shallow Solid Queue jobs |
| `rails-mailer` | ActionMailer with previews |
| `rails-hotwire` | Turbo + Stimulus + Tailwind patterns |
| `rails-review` | Code review + security audit (read-only) |
| `rails-lint` | RuboCop + Brakeman fixes |
| `rails-implement` | Implementation orchestrator |

### 23 Skills

Deep knowledge modules with patterns and examples:

| Skill | Purpose |
|-------|---------|
| `rails-architecture` | Architecture decision rubric and layer interactions |
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

### 2 Commands

| Command | Purpose |
|---------|---------|
| `frame-problem` | Challenge stakeholder requests to identify real needs |
| `refine-specification` | Refine feature specifications with structured Q&A |

### Security

- **`settings.json`** — Default permissions allowing standard Rails commands, denying destructive operations
- **`hooks/block-secrets.sh`** — PreToolUse hook preventing access to `.env`, `master.key`, credentials, and private keys

## Tech Stack Assumptions

| Component | Choice |
|-----------|--------|
| Ruby | 3.3+ |
| Rails | 8.x |
| Testing | Minitest + fixtures |
| UI Components | ViewComponents |
| Authorization | Pundit |
| Background Jobs | Solid Queue |
| Frontend | Hotwire (Turbo + Stimulus) |
| CSS | Tailwind CSS |
| Linting | RuboCop (omakase) |
| Security | Brakeman |

## Architecture Quick Reference

```
Where should this code go?
├─ Data validation, associations, simple logic? → Model
├─ Shared behavior across models? → Concern
├─ Business state tracking (who/when/why)? → State Record
├─ Orchestrates 3+ models or external APIs? → Service Object
├─ Complex query (3+ joins, aggregations)? → Query Object
├─ View formatting? → Presenter
├─ Authorization? → Pundit Policy
├─ Reusable UI with logic? → ViewComponent
├─ Async work? → Shallow Job (Solid Queue)
├─ Complex form (multi-model)? → Form Object
└─ HTTP request handling? → Controller (keep thin!)
```

## Conventions

- **Routing:** `POST /posts/:id/publications` not `POST /posts/:id/publish`
- **State:** `Closure` record, not `closed: boolean`
- **Jobs:** `order.fulfill_later` / `Order.fulfill_now` — jobs only delegate
- **Testing:** `assert_equal expected, actual` — never `expect(...).to eq(...)`
- **Models:** Rich first, extract only when complexity demands it

## License

MIT
