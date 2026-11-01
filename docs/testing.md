# Testing and Validation

## Testing Philosophy

This project prioritizes reproducible, non-destructive testing.

Offline tests must be performed before considering any interaction with physical hardware. A successful offline test does not establish that a command is safe or compatible with a particular sensor firmware.

## Build Environment

The experimental implementation was built using:

- Operating system: Linux Mint 22.3
- Build system: Meson
- Compiler: GCC
- Project: libfprint, Goodix TLS driver
- Build directory: `libfprint/builddir`

The modified library was compiled locally. It was not installed into the system.

## Build Instructions

From the upstream source repository:

```bash
cd libfprint
meson compile -C builddir -j 1
```

A successful build confirms that the modified source compiles in the tested environment. It does not establish hardware compatibility.

## Offline Test Suite

The test suite is located at:

`libfprint/tests/test-goodix-packets.c`

It covers the following cases:

### Existing packet parser tests

- Coalesced packet handling.
- Partial packet handling.
- Padded packet handling.
- Partial padded packet handling.

### Experimental IAP version tests

- Request packet encoding.
- Valid IAP version response parsing.
- Rejection of responses shorter than the required length.
- Rejection of empty responses.
- Rejection of invalid UTF-8 data.

## Running the Tests

From the upstream source repository:

```bash
cd libfprint
meson test -C builddir goodix-packets --print-errorlogs
```

## Recorded Results

The experimental implementation compiled successfully.

The `goodix-packets` test suite completed with:

- Failures: 0
- Skipped tests: 0
- Timeouts: 0

Meson reports one registered test executable. That executable runs nine GLib test cases.

## Continuous Integration

The repository includes a GitHub Actions workflow at
`.github/workflows/offline-tests.yml`.

The workflow was successfully executed on GitHub Actions with:

- Runner: Ubuntu 24.04.
- Upstream revision: `aaa9393d9e6b8d0f29f64879cf6c926a976bb1be`.
- Experimental patch: `experimental-iap-version.patch`.
- Build: Meson compilation of the Goodix TLS driver.
- Tests: `goodix-tls`, `goodix-deactivate` and `goodix-packets`.
- Result: all workflow steps passed.

Recorded successful run:

- Run ID: `41273086469`.
- Research repository commit: `fbd560532fb9011ff820a194e41e31d6db6580ad`.

This confirms that the patch applies to the pinned upstream revision,
compiles in the CI environment and passes the selected offline tests.
It does not establish physical sensor compatibility, command safety,
or successful communication with firmware `GF3268_RTSEC_APP_10024`.

## Hardware Testing Restrictions

The following operations are outside the scope of the current test suite:

- Sending `0xF6` to a physical sensor.
- Writing or provisioning a PSK.
- Flashing or updating firmware.
- Resetting the sensor to force a different initialization state.
- Installing the experimental driver system-wide.
- Running normal enrollment tests against the physical device.

The experimental IAP command has not been executed against physical hardware.

## Reproducibility and Evidence

Diagnostic results should distinguish clearly between:

- Source-code inspection.
- Offline compilation.
- Offline unit tests.
- Physical USB communication.
- Confirmed hardware behavior.

Logs must be reviewed and sanitized before publication. Personal paths, usernames, device identifiers unrelated to the investigation, and other potentially sensitive information should not be included unnecessarily.

## Current Validation Summary

| Area | Result |
|---|---|
| Compilation | Passed |
| Existing packet parser tests | Passed |
| IAP request encoding | Passed |
| IAP response validation | Passed |
| GitHub Actions build and offline tests | Passed (Ubuntu 24.04) |
| Physical execution of `0xF6` | Not performed |
| Firmware compatibility | Unconfirmed |
| PSK issue | Unresolved |
