# Protocol Command Reference

## Scope

This document records commands identified in the Goodix TLS driver and related protocol research.

A command being defined in source code, implemented locally, or tested offline does not mean it has been validated against physical hardware.

## Command Reference

| Command | Name | Function | Status |
|---|---|---|---|
| `0xA6` | READ_OTP | Read OTP data | Identified in source |
| `0xA8` | FIRMWARE_VERSION | Retrieve application firmware version | Identified in source |
| `0xAE` | QUERY_MCU_STATE | Query MCU state | Identified in source |
| `0xE0` | PRESET_PSK_WRITE | Write preset PSK | Hardware attempt timed out |
| `0xE4` | PRESET_PSK_READ | Read preset PSK | Hardware response observed |
| `0xF6` | GET_IAP_VERSION | Retrieve IAP firmware version | Implemented and tested offline only |

## Command Details

### `0xE4` — PRESET_PSK_READ

This command reads the sensor's preset PSK information.

**Observed behavior:**
- The device completed the command.
- The returned PSK hash did not match the expected value.

This is a hardware observation from the diagnostic session.

### `0xE0` — PRESET_PSK_WRITE

This command initiates preset PSK provisioning.

**Observed behavior:**
- A write operation was initiated.
- The operation timed out after five seconds.
- A subsequent PSK read still returned a mismatched hash.

The result does not establish whether the sensor processed any part of the write operation.

**Safety classification:** State-changing. Do not execute during further diagnostics.

### `0xF6` — GET_IAP_VERSION

This command was implemented experimentally in the local driver.

The implementation includes:
- Request packet encoding.
- Response parsing.
- Response length validation.
- Empty response rejection.
- UTF-8 validation.
- Offline packet and response tests.

The expected response format was based on the related Python implementation.

**Validation status:**
- Compilation: passed.
- Offline tests: passed.
- Physical hardware execution: not performed.
- Compatibility with `GF3268_RTSEC_APP_10024`: unconfirmed.

**Safety classification:** Pending maintainer confirmation. Do not execute against physical hardware yet.

## Verification Levels

This repository uses the following distinctions:

1. **Identified in source:** The command or its definition exists in the upstream implementation.
2. **Implemented locally:** Experimental code has been added to this research repository or its associated patch.
3. **Tested offline:** Encoding, parsing, or validation has been tested without communicating with a physical sensor.
4. **Observed on hardware:** A physical device returned a response or exhibited the documented behavior.
5. **Hardware validated:** The command's behavior and safety have been independently established for the relevant firmware.

These levels are not interchangeable.

## Outstanding Questions

- Is `0xF6` compatible with firmware `GF3268_RTSEC_APP_10024`?
- Does the IAP version response format remain consistent across firmware revisions?
- Can the IAP version be queried safely before normal driver activation?
- What explains the PSK mismatch and provisioning timeout?

No undocumented command should be sent to the sensor merely because its implementation appears straightforward.
