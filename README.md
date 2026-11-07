# Porte-Parole / MEA8000: Apple II peripheral emulation

**Source-only integration and portability package (prototype v0.2).**

This repository is intended to share a C++14 MEA8000 synthesis model and an AppleWin-specific Porte-Parole expansion-card integration, to help developers support this peripheral in other Apple II emulators.

**Status: private review draft, not cleared for public release.** Code provenance, third-party copyright notices, licensing, integration patch application and the full build workflow still require verification. Do not assume that passing synthesis unit tests proves accuracy against physical hardware.

## Planned contents

- `src/Mea8000.h`: synthesis model.
- `src/PorteParole.cpp` and `src/PorteParole.h`: AppleWin card adapter.
- `tests/`: synthesis regression tests and Windows test bridge.
- `applewin/AppleWin-integration.patch`: integration against upstream AppleWin commit `4a43bcdb8e1cb908662f4c270ca84f309a97802f`.
- `docs/`: original technical notes.
- `PORTING.md`, `LICENSING-REVIEW.md`, `INCOMPLETE-EXPORT.md`: porting and review notes.

**No original commercial disk images, voice banks or proprietary software should be uploaded.**

## Standalone synthesis smoke test

```sh
g++ -std=c++14 -O2 -Isrc tests/TestMea8000.cpp -o test_mea8000
./test_mea8000
```

In the local package preparation, the synthesis regression executable reported `PASS: 187 MEA8000 checks`. This is not yet an integrated AppleWin build certification.

## AppleWin

The original working configuration used `-model apple2e -s4 porteparole`. An Apple II software driver hardcoded for slot 4 will not necessarily work with the card in another slot.

The complete source package was prepared separately as `PorteParole-MEA8000-GitHub-Ready.zip`; its source files and supporting documentation still need to be uploaded here.