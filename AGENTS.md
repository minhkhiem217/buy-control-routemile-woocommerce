# Buy Control — development guide

Project: https://github.com/minhkhiem217/buy-control-routemile-woocommerce

This is an independently maintained WooCommerce delivery plugin derived from RouteMile 1.6.5 (GPL-3.0-or-later). The inherited architecture and historical context are archived in [docs/archive/UPSTREAM-AGENTS.md](docs/archive/UPSTREAM-AGENTS.md); treat old URLs, credentials examples, release instructions and historical roadmaps as reference only.

## Engineering constraints

- Work on feature branches and review changes before merging into main.
- Preserve the GPL license, original copyright notices and third-party attribution. Mark modified files where required.
- Keep `routew_` identifiers, text domain, order metadata, custom statuses, shipping method identifiers, and PHP entrypoint stable until a tested migration is designed. Never activate this distribution alongside upstream.
- Use WooCommerce CRUD APIs and preserve HPOS and supported checkout-block behavior.
- Validate input, escape output, enforce nonce/capability and order ownership checks. Never expose customer coordinates, credentials or COD records to unauthorized users.
- Avoid broad comment removal or blind replacement of identifiers. Remove stale comments only after checking behavior.
- Run `php tests/RouteWTestRunner.php` before requesting merge. Browser harness exists, but E2E specs must be verified before claiming coverage. Run against a dedicated staging installation, not production.
- Document behavior changes in CHANGELOG.md; do not publish to the upstream WordPress.org slug.

## Layout

- `routemile-woocommerce.php`: plugin bootstrap
- `includes/`: checkout, shipping, settings, orders, rider workflow, cash settlement
- `includes/services/`: domain services and map integrations
- `includes/api/`: REST checkout API
- `assets/`, `templates/`: UI and PWA
- `tests/`: static test runner
- `tools/ui/`: UI asset build

Next milestones: local environment, visible branding, smoke tests, security review, then feature roadmap. No production readiness is assumed.
