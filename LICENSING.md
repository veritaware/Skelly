# Licensing

Skelly is a monorepo with **two licenses, assigned per crate**.

| Path | License | Why |
|---|---|---|
| `crates/skelly-editor` | GPL-3.0-or-later | The authoring tool. Improvements to it stay open. |
| `crates/skelly-format` | MIT | The file format and its reference (de)serializer. Anyone may implement it. |
| `crates/skelly-runtime` | MIT | Playback runtime. Safe to embed in any game, open or closed. |
| `crates/skelly-wgpu` | MIT | Reference renderer, usable by games and by the editor. |

The root `LICENSE` is the GPL-3.0 text. It covers the repository as a whole,
including anything not covered by a crate-level `LICENSE`. Each crate directory
contains its own `LICENSE` file, which takes precedence for files inside it.

## Rules

- MIT crates must never depend on GPL/LGPL/AGPL code. The GPL editor may
  depend on MIT crates.
- Every source file starts with an `SPDX-License-Identifier:` line matching
  its crate.
- Contributions are accepted under the license of the crate they touch, with a
  DCO sign-off (`git commit -s`). No CLA.
- Do not copy code from `skelly-editor` into an MIT crate.

## Your own work

Projects, animations and exports you create with the editor are yours and are
not covered by the GPL. Games that embed `skelly-runtime` are not required to
be open source.
