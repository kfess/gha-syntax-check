# GitHub Actions YAML Key Type Error Validation Report

## 1. Overview

### Purpose

To validate the consistency between actual runtime error messages and VSCode extension error messages when using inappropriate types (number, null, date, etc.) as keys in GitHub Actions YAML files.

### Test Environment

- **Test Date**: YYYY/MM/DD
- **VSCode Version**: x.x.x
- **GitHub Actions Extension Version**: x.x.x
- **GitHub Actions Runner**: ubuntu-latest

## 2. Key Type Error Comparison Results

| No. | Key Type | YAML Example | Actual Runtime Error | VSCode Extension Error | Notes |
|-----|----------|--------------|---------------------|----------------------|-------|
| 1 | string | `"1": "value"` | `The identifier '1' is invalid. IDs may only contain alphanumeric characters, '_', and '-'. IDs must start with a letter or '_' and and must be less than 100 characters.` | `The identifier '1' is invalid. IDs may only contain alphanumeric characters, '_', and '-'. IDs must start with a letter or '_' and and must be less than 100 characters.` | ✅ |
| 2 | number | `1: "value"` | `The identifier '1' is invalid. IDs may only contain alphanumeric characters, '_', and '-'. IDs must start with a letter or '_' and and must be less than 100 characters.` | `i.indexOf is not a function` | Error Message in VSCode Extension is not appropriate |
| 3 | "null" | `"null": "value"` | ✅ | ✅ | ✅ |
| 4 | null | `null: "value"` | `Unexpected value ''` | `Unexpected value 'null'` | Error Message in VSCode Extension is not appropriate |
| 5 | true | `true: "value"` | ✅ | `i.indexOf is not a function` | |
| 6 | "true" | `"true": "value"` | ✅ | ✅ | ✅ |
| 7 | false | `false: "value"` | ✅ | `Unexpected value 'false', The identifier 'false' is invalid. IDs may only contain alphanumeric characters, '_', and '-'. IDs must start with a letter or '_' and and must be less than 100 characters.` | |
| 8 | "false" | `"false": "value"` | ✅ | ✅ | ✅ |
| 9 | undefined | `undefined: "value"` | ✅ | ✅ | ✅ |
| 10 | ~ | `~: "value"` | `Unexpected value ''` | `Unexpected value 'null', The identifier 'null' is invalid. IDs may only contain alphanumeric characters, '_', and '-'. IDs must start with a letter or '_' and and must be less than 100 characters.` | |
| 11 | 0 | `0: "value"` | `Unexpected value '0', The identifier '0' is invalid. IDs may only contain alphanumeric characters, '_', and '-'. IDs must start with a letter or '_' and and must be less than 100 characters.` | Error Message in VSCode Extension is not appropriate |

## 3. Hypothesis

- キーが 0 以外の数値の場合
- キーが 0 として扱われる場合
- キーが null の場合 -> '' として扱われる