# PSK Investigation

## Background

The Goodix TLS driver uses a pre-shared key (PSK) during its communication initialization.

The current implementation checks the device's PSK against the expected value. When the values do not match, the driver may attempt to provision the expected PSK automatically.

This behavior is relevant because an automatic provisioning attempt can modify the sensor's internal state.

## Observed Behavior

The diagnostic session was performed using:

- USB device: `27c6:55b4`
- Firmware: `GF3268_RTSEC_APP_10024`
- Driver: locally compiled Goodix TLS implementation
- PSK write timeout: 5 seconds
- Finger placement: no finger was placed on the sensor.

The relevant sequence was:

1. The driver sent PSK read command `0xE4`.
2. The command completed successfully.
3. The returned PSK hash did not match the expected value.
4. The driver initiated PSK write command `0xE0`.
5. The write operation timed out after five seconds.
6. A subsequent PSK read completed, but the hash still did not match.
7. The diagnostic implementation stopped activation.

## What This Establishes

The available evidence establishes that:

- The sensor responded to the PSK read command.
- The reported PSK hash differed from the expected value.
- A PSK write operation was initiated.
- The write operation did not complete within the configured timeout.
- The subsequent read did not show the expected PSK hash.

## What This Does Not Establish

The evidence does not establish:

- That the sensor successfully stored a new PSK.
- That the sensor's internal state remained unchanged.
- That firmware `GF3268_RTSEC_APP_10024` is incompatible with the driver.
- That the timeout is caused by the firmware rather than transport, protocol, or device state.
- That the PSK mismatch is the root cause of the initialization failure.

A timeout is not proof that a write was never processed. Likewise, a mismatched readback does not identify the underlying cause.

## Safety Considerations

PSK provisioning must be treated as a potentially state-changing operation.

For this reason, this research follows these restrictions:

- No repeated PSK write attempts.
- No automatic provisioning during diagnostic testing.
- No firmware flashing.
- No attempts to bypass the PSK verification process.
- No further hardware commands without a documented safety assessment.

## Current Status

<badge color="warning">Unresolved</badge>

The PSK mismatch and write timeout remain unexplained.

The next steps should prioritize non-destructive protocol investigation and confirmation of firmware compatibility with the driver maintainers.
