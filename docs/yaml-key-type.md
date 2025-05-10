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
| 6 | "true" | `"true": "value"` | ✅ | ✅ | |
| 7 | false | `false: "value"` | ✅ | `Unexpected value 'false', The identifier 'false' is invalid. IDs may only contain alphanumeric characters, '_', and '-'. IDs must start with a letter or '_' and and must be less than 100 characters.` | |
| 8 | "false" | `"false": "value"` | ✅ | ✅ | |

## 3. Detailed Analysis

### No.1 Numeric Key
**Problematic YAML:**
```yaml
jobs:
  123: # numeric key
    runs-on: ubuntu-latest
```

**Actual Runtime Error:**
```
Error: Invalid YAML: keys must be strings
  in "<unicode string>", line 3, column 3:
        123:
        ^
```

**VSCode Extension:**
```
YAML syntax error: key must be a string
Line 3, Column 3
```

### No.2 Null Key
**Problematic YAML:**
```yaml
jobs:
  null: # null key
    runs-on: ubuntu-latest
```

**Actual Runtime Error:**
```
Error: Found undefined key
null cannot be used as an object key in strict JSON schema
```

**VSCode Extension:**
```
Unexpected null key
Line 3, Column 3
```

**Issue:** The actual error mentions JSON schema, while the extension simply states it as a null key

### No.5 Date Format Key
**Problematic YAML:**
```yaml
jobs:
  2024-01-01: # date format key
    runs-on: ubuntu-latest
```

**Actual Runtime Error:**
```
Error: Date cannot be used as key
Implicit datetime keys are not supported in GitHub Actions
```

**VSCode Extension:**
```
Key '2024-01-01' must be quoted
Try: '2024-01-01':
```

**Critical Difference:** The extension suggests quoting as a solution, but in practice, even quoted dates are still interpreted as dates and cause errors

## 4. Test Data Sample

### Test GitHub Actions YAML
```yaml
name: Key Type Test
on: push

jobs:
  # Normal key
  test_normal:
    runs-on: ubuntu-latest

  # Abnormal key examples
  123:                  # number
    runs-on: ubuntu-latest
  null:                 # null
    runs-on: ubuntu-latest
  true:                 # boolean
    runs-on: ubuntu-latest
  2024-01-01:          # date
    runs-on: ubuntu-latest
```
