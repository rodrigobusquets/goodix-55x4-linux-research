# Hardware Profile

## Identificación

| Property | Value |
|---|---|
| Manufacturer | Goodix |
| USB Vendor ID | `27c6` |
| USB Product ID | `55b4` |
| USB identifier | `27c6:55b4` |
| Firmware | `GF3268_RTSEC_APP_10024` |
| USB interface | Vendor-specific (`0xff`) |
| OUT endpoint | `0x01` |
| IN endpoint | `0x82` |
| Transfer type | Bulk |

## Firmware Identification

The observed firmware identifier is:

`GF3268_RTSEC_APP_10024`

The existing driver recognizes the `GF3268_RTSEC_APP_` family through prefix matching. However, successful operation with other firmware revisions does not establish compatibility with `10024`.

## Communication

The device uses USB bulk transfers and a layered protocol:

1. USB bulk transport.
2. Message Pack framing.
3. Message Protocol framing.
4. TLS-PSK communication after initialization.

## Diagnostic Observations

During the documented diagnostic session:

- The device responded to PSK read command `0xE4`.
- The reported PSK hash did not match the expected value.
- The driver attempted PSK provisioning through `0xE0`.
- The write operation timed out after five seconds.

## Limitations

The available observations do not establish:

- Whether firmware `10024` is fully compatible with the driver.
- Whether the PSK write failure is caused by firmware behavior.
- Whether the sensor requires a different provisioning procedure.
- Whether the device's internal state changed after the timed-out operation.

No firmware update or manual provisioning has been performed as part of this research.

## Safety

Do not send undocumented commands or perform firmware operations on the device without establishing their compatibility and safety first.
