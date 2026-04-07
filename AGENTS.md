# Repository Guidelines

## Project Structure & Module Organization

This repository is intentionally small:

- [`install.sh`](/home/liu/proj/Gemini-in-Chrome/install.sh): the only executable source file; patches Chrome's `Local State` on macOS and Linux.
- [`README.md`](/home/liu/proj/Gemini-in-Chrome/README.md): user-facing install, restore, and safety documentation.

Keep logic changes in `install.sh` and keep `README.md` in sync whenever behavior, supported platforms, or setup steps change.

## Build, Test, and Development Commands

There is no build system. Use lightweight shell validation before committing:

- `bash -n install.sh`: syntax-check the installer.
- `git diff --check`: catch whitespace errors and malformed patches.
- `shellcheck install.sh`: optional, but recommended if available locally.

When changing patch logic, test against a disposable copy of Chrome's `Local State`, not a live profile.

## Coding Style & Naming Conventions

- Use POSIX-friendly shell where practical; keep the script compatible with `bash`.
- Indent shell blocks with 4 spaces.
- Prefer short functions for risky operations such as process detection and file mutation.
- Keep output messages concise and user-facing.
- Preserve existing file names and top-level layout; this repo does not use nested source directories.

For text replacements, favor readable, narrowly scoped patterns over dense one-liners.

## Testing Guidelines

This project has no automated test suite yet. Minimum verification for every change:

1. Run `bash -n install.sh`.
2. Run `git diff --check`.
3. Confirm README examples still match the current script behavior.

If you change OS detection, process checks, or patch expressions, document the manual test case in the PR.

## Commit & Pull Request Guidelines

Recent history uses short imperative summaries with `fix:` prefixes for follow-up corrections. Prefer:

- `fix: detect Chrome process on Linux`
- `docs: update install instructions`

Open PRs from a feature branch, not `master`. PR titles and descriptions should be in English and include:

- a short summary of user-visible changes
- verification steps run locally
- any limitations or manual follow-up needed

Do not force-push after opening a PR; add follow-up commits instead.
