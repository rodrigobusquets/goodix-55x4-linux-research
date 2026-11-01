# Changelog

All notable changes to this research project will be documented here.

## Unreleased

### Added

- Initial bilingual project documentation (English and Spanish).
- Hardware profile for Goodix USB device `27c6:55b4`.
- Documentation of the PSK mismatch and provisioning timeout.
- Protocol command reference.
- Experimental `GET_IAP_VERSION` (`0xF6`) implementation patch.
- Offline packet encoding and response validation tests.
- Testing, contribution and security guidelines.
- Separate licensing for derived code and original documentation.

### Research Findings

- Identified firmware version `GF3268_RTSEC_APP_10024`.
- Observed a PSK hash mismatch during hardware diagnostics.
- Observed a timeout during the attempted PSK write operation.
- Implemented and tested IAP version handling offline.

### Limitations

- The experimental `0xF6` command has not been tested on physical hardware.
- Firmware compatibility remains unconfirmed.
- The PSK provisioning issue remains unresolved.
- No production-ready driver modifications are provided.
