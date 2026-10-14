# Skelly Roadmap

## Vision

An open-source 2D skeletal animation tool in the vein of Spine, Spriter Pro,
Rive and COA Tools 2: rig 2D images with bones and meshes, then animate
deformation, opacity, blend modes and visibility on a timeline. The editor is
GPL-3.0; the format and runtimes are MIT so any game can embed them.

## Tech stack

| Layer | Choice |
|---|---|
| Language | Rust |
| Rendering | wgpu (Vulkan / Metal / DX12, GL fallback) |
| UI | egui (`eframe`) + `egui_dock` |
| Geometry | `lyon`, `earcutr`, `spade` |
| Images | `image`, `psd` (later `resvg`) |
| Serialization | `serde`; JSON project format, compact binary export |
| Packaging | AppImage/Flatpak, MSI, dmg via GitHub Actions |
| Testing | `cargo test`, headless wgpu golden-image tests, property tests |

Architecture rule: the editor is a thin shell. Evaluation, skinning and
rendering live in the MIT crates so the editor shows exactly what runtimes
will show. Runtime crates stay WASM-friendly, but a web runtime is not a goal
for now.

## MVP (v0.1)

**Goal:** import images, rig a character, animate it, and play it back in a
game using the runtime.

In scope:
- PNG import into a slot/attachment hierarchy (PSD layers as a stretch goal).
- Bones: create, parent, edit rotate / translate / scale / shear.
- Region attachments, then free-form meshes with manual vertices.
- Weight painting and linear blend skinning.
- Per-slot visibility, opacity and colour tint.
- Blend modes: normal, additive, multiply, screen.
- Timeline: keyframes, dopesheet, linear / stepped / bezier interpolation,
  multiple animations, scrubbing and playback.
- Undo/redo everywhere; save/load project (JSON); export to runtime format.
- Reference runtime (Rust, C ABI) and a demo player.

Deferred: IK / path constraints, effects and filters, state machines, skins,
events, physics, atlas packing optimizations, Spine / DragonBones import,
web runtime.

## Milestones

| # | Milestone | Outcome |
|---|---|---|
| M0 | Foundations | Workspace, licenses, CI on 3 OSes, `cargo-deny`, window with wgpu viewport and docking panels. Validates egui's risk areas early. |
| M1 | Document model and format | Bones, slots, region attachments, versioned JSON schema, command/undo system. |
| M2 | Rig editing | Image import, bone creation and gizmos, hierarchy and inspector panels, posed skeleton rendering. |
| M3 | Animation | Timeline, keyframes (transform, colour/opacity, visibility), bezier curves, playback. Evaluator lives in `skelly-runtime`. |
| M4 | Meshes and deformation | Mesh editing, auto-mesh from alpha contours, weight painting, skinning, mesh vertex (FFD) keyframes. |
| M5 | Blend modes and render pipeline | Offscreen passes, blend modes, clipping masks, golden-image tests. |
| M6 | Export and runtime | Binary export, runtime API with C ABI, demo player, format specification. |
| M7 | Polish and v0.1 release | Packaging for all platforms, autosave and crash recovery, sample projects, docs. |

Post-MVP, in priority order: IK and transform constraints, skins, events,
effects (blur, glow, ... as post passes), state machines, Unity / Godot / Web
runtimes.

## Risks

1. **Timeline and curve editor.** The most custom UI in the project. M0-M3 will
   show whether egui is adequate; the UI layer is thin enough to replace.
2. **Weight painting UX.** Highest value and highest effort; M4 is the most
   likely to slip.
3. **Format stability.** Breaking the format after people author content is
   costly. Version and plan migrations from M1.
4. **License hygiene.** MIT crates must not pick up GPL dependencies or code
   from the editor. Enforce with `cargo-deny` in CI.
