# Polaris-PySDK Build and Deployment

## Purpose and scope

Polaris-PySDK is a Python SDK package using `uv`, setuptools, gRPC, and protobuf. The root Makefile creates a virtual environment, installs the package editable with development extras, regenerates protocol/type bindings, runs checks, and builds a wheel and source distribution.

## 1. Prerequisites

- Python 3.10 or newer, GNU Make, and `uv` on PATH (override with `UV=...`).
- Network access for `uv` dependency installation.
- The sibling `Polaris-HAL/protos` source expected by the generation tools must be available at the path assumed by `tools/gen_proto.py`.

## 2. Setup

```bash
make venv                   # create .venv only
make setup                  # install polaris-sdk[dev] editable
```

The package manifest declares gRPC/protobuf runtime dependencies and development extras including pytest, coverage, mypy, ruff, and protobuf generation tools.

## 3. Build and compile

```bash
make gen                    # regenerate proto and dataclass bindings
make gen-check              # fail if committed stubs are stale
make gen-clean              # remove and fully regenerate stubs
make build                  # wheel + sdist in polaris-sdk/dist
```

Generated output is under `polaris-sdk/src/polaris_sdk/_proto` and should be reviewed before committing. `gen-check` is the non-mutating freshness check apart from its temporary regeneration/revert workflow.

## 4. Test and lint

```bash
make test                   # pytest with coverage
make lint                   # ruff check
make typecheck              # mypy --strict
make check                  # lint, typecheck, and test
```

The Makefile runs tests under `polaris-sdk/tests` and excludes generated/protocol directories from the configured lint/type-check rules.

## 5. Packaging and artifacts

`make build` installs the `build` package into `.venv` if needed and writes the setuptools wheel and source distribution to `polaris-sdk/dist`. No publishing or registry upload target exists; credentials and release signing are external.

## 6. Deployment, install, and run

```bash
make shell                  # uv-activated development shell
uv pip install polaris-sdk/dist/*.whl
```

The first command is an exact Make target. The wheel install is a manual consumer-side command, conditional on a completed build and shell glob expansion. This repository declares no device, cloud, service, or credentialed deployment target; runtime integration with the HAL requires a compatible gRPC endpoint and generated contract.

## 7. Cleanup

```bash
make clean                  # package build outputs and caches; keep .venv
make distclean              # clean plus remove .venv and stamps
```

## 8. Verification caveats

Unit tests and static checks do not prove compatibility with a live Polaris HAL or target hardware. Manually verify protobuf compatibility, endpoint connectivity, target authentication, streaming behavior, and SDK installation in the intended Python environment. No cloud deployment is defined.