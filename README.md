# DAW JSON-LINK VCPKG TESTS

This repository is ported from [daw_json_link](https://github.com/beached/daw_json_link)'s
tests.

Seriously, if you want fast JSON parsing, use [daw_json_link](https://github.com/beached/daw_json_link).

Easiest is to depend on the vcpkg `daw-json-link` port.

## Building And Running

```sh
# Set CMAKE_TOOLCHAIN_FILE to where your vcpkg toolchain file actually is located.
# You can also add -DVCPKG_TARGET_TRIPLET=... to get other than the default vcpkg triplet
cmake -B build -S . -G Ninja -DCMAKE_TOOLCHAIN_FILE=../vcpkg/scripts/buildsystems/vcpkg.cmake

cmake --build build

cd build

ctest
```

## Why This Version Of The Tests?

The difference is that these tests use [vcpkg](https://github.com/microsoft/vcpkg)
`daw-json-link` port for the source to test.

Note: the [vcpkg](https://github.com/microsoft/vcpkg) `daw-json-link` port
depends on the `daw-utf-range` port which, in turn, depends on the
`daw-header-libraries` port.

## Changes To Run In The Vcpkg Ecosystem

The use of the `nanobench` port. Nanobench can be used header-only or
header + library. The [vcpkg](https://github.com/microsoft/vcpkg) port of
nanobench is header-only while the original test code assumed
header + library. Nanobench dependency
[here](https://github.com/mheyman/daw_json_link_vcpkg_tests/blob/ac4e438872ac64dc6bc59933d2f9341a8452c8a5/vcpkg.json#L7).

Changes to the unit tests were needed to accomodate that.

## Miscellaneous Changes

There were some un-run tests that still had source code that got parsed.
This may be compiler related (different compilers may behave differently).
That code failed to compile so this repository ifdefs it out.
