# Goodix 55x4 Linux Research

Independent research into the Goodix `27c6:55b4` fingerprint sensor and its compatibility with Linux and libfprint.

**Language:** English | [Español](README.es.md)

## Purpose

This project investigates protocol behavior, firmware compatibility, PSK provisioning, USB communication and TLS initialization in Goodix fingerprint sensors.

The goal is to document reproducible findings, develop offline-tested improvements and contribute useful technical evidence to the Linux fingerprint community.

## Hardware Under Investigation

| Property | Value |
|---|---|
| USB ID | `27c6:55b4` |
| Firmware | `GF3268_RTSEC_APP_10024` |
| Driver | Goodix TLS for libfprint |
| Platform | Linux |

## Current Findings

- The sensor responds to the PSK read command (`0xE4`).
- The reported PSK hash does not match the expected value.
- The upstream driver attempts automatic PSK provisioning through command `0xE0` when a mismatch is detected.
- During a modified diagnostic session, the provisioning attempt timed out after five seconds.
- A subsequent PSK hash read still did not match the expected value.
- The diagnostic implementation stopped activation rather than retrying the write.

These observations do not establish whether the firmware is incompatible, whether provisioning is failing for another reason, or whether the device enters an altered state.

## Experimental Work

The `0xF6` GET_IAP_VERSION command has been implemented locally.

The implementation includes:

- Request encoding.
- Response parsing and validation.
- Offline packet and response tests.

**It has not been executed against physical hardware.**

See [Experimental IAP Patch](patches/README.md).

## Research Principles

- No undocumented hardware writes.
- No firmware flashing.
- No automatic PSK provisioning during diagnostic testing.
- Offline testing before hardware testing.
- Clear separation between confirmed observations and hypotheses.
- Preserve original authorship and licensing.

## Repository Structure

- `docs/` — Technical documentation.
- `diagnostics/` — Sanitized diagnostic evidence.
- `patches/` — Experimental code changes.

## Relationship to Upstream

This research builds on the Goodix TLS driver in:

[GuNanOvO/goodix-55x4-linux](https://github.com/GuNanOvO/goodix-55x4-linux)

This is an independent research repository, not an official upstream project.

## License

Code modifications derived from LGPL-2.1-or-later code remain subject to the applicable LGPL terms.

Original copyright notices are preserved.

Original research documentation is licensed under CC BY 4.0.
