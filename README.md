# `Lich`

*Defying OS-based firmware defects through forbidden magical instruments*

## Description

**Lich** is an OS-based firmware analyzer designed to detect vulnerabilities and
extract energy consumption data.

The core idea behind this software is to aggregate results from various tools
into a single final report. To generate this report, all selected tools are
executed sequentially.
A tool can be excluded from execution via a configuration file option, offering
flexibility, especially when dealing with unmaintained tools.

The programming language used to develop the firmware doesn't matter, as only
the final binary and its variants are considered during the analysis.

Unlike other tools, **Lich** eliminates the need for developers to install any
dependencies on their local machines. All tests are run within a self-contained
environment created by Docker.

The final results are presented in a single markdown document, with each test
output assigned to a separate section.

**Lich** is written in Rust, which ensures safe management of tool invocations.
The Rust `Command` API provides a fine-grained process builder for precise
control over how processes are spawned. Additionally, using Rust reduces the
risk of introducing vulnerabilities into the tool itself.

## Usability

**Lich** can also be used for Continuous Integration (CI) purposes. It can be
run either on every commit or before a firmware release to check for internal
vulnerabilities, or even to estimate firmware energy consumption.
The final results can be provided as CI artifacts or displayed as a pull request
comment with a link to a temporary `html` file.

This tool can also be integrated into a certification process to verify whether
specific properties are met. If a property is violated, the corresponding test
**should** fail.

Energy costs are a growing concern. Estimating firmware energy consumption
during execution can help lower monthly billing, particularly for firmware that
runs continuously, day and night.

## Limitations

- **Lich** **must** be run on the same hardware architecture as the OS-based
firmware, since the firmware needs to be executed at runtime to perform most of
the tests.
An emulator may not always be a viable solution due to common limitations in
such software.
- Some tools used by **Lich** may only support popular hardware architectures,
excluding niche or independent platforms from the analysis.
