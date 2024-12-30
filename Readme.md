# `@Jarod42/install-premake5`

Install [premake5](https://premake.github.io/) for your workflow.

## Usage

### Inputs

```yaml
- uses: Jarod42/install-premake5@v3
  with:
    # Alternative premake fork repository to use
    # Optional. Default to 'premake/premake-core'
    repository:

    # The branch, tag or SHA to use
    # Optional. Default to 'v5.0.0-beta4'
    ref:

    # Alternative temporary path where to checkout and build premake
    # Optional. Default to '.premake-build'
    path:

    # For windows, alternative visual to build premake (requires for `run-on windows-2019` to use `msdev: vs2019`)
    # one of vs2019 or vs2022
    # Optional. Default to 'vs2022'
    msdev:
```

## Examples

### Typical default usage on Windows
```yaml
runs-on: windows-latest

steps:
- name: Installing premake5
  uses: Jarod42/install-premake5@v3

- name: Checkout
  uses: actions/checkout@v4

- name: run premake5
  run: premake5 vs2022 --to=solution/vs2022

- name: Add msbuild to PATH
  uses: microsoft/setup-msbuild@v2

- name: build
  run: |
    cd solution/vs2022
    msbuild.exe /property:Configuration=Release MySolution.sln
```

### Typical default usage on Ubuntu:
```yaml
runs-on: ubuntu-latest

steps:
- name: Installing premake5
  uses: Jarod42/install-premake5@v3

- name: Checkout
  uses: actions/checkout@v4

- name: run premake5
  run: premake5 gmake2 --to=solution/gmake2

- name: build
  run: |
    cd solution/gmake2
    make
```

### Typical default usage on MacOS:
```yaml
runs-on: macos-latest

steps:
- name: Installing premake5
  uses: Jarod42/install-premake5@v3

- name: Checkout
  uses: actions/checkout@v4

- name: run premake5
  run: premake5 xcode4 --to=solution/xcode4

- name: build
  run: |
    cd solution/xcode4
    xcodebuild -project MyProject.xcodeproj -configuration Release -scheme MyProject build
```

### Typical default usage on Windows-2019
```yaml
runs-on: windows-2019

steps:
- name: Installing premake5
  uses: Jarod42/install-premake5@v3
  with:
    msdev: 'vs2019'
    
- name: Checkout
  uses: actions/checkout@v4

- name: run premake5
  run: premake5 vs2022 --to=solution/vs2022

- name: Add msbuild to PATH
  uses: microsoft/setup-msbuild@v2

- name: build
  run: |
    cd solution/vs2022
    msbuild.exe /property:Configuration=Release MySolution.sln
```

### Use latest premake version

```yaml
steps:
- name: Installing premake5
  uses: Jarod42/install-premake5@v3
  with:
    ref: 'master'
```
