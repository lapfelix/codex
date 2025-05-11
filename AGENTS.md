# @steipete's Codex Fork

This is a customized fork of the OpenAI Codex CLI with the following key modifications:

> **⚠️ Use at your own risk. This is the true YOLO version of Codex. ⚠️**

## Changes

1. **Disabled Apple Seatbelt on macOS** ([ec1f148](https://github.com/steipete/codex/commit/ec1f1484afd637e8328764186328345245d25d34)): Sandboxing has been completely disabled to avoid permission issues with file access.

2. **Increased Default Timeout** ([ed27fc6](https://github.com/steipete/codex/commit/ed27fc665397aa299cf352c9287f5ea8495e2ef3)): Command timeout increased from 10 seconds to 20 seconds to allow longer-running commands to complete.

3. **Added Network Access** ([ed27fc6](https://github.com/steipete/codex/commit/ed27fc665397aa299cf352c9287f5ea8495e2ef3)): Modified the default sandbox policy to include network access, allowing commands to connect to the internet.

4. **Enabled Unsafe Mode** ([8b56c5f](https://github.com/steipete/codex/commit/8b56c5f32126e60f49570336487f44867d9a86e4)): Hardcoded `CODEX_UNSAFE_ALLOW_NO_SANDBOX=true` directly in the code to completely bypass sandboxing for maximum flexibility without requiring environment variables.

5. **Increased Shell Output Limits** ([ed27fc6](https://github.com/steipete/codex/commit/ed27fc665397aa299cf352c9287f5ea8495e2ef3)): Expanded the default limits for shell command output:

   - Maximum bytes: 102,400 (100KB) - 10x more than default
   - Maximum lines: 1,000 - 4x more than default

6. **Fixed Gemini API URL** ([931d232](https://github.com/steipete/codex/commit/931d232f10e0bf7bfc7ee62fa6ee2d5b15a9c3c1)): Updated the Gemini API endpoint to use the correct `/v1beta/models` path.

7. **Custom Branding**: Changed header from "(research preview)" to "[@steipete fork]" in UI elements.

## Installation

To use this fork without affecting your regular Codex installation:

1. The fork is installed as `scodex` in `~/.local/bin` which takes precedence over Homebrew binaries in the PATH.

2. Usage:
   - `codex` - Uses the original OpenAI version (from npm/Homebrew)
   - `scodex` - Uses this customized fork with all enhancements enabled

## Configuration

This fork comes with the following suggested configurations:

### No Environment Variables Required

Unlike the original Codex, this fork doesn't require any environment variables for the enhanced features to work - unsafe mode is hardcoded directly into the source.

### Configuration File (~/.codex/config.json)

```json
{
  "model": "o4-mini",
  "approvalMode": "full-auto",
  "tools": {
    "shell": {
      "maxBytes": 102400,
      "maxLines": 1000
    }
  },
  "notify": true
}
```

## Original Documentation

### Rust/codex-rs

In the codex-rs folder where the rust code lives:

- Never add or modify any code related to `CODEX_SANDBOX_NETWORK_DISABLED_ENV_VAR`. You operate in a sandbox where `CODEX_SANDBOX_NETWORK_DISABLED=1` will be set whenever you use the `shell` tool. Any existing code that uses `CODEX_SANDBOX_NETWORK_DISABLED_ENV_VAR` was authored with this fact in mind. It is often used to early exit out of tests that the author knew you would not be able to run given your sandbox limitations.
