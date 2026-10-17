# v0.0.18-fork.3
## Fixes
- `build` and watch rescans no longer delete all outputs before they write them
  again. The scan writes each output first and then removes only stale outputs.
  Rojo no longer logs `$path` errors for missing `.model.json` files during a
  rebuild.
- Outputs are written to a temp file and then renamed, so a watcher never reads
  an empty or partial file. Outputs with no change are not written.
- In-place builds (no `--output`) no longer delete outputs that the same scan
  generated.
- A directory created in watch mode now scans the correct output folder.

# v0.0.18-fork.2
## Features
- Imports root-level `$!` static tokens from derived stylesheets at build time,
  allowing themes to derive shared token sheets like `colors.rsml` without
  duplicating static palettes inline.

# v0.0.18-fork.1
## Fixes
- Fixed crash on Windows where `@derive` paths weren't canonicalized to match
  `input_dir`, causing a `StripPrefixError` panic in
  `rsml_to_model_json.rs::resolve_derive`. Same root cause as the v0.0.16 watch
  fix (`std::path::Path::canonicalize` adds a `\\?\` extended-length prefix
  that `dunce::canonicalize` does not), now applied to the build path as well.

# v0.0.18
## Features
- Upgraded `rbx-rsml` version:
    - Fixed tweens not being compiled correctly.

# v0.0.17
## Features
- Upgraded to `rbx-rsml` v1.0.1.

# v0.0.16
## Fixes
- Fixed crash on Windows where VFS event paths weren't canonicalized, causing a `StripPrefixError` during watch mode.

# v0.0.15
## Features
- Added a custom crash message which contains useful information.

# v0.0.14
## Fixes
- Fixed crash on windows due to normalization and canonicalization differing in output.

# v0.0.13
## Fixes
- Properties order when serialized is now deterministic.
- Updated to rsml 0.1.12.

# v0.0.12
## Fixes
Fixed issue where file system events from the build step polluted the watcher leading to .model.json files being immediately deleted after being created in certain scenarios.

# v0.0.11
## Fixes
Derives are now resolved properly when there is no luaurc file.

# v0.0.10
## Fixes
Removed redundant print statement.

# v0.0.9
## Changes
- Adds support for Luaurc aliases in derives. It attempts to find a Luaurc file either at the input directory or the parent of the input directory. You can also manually specify a Luaurc file via the `luaurc` flag.
- Throws an error if the input doesn't exist or isn't a directory.

## Fixes
- Fixed issue where renaming a directory did not update the corresponding `.model.json` files.
- Fixed issue where deleted `rsml` files weren't removed from the internal dependencies map.

# v0.0.8
## Fixes
- Fixed issue where the input directory was cleaned (the removal of redundant .model.json files) on initialisation instead of the output directory.

# v0.0.7
## Fixes
- Fixed issue where moving a .rsml file to another location would not remove the corresponding .model.json
- Fixed issue where redundant rsml .model.json files weren't deleted on initialization.

## Changes
- Added a `build` command.


# v0.0.6
## Fixes
- Fixed issue where derives would not be properly resolved.


# v0.0.5
## Fixes
- Fixed issue where macros from indirect derives were not being imported.

## Changes
- Removed some dead dependencies


# v0.0.4
## Changes
- The `run` command has been renamed to `watch`.
- added a `version` command.
