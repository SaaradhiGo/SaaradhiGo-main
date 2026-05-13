# SaaradhiGo Web

Web client for the SaaradhiGo / VahanGo platform. Lives under the [SaaradhiGo-web](../../) monorepo at `apps/web`.

> Status: placeholder. No application code has been added yet.

## Scope

This directory will contain the SaaradhiGo web application — most likely a rider/landing web experience and/or an internal operations console — including:

- Source code, build tooling, and dependency manifest (e.g. `package.json` / lockfile)
- Static assets and environment configuration
- App-specific tests
- GitHub Actions workflows producing the `build/web` and `test/web` status checks required by the monorepo branch-protection rules

## Backend integration

Consumers in this app should target the same SaaradhiGo backend as the mobile client:

- REST: `https://dev.api.saaradhigo.in/api/v1`
- WebSocket: `wss://dev.api.saaradhigo.in/ws`

See [SaaradhiGo-backend](../../../SaaradhiGo-backend) for the full endpoint list.

## Getting started

To be filled in once the app is scaffolded. Expected entries:

- Prerequisites (Node version, package manager)
- Install / dev / build / test commands
- Environment variables and `.env` template
- Deployment notes
