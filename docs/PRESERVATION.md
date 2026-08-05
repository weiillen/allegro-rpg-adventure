# Preservation Policy

The portfolio repository was assembled without editing the original project artifacts.

## Included unchanged

- every `.c` and `.h` file under `Src/`;
- every image, audio file, font, and map file under `Assets/`, except the macOS `.DS_Store` metadata file;
- `last_dance.vcxproj`;
- `last_dance.vcxproj.filters`;
- `packages.config`.

These files were copied byte-for-byte. Their SHA-256 values are recorded in `ORIGINAL_FILE_MANIFEST.tsv`.

## Added documentation and repository support

- `README.md`;
- files under `docs/`;
- `.gitignore`;
- `.gitattributes`;
- `ORIGINAL_FILE_MANIFEST.tsv`.

## Excluded generated or machine-specific files

- `.DS_Store`;
- `last_dance.vcxproj.user`;
- `x64/Debug/` object files and Visual Studio build outputs;
- `last_dance.log` and `log.txt` runtime/build logs.

Exclusion of these files does not change the source implementation or the runtime assets. No source code was refactored, fixed, reformatted, or renamed.
