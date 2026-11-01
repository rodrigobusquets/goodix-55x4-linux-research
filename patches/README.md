# Experimental IAP Version Query

## Overview

This patch adds support for the Goodix `GET_IAP_VERSION` protocol command (`0xF6`) to the experimental libfprint Goodix TLS driver.

It includes:
- IAP version request encoding.
- IAP version response parsing and validation.
- Offline packet encoding tests.
- Offline response validation tests.

## Safety Status

**Experimental — hardware execution not authorized.**

The implementation has only been compiled and tested offline. It has not been executed against physical hardware.

Do not invoke the new command on a physical sensor until its compatibility and safety have been confirmed for the target firmware.

## Known Hardware

- USB ID: `27c6:55b4`
- Firmware: `GF3268_RTSEC_APP_10024`

## Validation

The offline test suite passed:
- Request packet encoding.
- Valid response parsing.
- Short response rejection.
- Empty response rejection.
- Invalid UTF-8 rejection.

No hardware interaction was performed during these tests.

## Licensing

The patch modifies LGPL-2.1-or-later code. Original copyright notices must be preserved.

See the repository license and attribution information.

## Base Revision

The patch was developed against the following upstream repository revision:

- Repository: https://github.com/GuNanOvO/goodix-55x4-linux
- Branch: `main`
- Commit: `aaa9393d9e6b8d0f29f64879cf6c926a976bb1be`

The patch should be reviewed and tested against this exact revision before applying it to other versions.
