# SwISD-Core

Headless node runtime library: everything a headless Pi node needs to boot, provision, pull models, verify, and self-update. The swarm brain (network, crdt, peer, ownership, executor, tasks, admin) stays in the testbed, which consumes this library.

## Modules

| Path | Contents |
| --- | --- |
| `src/config` | Schemas, loader, provision config, credentials |
| `src/crypto` | Argon2id, Ed25519, HMAC, hex |
| `src/delivery` | OTA updater (SHA-256 + Ed25519 verification), identity, heartbeat, installer, local supervisor, verifier, watchdog |
| `src/provision` | USB-stick apply, WiFi, captive DNS, setup agent |
| `src/models` | HuggingFace fetch, downloader, ingest, registry, manager, approval, intent, chunk storage convention |
| `src/storage` | Capacity |
| `src/performance` | Load monitor |
| `src/observability` | Event bus + schema |
| `src/errors.ts`, `src/types.ts`, `src/utils.ts` | Shared |

## Requirements

- Node >= 22
- Single external runtime dependency: `@noble/hashes`. Everything else is Node builtins.
- TypeScript, strict, NodeNext. Strict ESM.

## Install / build / test

```sh
npm install
npm run build   # tsc
npm test        # node:test suite, 62 tests, run via tsx
```

## Usage

Subpath exports: `./config`, `./crypto`, `./delivery`, `./models`, `./observability`, `./performance`, `./provision`, `./storage`.

```ts
import { loadProvisionConfig } from 'swisd-core/config';
import { verifyReleaseArtifact } from 'swisd-core/delivery';
```

## Tailscale

The provision config schema supports an optional `tailscale` block (`authKey`, `hostname`) so a headless Pi autoconnects to a tailnet. The updater's pending-requirements flow lets an operator flag Tailscale installation for the next OTA update.

## License

MPL-2.0.
