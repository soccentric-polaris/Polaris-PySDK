# Polaris-PySDK — specs Remote: `git@github.com:soccentric-polaris/Polaris-PySDK.git`
Stack: Python, uv-managed, src layout. Consumes the `HalService` gRPC endpoint exposed by Polaris-Client — the same wire contract
Polaris-Server speaks. ## Layout * `polaris-sdk/` — everything: source, tooling, docs, examples, the make workflow (setup/ gen/ check/ build).
* `polaris-sdk/src/polaris_sdk/` — the package. Import name `polaris_sdk`, distribution name `polaris-sdk`.
* `polaris-sdk/src/polaris_sdk/_proto/` and `types/` — generated stubs, ~270 files, **committed on purpose**.
* `acadia_sdk` — deprecation shim re-exporting the public surface for callers on the old name. Lazy PEP 562 `__getattr__`, emits a `DeprecationWarning`, ships in the wheel. ## The regeneration exception This is the one leaf that regenerates protos. Polaris-Client and Polaris-Server must not, because a
second copy of the generated C++ symbols causes ODR/duplicate-symbol link errors. That is a C++
constraint with no Python equivalent, so it does not apply here.
