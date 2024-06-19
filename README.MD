<div align="center">
  <a href="https://github.com/Reloaded-Project/devops-rust-test-in-wine" target="_blank">
    <img src="assets/reloaded-logo.png" alt="Reloaded Logo" width="100"/>
  </a>

  <h1 align="center">Reloaded Test Rust on Wine Action</h1>

  <p>
    <a href="LICENSE">
      <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License">
    </a>
  </p>
</div>

This GitHub Action allows you to run Rust tests for a single target in a Wine environment.

It provides a convenient way to test your Rust package on Windows targets using the Wine compatibility layer.

## Purpose

Many components of Reloaded3 that enable modding touch low-level components of the Windows OS.

Therefore, I actively test our libraries against Wine to ensure that our code works equally well on
Linux. Thanks to this, several inconsistencies and bugs have already been found and fixed.

## Features

- Test Rust packages on Windows targets using Wine
- Support for different Rust toolchains (stable, beta, nightly)
- Caching of Rust dependencies for faster builds
- Customizable build and test flags
- Easy integration into your GitHub Actions workflow

## Usage

To use this action in your GitHub Actions workflow, you can add the following step:

```yaml
steps:
  - name: Test on Wine
    uses: Reloaded-Project/devops-rust-test-in-wine@v1
    with:
      target: i686-pc-windows-gnu
      rust-toolchain: stable
      extra-build-flags: --features="feature1 feature2"
```

### Inputs

The action supports the following inputs:

- `rust-project-path` (optional): Path to the Rust project. Default: `.`
- `rust-toolchain` (required): Rust toolchain to use (stable, beta, nightly). Default: `stable`
- `target` (required): The target platform for the Rust compiler.
    - Targets that use Wine: `i686-pc-windows-gnu`, `x86_64-pc-windows-gnu`
- `extra-test-flags` (optional): Extra flags to pass to the `cross test` command. Default: `''`

## Example Workflow

Here's an example of how you can use this action in your GitHub Actions workflow:

```yaml
name: Test on Wine

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
      
    - name: Test on Wine (x86)
      uses: Reloaded-Project/devops-rust-test-in-wine@v1
      with:
        target: i686-pc-windows-gnu
        
    - name: Test on Wine (x64)
      uses: Reloaded-Project/devops-rust-test-in-wine@v1
      with:
        target: x86_64-pc-windows-gnu
```

This workflow runs the tests on both x86 and x64 Windows targets using different
Rust toolchains and custom build/test flags.

This action should be ran from one of the Linux runners, e.g. `ubuntu-latest`.

## License

This project is licensed under the [MIT License](LICENSE).

## Contributing

Contributions are welcome! If you have any suggestions, bug reports, or feature requests,
please open an issue or submit a pull request.

## Acknowledgements

This action was inspired by the need to easily test Rust packages on Windows targets using
GitHub Actions. It builds upon the excellent work of the Rust and Wine communities.