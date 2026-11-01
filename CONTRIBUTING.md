# Contributing Guidelines

Thank you for your interest in contributing to this research project.

The goal is to improve understanding of Goodix fingerprint sensors, their firmware, communication protocols and Linux driver compatibility through reproducible and responsible investigation.

## 1. General Principles

Contributions should prioritize:

- Technical accuracy.
- Reproducibility.
- Clear documentation.
- Respect for original authorship and licenses.
- Non-destructive experimentation.
- Transparency about limitations and uncertainty.

## 2. Reporting Issues

When reporting a problem, include as much relevant information as possible:

- USB Vendor ID and Product ID.
- Sensor firmware version.
- Linux distribution and kernel version.
- libfprint version or source revision.
- Relevant build and test results.
- Sanitized diagnostic logs.
- Steps required to reproduce the issue.

Do not include passwords, private keys, personal information or unnecessary device identifiers.

## 3. Hardware Safety

This project does not encourage undocumented or potentially destructive hardware operations.

Contributors must not assume that a command is safe simply because it is described as a read or query operation.

Before proposing hardware tests, document:

- The command's purpose.
- Its expected behavior.
- Whether it can modify persistent device state.
- Firmware compatibility requirements.
- Potential failure modes.
- Recovery options, if applicable.

Do not recommend firmware flashing, PSK provisioning or undocumented writes without sufficient technical evidence.

## 4. Code Contributions

Code contributions should:

- Follow the existing project's coding conventions.
- Preserve original copyright notices.
- Include appropriate error handling.
- Avoid unnecessary changes outside the intended scope.
- Include offline tests whenever possible.
- Clearly identify experimental functionality.

Do not claim hardware compatibility based exclusively on successful compilation or offline tests.

## 5. Documentation Contributions

Documentation should distinguish between:

- Confirmed observations.
- Source-code findings.
- Experimental results.
- Hypotheses.
- Unresolved questions.

Include references whenever findings originate from external projects or technical reports.

## 6. Testing Requirements

Before submitting code changes:

1. Review the proposed changes.
2. Build the modified source.
3. Run relevant offline tests.
4. Report the exact results.
5. Document any untested behavior.

Physical hardware testing is not a prerequisite for contributing.

## 7. Pull Requests

Pull requests should include:

- A concise description of the change.
- The technical motivation.
- Relevant evidence or references.
- Tests performed.
- Known limitations.
- Hardware testing status.

Small, focused contributions are preferred.

## 8. Licensing

Contributors must ensure that submitted material can legally be distributed under the applicable license.

Code derived from the upstream LGPL-licensed driver must preserve its original copyright notices and applicable licensing obligations.

Documentation and independently authored research material follow the licenses specified in this repository.

## 9. Research Integrity

Do not present assumptions as established facts.

Do not claim that a problem has been solved without sufficient evidence.

Negative results, timeouts and unsuccessful experiments are valuable contributions when documented accurately.

Thank you for helping make Linux fingerprint support more transparent and reliable.
