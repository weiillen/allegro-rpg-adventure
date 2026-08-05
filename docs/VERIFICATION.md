# Verification Record

Verification was limited to checks that do not modify the submitted implementation.

## Checks completed

- Parsed `last_dance.vcxproj`, `last_dance.vcxproj.filters`, and `packages.config` as XML.
- Confirmed that all source/header paths referenced by the Visual Studio project exist.
- Validated all 25 preserved PNG files with an image decoder.
- Probed all 15 preserved audio files with `ffprobe`.
- Parsed the map header and confirmed a 19 × 21 grid containing exactly 399 cells.
- Confirmed that the map contains one player spawn, two slime spawns, and four coin tiles.
- Recomputed SHA-256 hashes after copying and confirmed byte identity for every artifact listed in `ORIGINAL_FILE_MANIFEST.tsv`.

## Build status

A complete compile/run test was not performed in the artifact environment because the Allegro development package and the Visual Studio/NuGet toolchain used by the original project were not available. The repository therefore does **not** claim a fresh successful build.

The original archive contains Visual Studio object files and logs indicating that it had previously been built in an x64 Debug environment, but generated outputs are not treated as independent proof of current reproducibility.
