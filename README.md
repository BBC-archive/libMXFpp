# libMXF++

libMXF++ is a C++ wrapper library for [libMXF](https://github.com/bbc/libMXF) that supports reading and writing the [SMPTE ST 377-1 MXF file format](https://ieeexplore.ieee.org/document/7292073).

libMXF++ and [libMXF](https://github.com/bbc/libMXF) are used in the [bmx](https://github.com/bbc/bmx) project.

libMXF++ was originally developed as part of the [Ingex Project](http://ingex.sourceforge.net/) where it supported MXF transfer, playback and storage applications.

## Examples

A number of examples can be found in the [examples](./examples) directory. These are not part of the core library and are not required to build [bmx](https://github.com/bbc/bmx).

* [D10MXFOP1AWriter](./examples/D10MXFOP1AWriter): library code used in the [Ingex Project](http://ingex.sourceforge.net/) for writing [SMPTE ST 386](https://ieeexplore.ieee.org/document/7291350) MXF D-10 (Sony MPEG IMX) files.
* [OPAtomReader](./examples/OPAtomReader): library code used in the [Ingex Project](http://ingex.sourceforge.net/) for recovering Avid MXF OP-Atom files after a system failure.

## Build, Test and Install

libMXF++ is developed on Ubuntu Linux but is supported on other Unix-like systems and Windows.

The [cmake](https://cmake.org/) build system is used and version >= **3.12** is required. The build process has been tested on 32- and 64-bit versions of Ubuntu, Debian and Windows (Microsoft Visual C++ 2017 (updated) and later versions).

### Dependencies

The [libMXF](https://github.com/bbc/libMXF) library is required and is included as git submodules in the `deps/` directory. Run

```bash
git submodule update --init
```

to ensure the submodules are available and up-to-date in the working tree.

### Commands

A basic commandline process is described here for platforms that default to the Unix Makefiles or Visual Studio cmake generators. See [./docs/build.md](./docs/build.md) for more detailed build options.

Replace `<build type>` in the commandlines below with `Debug` or `Release`. Note that the Visual Studio generator supports multiple build types for a configuration, which is why the build type is selected _after_ configuration.

The default generator can be overridden using the cmake `-G` option. The list of available generators is shown at the end of the output of `cmake --help`.

Start by creating a build directory and change into it. The commandlines below use a `out/build` build directory in the working tree, which follows the approach taken by Microsoft Visual Studio C++.

#### Unix-like (Unix Makefiles)

```bash
cmake ../../ -DCMAKE_BUILD_TYPE=<build type>
cmake --build .
make test
sudo make install
```

Run `ldconfig` to update the runtime linker cache. This avoids library link errors similar to "error while loading shared libraries".

```bash
sudo /sbin/ldconfig
```

#### Windows (Visual Studio)

```console
cmake ..\..\
cmake --build . --config <build type>
ctest -C <build type>
cmake --build . --config <build type> --target install
```

## Source and Binary Distributions

Source distributions and Windows binaries are made [available on SourceForge](https://sourceforge.net/projects/bmxlib/files/).

## License

The libMXF++ library is provided under the BSD 3-clause license. See the [COPYING](./COPYING) file provided with this library for more details.
