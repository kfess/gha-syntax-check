# GitHub Actions Runner Support Status

This document summarizes the support status of various GitHub Actions runner environments as of May 2025.

[GitHub Actions Result](https://github.com/kfess/gha-syntax-check/actions/runs/14941228853/job/41978537750)

## Test Results

| Runner | Status | Reason |
|---------|------|------|
| **Linux (x64)** |  |  |
| `ubuntu-16.04` | ❌ Unavailable | [End of support](https://github.com/actions/runner-images/issues/3287) |
| `ubuntu-18.04` | ❌ Unavailable | [End of support](https://github.com/actions/runner-images/issues/6002) |
| `ubuntu-20.04` | ❌ Unavailable | [Support just ended in April 2025](https://github.com/actions/runner-images/issues/11101) |
| `ubuntu-22.04` | ✅ Available | Currently supported |
| `ubuntu-24.04` | ✅ Available | Currently supported |
| `ubuntu-latest` | ✅ Available | Currently supported (points to `ubuntu-24.04`) |
| **Linux (ARM64)** |  |  |
| `ubuntu-16.04-arm` | ❌ Unavailable | Runner does not exist |
| `ubuntu-18.04-arm` | ❌ Unavailable | Runner does not exist |
| `ubuntu-20.04-arm` | ❌ Unavailable | Runner does not exist |
| `ubuntu-22.04-arm` | ✅ Available | Currently supported |
| `ubuntu-24.04-arm` | ✅ Available | Currently supported |
| **Windows** |  |  |
| `windows-2019` | ✅ Available | Currently supported |
| `windows-2022` | ✅ Available | Currently supported |
| `windows-2023` | ❌ Unavailable | Runner does not exist |
| `windows-2024` | ❌ Unavailable | Runner does not exist |
| `windows-2025` | ✅ Available | Currently supported |
| `windows-latest` | ✅ Available | Currently supported (points to `windows-2022`) |
| `windows-11-arm` | ✅ Available | Currently supported (Public Preview) |
| **macOS (Standard)** |  |  |
| `macos-10.15` | ❌ Unavailable | End of support |
| `macos-11` | ❌ Unavailable | End of support |
| `macos-12` | ❌ Unavailable | End of support |
| `macos-13` | ✅ Available | Currently supported (Intel) |
| `macos-14` | ✅ Available | Currently supported (ARM64) |
| `macos-15` | ✅ Available | Currently supported (ARM64) |
| `macos-latest` | ✅ Available | Currently supported (points to `macos-14`, ARM64) |
| **macOS (Larger Runners)** |  |  |
| `macos-13-large` | 💰 Available but not tested due to billing | Requires billing setup (Intel) |
| `macos-13-xlarge` | 💰 Available but not tested due to billing | Requires billing setup (ARM64) |
| `macos-14-large` | 💰 Available but not tested due to billing | Requires billing setup (ARM64) |
| `macos-14-xlarge` | 💰 Available but not tested due to billing | Requires billing setup (ARM64) |
| `macos-15-large` | 💰 Available but not tested due to billing | Requires billing setup (ARM64) |
| `macos-15-xlarge` | 💰 Available but not tested due to billing | Requires billing setup (ARM64) |
| `macos-latest-large` | 💰 Available but not tested due to billing | Requires billing setup (ARM64) |
| `macos-latest-xlarge` | 💰 Available but not tested due to billing | Requires billing setup (ARM64) |
| **macOS (Unofficial ARM64 Format)** |  |  |
| `macos-13-arm64` | ❌ Unavailable | Runner does not exist |
| `macos-14-arm64` | ❌ Unavailable | Runner does not exist |
| `macos-15-arm64` | ❌ Unavailable | Runner does not exist |

## Status Explanation

- ✅ **Available**: Runner works properly and can execute jobs
- ❌ **Unavailable**: Runner cannot be used due to end of support or other reasons (remain in queue indefinitely)
- 💰 **Available but not tested due to billing**: Runner exists but requires billing setup to run (considered available)

## Notes

- Larger runners for ubuntu and Windows are not included in this document.