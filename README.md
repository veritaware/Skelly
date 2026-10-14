# Skelly

Skelly is a 2D skeletal animation software for game designers.

Rig 2D images onto a skeleton, deform meshes, and animate transforms, opacity,
colour, blend modes and visibility on a timeline. Desktop-first (Windows,
Linux, macOS), written in Rust.

**Status:** pre-alpha, nothing usable yet. See the [roadmap](docs/ROADMAP.md).

## Layout

| Crate | Purpose | License |
|---|---|---|
| [`skelly-format`](crates/skelly-format) | Data format, serialization, versioning | MIT |
| [`skelly-runtime`](crates/skelly-runtime) | Animation evaluation, skinning, constraints | MIT |
| [`skelly-wgpu`](crates/skelly-wgpu) | Reference wgpu renderer | MIT |
| [`skelly-editor`](crates/skelly-editor) | The editor application | GPL-3.0-or-later |

See [LICENSING.md](LICENSING.md) for details.
