# Polaris-PySDK

## Project Summary

- Polaris-PySDK packages the Python client used to call the HalService
  exposed by Polaris-Client. The distributable project is `polaris-sdk/`;
  its package name is `polaris-sdk` and its import namespace is
  `polaris_sdk`. The SDK combines a typed public API with generated
  protobuf and gRPC bindings under `src/polaris_sdk/_proto`, domain
  dataclasses and enums under `src/polaris_sdk/types`, and runtime helpers
  for connection, discovery, one-shot calls, monitoring, events, and
  long-running tests. `py.typed` marks the package for type-aware
  consumers.

- The repository also contains generators in `polaris-sdk/tools`, examples
  for common and long-running operations, documentation, and a
  compatibility/deprecation shim for the former package name. The generated
  bindings cover the same broad module vocabulary as Polaris-HAL, so the
  SDK is a client contract rather than a local hardware implementation. It
  depends on a reachable HalService and therefore cannot prove physical
  peripheral support by itself.

- The root Makefile declares setup, virtual-environment, generation,
  stale-generated-file checks, pytest, Ruff, strict mypy, build, and
  cleanup workflows. The test suite includes connection, discovery,
  one-shot, event, monitor, long-running, type round-trip, deprecation, and
  fake-server fixtures. That is meaningful protocol/client coverage, though
  server interoperability, generated-code freshness in every environment,
  and real board behavior still need manual confirmation. The inventory
  below separates API functionality from deployment assumptions.

## Feature Inventory

| # | Name / Description | Implemented? | Test Coverage? | Manual Test |
|---:|---|---|---|---|
| 1 | Typed `polaris_sdk` package and `py.typed` marker | Implemented | Strict mypy target; package tests | [ ] Manual verification required |
| 2 | gRPC/protobuf generated bindings | Implemented | Generation/staleness checks declared | [ ] Manual verification required |
| 3 | Client connection and channel setup | Implemented | `test_connect.py`, fake server | [ ] Manual verification required |
| 4 | Service discovery | Implemented | `test_discovery.py` | [ ] Manual verification required |
| 5 | One-shot module test calls | Implemented | `test_oneshot.py` | [ ] Manual verification required |
| 6 | Monitoring and event callbacks | Implemented | `test_monitor.py`, `test_event.py` | [ ] Manual verification required |
| 7 | Long-running test operations | Implemented | `test_long_running.py` | [ ] Manual verification required |
| 8 | Typed module dataclasses and round trips | Implemented | `test_types_roundtrip.py` | [ ] Manual verification required |
| 9 | Fake server integration fixture | Implemented | `tests/fakes/fake_server.py` and suite | [ ] Manual verification required |
| 10 | Former-name deprecation shim | Implemented | `test_deprecation_shim.py` | [ ] Manual verification required |
| 11 | Code generation tools and clean regeneration | Implemented | `make gen`, `gen-check`, `gen-clean` declared | [ ] Manual verification required |
| 12 | Lint, typecheck, wheel/sdist build | Implemented | `make lint`, `typecheck`, `build` declared | [ ] Manual verification required |
| 13 | Real Polaris-Client/HAL interoperability | Partial | Fake-server tests only; live integration not found | [ ] Manual verification required |

## Validation

```bash
make setup
make gen-check
make lint
make typecheck
make test
make build
```

Run examples against a real HalService to validate networking, permissions, and hardware-backed results.
