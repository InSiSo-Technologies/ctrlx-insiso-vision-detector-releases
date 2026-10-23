# InSiSo Visual Detector — downloads

Snap builds of the **InSiSo Visual Detector** for Bosch Rexroth **ctrlX OS**.

This repository holds published builds only. There is no source code here.

## Which version

**The first number is the ctrlX OS major version the build is for**: 4.x.x
runs on ctrlX OS 4.x. The other two numbers count releases: 4.7.19 would be a
fix, 4.8.0 a new function.

4.7.18 is the first build numbered this way. Earlier test builds went up to
7.2.17, and **all of them are older than 4.7.18**, even though their numbers
are higher. Delete old snap files so the newest is clear.

## Download

**[→ Latest release](../../releases/latest)**

| Asset | Device | Carries |
|---|---|---|
| `ctrlx-insiso-vision-detector_<version>_amd64.snap` | ctrlX CORE **X5**, **X7**, a ctrlX **IPC** (with or without the NVIDIA extension), ctrlX OS in a VM | Hailo-8 support and the NVIDIA GPU runtime, so over 3 GB |
| `ctrlx-insiso-vision-detector_<version>_arm64.snap` | ctrlX CORE **X3** | Hailo-8 support |

Pick by the device's architecture, not by file size. A snap installs only on
the architecture it was built for. On a device without an NVIDIA GPU, the
amd64 snap's GPU runtime is not used.

GitHub accepts release files up to 2 GiB, and the amd64 snap is larger than
that. If a release has no amd64 snap attached, ask
**srishti@insisotech.com** for a download link.

Each release lists the SHA-256 of its files (`SHA256SUMS`). To check a
download on Windows, run `Get-FileHash <file>.snap` in PowerShell. On Linux,
run `sha256sum <file>.snap`.

## Install

**From the ctrlX web interface:** switch the device to Service mode. Then go
to Settings → Apps → *Install from file* and pick the `.snap`. These builds
do not come from the ctrlX Store, so the device must allow installation from
an unknown source.

**From a shell on the device:**

```
snap install --dangerous ./ctrlx-insiso-vision-detector_<version>_<arch>.snap
```

`--dangerous` is needed because these builds do not come through a store, so
snapd has no store signature for them. It is not a warning about the
contents.

**Updating:** install the new file over the old one. Settings, cameras,
models and calibration are kept. Then **reboot the device once**: this frees
any licence seats the previous version still held.

## Licensing

The app installs and runs without a licence, and each function unlocks
through the ctrlX License Manager (Settings → Apps & Licenses). An unlicensed
installation works, with its functions locked, so it is safe to install
first and license afterwards.

- **Runtime** is required: every other function needs it.
- **Add-ons:** Camera Connector (one per camera), Color Detection, Object
  Detection, Machine Coordinate Transformation, Code Reading, 3D
  Dimensioning, Parcel Tracking.
- **Packages:** Vision Guidance Package and Parcel Tracking Package. Each
  includes the Runtime.

## What it does

Machine vision on ctrlX OS, with every result published in the ctrlX Data
Layer, so a PLC or Node-RED reads it directly:

- **Cameras:** GigE Vision and USB3 Vision, 2D and 3D. A camera can run
  free, be triggered by the PLC over the Data Layer, or be triggered by a
  hardware pulse.
- **Color Detection:** colors by range, one detector per camera, with
  positions and sizes in camera pixels.
- **Object Detection:** `.onnx` models on the CPU or an NVIDIA GPU, and
  `.hef` models on a Hailo-8 module.
- **Coordinate Mapping:** detected objects in machine millimetres.
- **Code Reading:** Data Matrix and Code 128.
- **3D Dimensioning:** length, breadth and height from a time-of-flight
  camera.
- **Detection History**, with CSV export.

**The Data Layer** is one folder, `insiso/visual-detector`. A PLC writes a
value to `trigger` and reads the results under `picture/`, `color/`,
`object/` and `coordinates/`. Every result carries `picture/id`, a counter,
so values from the same picture can be matched. Every button in the web
pages also has a node under `command`. The app's Help page lists every node
and command.

## Support

Issues and questions: **srishti@insisotech.com**

---

© InSiSo Technologies. All rights reserved. The binaries here are
redistributable for evaluation and for use on licensed ctrlX devices; they
are not open source.
