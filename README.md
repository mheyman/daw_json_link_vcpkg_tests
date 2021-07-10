# DAW JSON-LINK VCPKG TESTS

This repository is ported from [daw_json_link](https://github.com/beached/daw_json_link)'s
tests.

Seriously, if you want fast JSON parsing, use [daw_json_link](https://github.com/beached/daw_json_link).

Easiest is to depend on the vcpkg `daw-json-link` port.

## Building And Running

```sh
# Set CMAKE_TOOLCHAIN_FILE to where your vcpkg toolchain file actually is located.
cmake -B build -S . -G Ninja -DCMAKE_TOOLCHAIN_FILE=../vcpkg/scripts/buildsystems/vcpkg.cmake

cmake --build build

cd build

ctest
```

## Why This Version Of The Tests?

The difference is that these tests use [vcpkg](https://github.com/microsoft/vcpkg)
`daw-json-link` port for the source to test.

## Changes needed to use the vcpkg `daw-json-link` port.

The [vcpkg](https://github.com/microsoft/vcpkg) `daw-json-link` port depends on the
`daw-utf-range` port which, in turn, depends on the `daw-header-libraries` port.

The `daw-utf-range` port is the troublesome one because it includes a version of the
`utfcpp` port. To keep conflicts to a minimum, that port moves `utfcpp`'s `utf8::`
namespace to `daw::utf8::` and puts the header files under `include/daw`.

Changes to the unit tests were needed to accomodate those changes.

Another difference is the use of the `nanobench` port. Nanobench can be used
header-only or header + library. The [vcpkg](https://github.com/microsoft/vcpkg) port
of nanobench is header-only while the original test code assumed header + library.

Changes to the unit tests were needed to accomodate those changes as well.

Finally, there were some un-run tests that still had source code that got parsed.
That code failed to compile so this repository ifdefs it out.
