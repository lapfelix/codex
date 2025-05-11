# Steipete's Codex Fork

This is a customized fork of the OpenAI Codex CLI with the following key modifications:

## Changes

1. **Disabled Apple Seatbelt on macOS**: Sandboxing has been completely disabled to avoid permission issues with file access.

2. **Increased Default Timeout**: Command timeout increased from 10 seconds to 20 seconds to allow longer-running commands to complete.

3. **Added Network Access**: Modified the default sandbox policy to include network access, allowing commands to connect to the internet.

4. **Custom Branding**: Changed header from "(research preview)" to "[steipete fork]" in UI elements.

## Installation

To use this fork without affecting your regular Codex installation:

1. The fork is installed as `scodex` in `~/.local/bin` which takes precedence over Homebrew binaries in the PATH.

2. Usage:
   - `codex` - Uses the original OpenAI version (from npm/Homebrew)
   - `scodex` - Uses this customized fork with Seatbelt disabled and increased timeouts

## Original Documentation

### Rust/codex-rs

In the codex-rs folder where the rust code lives:

- Never add or modify any code related to `CODEX_SANDBOX_NETWORK_DISABLED_ENV_VAR`. You operate in a sandbox where `CODEX_SANDBOX_NETWORK_DISABLED=1` will be set whenever you use the `shell` tool. Any existing code that uses `CODEX_SANDBOX_NETWORK_DISABLED_ENV_VAR` was authored with this fact in mind. It is often used to early exit out of tests that the author knew you would not be able to run given your sandbox limitations.
