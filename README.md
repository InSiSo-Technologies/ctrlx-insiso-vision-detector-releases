# InSiSo Visual Detector — downloads

Snap builds of the **InSiSo Visual Detector** for Bosch Rexroth **ctrlX OS**.

This repository holds published builds only. There is no source code here.

## Download

**[→ Latest release](../../releases/latest)**

| Asset | Device |
|---|---|
| `ctrlx-insiso-vision-detector_<version>_amd64.snap` | ctrlX CORE **X7**, or ctrlX OS on an IPC |
| `ctrlx-insiso-vision-detector_<version>_arm64.snap` | ctrlX CORE **X3** |

Pick by the device's architecture, not by file size. Installing the wrong one
fails at install time rather than silently misbehaving, but it wastes a
download on a slow link.

## Install

**From the ctrlX web interface** — Settings → Apps → *Install from file*, and
pick the `.snap`.

**From a shell on the device:**

```
snap install --dangerous ./ctrlx-insiso-vision-detector_<version>_<arch>.snap
```

`--dangerous` is required because these builds are signed by us rather than
published through the Snap Store. It tells snapd to accept an unasserted
snap; it is not a warning about the contents.

## Licensing

The app installs and runs without a licence, and its features are gated
individually — Camera Connector, Object Detection, Colour Detection,
Coordinate Mapping and the Core Runtime each unlock against their own SKU
through the ctrlX License Manager. An unlicensed installation is a working
installation with locked tabs, not a broken one, so it is safe to install
first and license afterwards.

## What it does

Machine vision on a ctrlX CORE, published into the ctrlX Data Layer so a PLC
or Node-RED reads results directly:

- object detection with an ONNX or Hailo model, and colour detection by HSV
  range, each running as one or more **detectors** — any number of them, each
  bound to its own camera
- results per detector and per class or colour, as arrays, with pixel and
  machine coordinates
- free-run, software-triggered or hardware-triggered capture
- every result carries the number and exposure time of the picture it came
  from, so two results can be proven to be the same instant
- a durable detection history with CSV export

Full release notes, including the Data Layer address changes in 5.0.0, are on
each release.

## Support

Issues and questions: **srishti@insisotech.com**

---

© InSiSo Technologies. All rights reserved. The binaries here are
redistributable for evaluation and for use on licensed ctrlX devices; they
are not open source.
