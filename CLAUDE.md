# Yeopker

## Layout
- `mobile/` - the Yeopker mobile app (Expo, React Native, TypeScript). Android + iOS from one codebase.
- `*.html` at the root - old redirect pages to `wook673.github.io/daniel-rental`. Do not edit.
- `.github/workflows/mobile-ci.yml` - typecheck + lint on every PR that touches `mobile/`.
- `.github/workflows/mobile-release.yml` - EAS build + store submit on a `v*` tag or a manual run.

## Agents
- `app-developer` - feature work and bug fixes in `mobile/`.
- `release-manager` - version bump, tag, build, and store submit. See `mobile/RELEASE.md`.

Flow: app-developer makes a change -> PR -> CI green -> merge -> release-manager bumps version and tags -> EAS builds -> Play internal track + TestFlight -> a person promotes to the public stores.

## Commands (run in mobile/)
- `npm run check` - typecheck + lint. Must pass before any commit.
- `npx expo start` - dev server. Open with the Expo Go app on a phone.
