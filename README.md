# resigrok

A Rust reimplementation of [libsigrok](https://github.com/sigrokproject/libsigrok): hardware access for logic analyzers, oscilloscopes, multimeters and other test and measurement gear, plus input/output file format support.

## Architecture

```
 hardware ──► parsers
    │
    ├──────► transport ──► core
    └──────────────────────► core
 input / output / transform ─► core
```

Drivers emit typed packets into a session. The session routes them through transforms to outputs and frontends.

| Module      | Role                                                        |
|-------------|-------------------------------------------------------------|
| `core`      | Session, datafeed packets, device/channel model, config keys, triggers. No I/O. |
| `transport` | Serial, USB, SCPI, Bluetooth, HID                           |
| `parsers`   | Pure protocol/chip parsers (DMM, LCR, scale)                |
| `hardware`  | Device drivers                                              |
| `input`     | File format readers                                         |
| `output`    | File format writers                                         |
| `transform` | Mid-stream datafeed transforms                              |
| `error`     | Crate-wide error type                                       |
