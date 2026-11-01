# Security Policy

## Scope

This repository investigates Goodix fingerprint sensors, their firmware, communication protocols and Linux driver implementations.

Security considerations include:

- TLS-PSK communication.
- PSK provisioning and verification.
- USB protocol handling.
- Firmware identification and compatibility.
- Device initialization and persistent state changes.
- Potential vulnerabilities in the driver or communication protocol.

## Reporting a Security Issue

Please do not publish sensitive vulnerability details, credentials, private keys or potentially exploitable information in public issues.

For security-sensitive reports, use GitHub's private vulnerability reporting feature if it is enabled for this repository.

If private reporting is unavailable, contact the repository maintainers through an appropriate private channel before disclosing sensitive technical details.

Include:

- A concise description of the issue.
- Affected hardware and firmware versions.
- Relevant source-code references.
- Reproduction conditions.
- Potential impact.
- Available mitigations.

Do not include personal information or unrelated device identifiers.

## Responsible Disclosure

Please allow time for investigation before publicly disclosing vulnerabilities.

Reports should distinguish between confirmed vulnerabilities, suspected weaknesses and theoretical risks.

A protocol timeout, failed initialization or PSK mismatch does not automatically constitute a security vulnerability.

## Experimental Code

Experimental implementations must not be assumed safe for production use.

In particular:

- Do not assume undocumented commands are harmless.
- Do not execute unverified provisioning operations.
- Do not flash firmware without a documented recovery procedure.
- Do not expose PSKs, private keys or authentication material in logs.
- Do not install experimental drivers system-wide without understanding their behavior.

## Known Research Limitations

The current research has not established:

- Whether the PSK provisioning behavior is vulnerable.
- Whether the observed PSK mismatch has security implications.
- Whether the experimental `0xF6` command is compatible with the investigated firmware.
- Whether undocumented commands can modify persistent device state.

These questions remain open and require further evidence.

## Supported Versions

This repository is currently an experimental research project.

There are no production releases or security maintenance guarantees at this stage.
