[![test](https://github.com/KnicKnic/os-specific-run/workflows/test/badge.svg?branch=master&event=push)](https://github.com/KnicKnic/os-specific-run/actions?query=branch%3Amaster++event%3Apush+)
# os-specific-run 

A github action for running a separate command based on the os

```yaml
    - uses: knicknic/os-specific-run@v1.0.3
      with:
        macos: echo "Hi from macos"
        linux: |
          echo "Hi from linux"
          echo "Hi from linux second line"
        windows: echo "Hi from windows"
```

## Params

### (optional) Command you wish to run
| os      | command value                           |
|---------|-----------------------------------------|
| macos   | echo "No command specified for macos"   |
| linux   | echo "No command specified for linux"   |
| windows | echo "No command specified for windows" |

### (optional) Shell you wish to use
| os      | command value                           |
|---------|-----------------------------------------|
| macosShell   | bash |
| linuxShell   | bash |
| windowsShell | pwsh |

See https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#using-a-specific-shell for more details

## Full Example

```yaml
name: test

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: ["ubuntu-latest", "windows-latest", "macos-latest"]
    steps:
    - uses: actions/checkout@v2

    - uses: knicknic/os-specific-run@v1
      with:
        macos: echo "Hi from macos"
        linux: |
          echo "Hi from linux"
          echo "Hi from linux second line"
        windows: echo "Hi from windows"
```

## Alternatives

You can do what this project accomplishes with simple `if` statements in github actions.

The problem is you have to figure them out, and they end up creating multiple steps one per each OS. I think a single step (rather than multiple steps in each OS that are not run) looks cleaner and is more obvious what failed. More details on if statements - https://github.community/t/what-is-the-correct-if-condition-syntax-for-checking-matrix-os-version/16221/4

## Developer instructions

### Setup Environment

```pwsh
npm i -g @vercel/ncc
npm install
```

### Update project

```pwsh
ncc build index.js
```
