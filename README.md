# Polaris-PySDK Python SDK leaf for the **Polaris** project (Renesas RZ/G2L + STM32) in the
SiliconCentric `project-managers` fleet. This leaf provides `polaris-sdk`, a Pythonic gRPC client for the `HalService`
endpoint exposed by `Polaris-Client`. The SDK distribution package is
**`polaris-sdk`** (import name `polaris_sdk`); a `acadia_sdk` deprecation shim
re-exports the public surface for callers still on the old name. The SDK source, tooling, docs, examples, and test suite live under
[`polaris-sdk/`](polaris-sdk). See [`polaris-sdk/README.md`](polaris-sdk/README.md)
for the full API, quickstart, and `make` targets (`setup`, `gen`, `check`,
`build`). ---
Part of the `Polaris` project in the `project-managers` fleet. See
`docs/project-managers.md` for the full 9-project/ 8-leaf hierarchy and
shared conventions.