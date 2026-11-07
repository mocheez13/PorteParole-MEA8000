# Porte-Parole / MEA8000: Apple II peripheral emulation

**Source-only integration and portability package (prototype v0.2).**

This repository candidate contains an independently written, header-only C++14 MEA8000 synthesis model and a Porte-Parole expansion-card integration for an AppleWin fork. The goal is to help developers integrate the peripheral into other Apple II emulators. **No original commercial disk images, voice banks, or software are included.**

## Contents

- `src/Mea8000.h` — standalone synthesis device model.
- `src/PorteParole.cpp` and `src/PorteParole.h` — AppleWin-specific card implementation: slot I/O, CPU cycle synchronization, DirectSound, save state.
- `tests/TestMea8000.cpp` — portable regression tests for the synthesis model.
- `tests/MeaBridge.cpp` — Windows DLL bridge used in the original testing workflow; requires MSVC and is not portable as-is.
- `applewin/AppleWin-integration.patch` — AppleWin-specific registration, CLI and build-file changes.
- `docs/` — original technical notes, retained as supplied. `PorteParole.md` contains pre-existing character-encoding corruption.
- `PORTING.md`, `LICENSING-REVIEW.md`, `INCOMPLETE-EXPORT.md` — integration and release notes.

## Quick check (Linux/macOS with g++)

```sh
g++ -std=c++14 -O2 -Isrc tests/TestMea8000.cpp -o test_mea8000
./test_mea8000
```

Observed on package preparation: `PASS: 187 MEA8000 checks`. This checks software behavior, not complete analog fidelity to a real chip or integrated AppleWin behavior.

## AppleWin integration

Target upstream revision: `4a43bcdb8e1cb908662f4c270ca84f309a97802f`. Apply the patch to a **clean separate checkout** of that revision and copy the three files in `src/` to its `source/` directory. Read `applewin/../docs/PATCH-NOTES.md` and the original technical documentation.

With a compatible build, the original test launch used `-model apple2e -s4 porteparole` (Porte-Parole in slot 4). Behavior in another slot depends on the software's slot addressing.

**Status:** testable draft for review; not yet confirmed ready for public release. See `LICENSING-REVIEW.md` and `INCOMPLETE-EXPORT.md`.
