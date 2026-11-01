# References and Sources

## 1. Upstream Repository

**Project:** goodix-55x4-linux

**Author:** GuNanOvO

**Repository:** https://github.com/GuNanOvO/goodix-55x4-linux

This repository is the primary source for the Goodix TLS driver implementation examined in this research.

Relevant material includes:

- Goodix TLS driver source code.
- USB communication and protocol implementation.
- PSK provisioning logic.
- Firmware version handling.
- Technical documentation.
- Existing Python implementation.

This research is independent and is not an official upstream project or a replacement for the original repository.

## 2. libfprint

**Project:** libfprint

**Repository:** https://gitlab.freedesktop.org/libfprint/libfprint

libfprint provides the fingerprint reader framework into which the Goodix TLS driver is integrated.

It is relevant for understanding:

- Driver architecture.
- Device initialization.
- USB communication lifecycle.
- Enrollment and device management.
- Build and testing infrastructure.

## 3. Goodix Device Identification

**USB Vendor ID:** `27c6`

**USB Product ID:** `55b4`

**Observed firmware:** `GF3268_RTSEC_APP_10024`

These identifiers were obtained during the investigation of the physical device.

The firmware identification should not be interpreted as proof of full compatibility with the upstream driver.

## 4. Related Technical Reports

Additional information may be found in the upstream repository's issue tracker:

https://github.com/GuNanOvO/goodix-55x4-linux/issues

Existing reports are useful for comparing firmware versions, initialization behavior and hardware observations.

However, behavior reported for another device or firmware revision must not automatically be attributed to the device examined here.

## 5. Original Diagnostic Evidence

The investigation includes:

- Source revision information.
- Local library linkage verification.
- PSK diagnostic output.
- Offline packet tests.

Diagnostic evidence should be interpreted within its documented scope.

In particular, a timeout does not establish whether a command was partially or fully processed by the sensor.

## 6. Attribution and Independence

This research builds upon publicly available work by other developers.

Original code, copyright notices and applicable licenses must be preserved when distributing modified source code.

All findings, experimental implementations and conclusions published here should be distinguished from upstream claims.

This repository is an independent research effort. It is not affiliated with or endorsed by Goodix, libfprint maintainers or the authors of the upstream driver.
