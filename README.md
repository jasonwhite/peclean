# pepatch

*This is a work in progress.*

This is a simple tool to make builds of Portable Executables (PEs) reproducible.

Timestamps and other non-deterministic data are embedded in DLLs, EXEs, and
PDBs. If a DLL is compiled and linked twice without changing any source, the
DLLs will not be bit-by-bit identical. This tool fixes that.

Builds that are reproducible are very useful for a number of reasons. The site
https://reproducible-builds.org/ does an excellent job of enumerating those
reasons.

## Using It

Usage is as follows:

    $ pepatch IMAGE [PDB]

The EXE/DLL is specified as the first parameter and the PDB is optionally
specified as the second. The PDB must be modified because changing the image
invalidates the signature for the PDB.

As a post-build step, simply run:

    $ pepatch MyModule.dll MyModule.pdb

The files are overwritten in-place.

## Building It

This is a very simple C++ program. There are no dependencies and it should be
buildable and runnable on any platform (even non-Windows!).

### Windows

Just open `vs/vs2015/peclean.sln` and build it. Of course, this requires Visual
Studio 2015. If another version of Visual Studio is needed, please submit an
issue or, better yet, a pull request.

### Linux

Although this is primarily a Windows utility, it was developed in a Linux
environment simply because it is faster and easier. One might also want to use
it for compiling Windows binaries on Linux. Thus, it builds and runs on Linux as
well.

To build it, just run `make`.

### OS X

This hasn't been tested on OS X, but it probably works as there is nothing
Linux-specific in the code.

To build it, just run `make`.

If you find that this works, please submit an issue letting me know.

## Related Work

I am only aware of the [zap_timestamp][] tool in [Syzygy][]. Unfortunately, it
has a couple of problems:

 1. It does not work with 64-bit PE files (i.e., the PE32+ format).
 2. It is a pain to build. It is part of a larger suite of tools that operate on
    PE files. That suite then requires Google's depot_tools. The end result is
    that you're required to download hundreds of megabytes of tooling around
    something that should be very simple.

[zap_timestamp]: https://github.com/google/syzygy/tree/master/syzygy/zap_timestamp
[Syzygy]: https://github.com/google/syzygy

## License

As always, this tool uses the very liberal [MIT License](/LICENSE). Use it for
whatever nefarious purposes you like.
