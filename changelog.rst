##################
BlocksDS changelog
##################

Version 0.8 (2023-07-16)
========================

- ``libnds``:

  - Document MPU setup code properly.
  - Cleanup exception handling code.
  - Add asynchronous math functions to complement the previous synchronous ones.
  - Support redirecting ``stdout`` and ``stderr`` to user functions.
  - Fix code that selects the default filesystem (DSi SD or DLDI).
  - Fix leaking file handlers in ``truncate()``.
  - Fix memory leaks in ``image`` and ``pcx`` modules.
  - Support more rumble packs.

- ``ndstool``:

  - Fix warnings.
  - Remove non-homebrew-related functionality.

- SDK:

  - Automatically link with libc and libstdc++ rather than forcing users to do
    it explicitly.
  - Support ``*.arm.c`` and ``*.arm.cpp`` filenames for compatibility with
    devkitARM.
  - Correctly initialize TLS in the ARM7.
  - Improve ``bin2c``.
  - Update libc documentation.
  - Improve and cleanup some examples.

Version 0.7 (2023-04-19)
========================

- ``libnds``:

  - Unify all coding and documentation style of the codebase.
  - Change license of GL2D to Zlib (with the author's permission).
  - Improve ``sassert()`` so that it can exit to the loader instead of locking
    the application.

  - Keyboard:

    - Fix initialization glitch where it would blink for a frame.
    - Fix backspace handling.
    - Make it use cothread functions so that it never blocks the application.

  - ``cothread``:

    - Fixed stack alignment
    - Fixed stack size of the scheduler thread.

  - ``libc``:

    - Fix no$gba debug messages on the ARM9.
    - Add support of no$gba debug messages to the ARM7.

- ``mmutil``:

  - Fix segfault with samples with implied zero loop.

- SDK:

  - Improve some old examples. Fix memory leaks in all examples that used
    ``getcwd()``.
  - Fix ARM9 linkerscript to place ITCM sections in ITCM correctly.
  - Add new examples: Exception handling, assertions, no$gba debug console.
  - Prevent ``mkfatimg`` from generating FAT images that are so small that FatFs
    can't mount them.
  - Improve installation instructions.

Version 0.6 (2023-04-11)
========================

- ``libnds``:

  - Document MPU setup steps and CP15 registers.
  - Enable more warnings in the Makefile and fix them.

  - FIFO subsystem:

    - The FIFO subsystem has been cleaned up and documented.
    - Some bugs in the FIFO subsystem have been fixed (the stress test still
      fails, though).
    - Prevent using ``cothread_yield()`` in the ARM7.

  - ``libc``:

    - Alignment of thread local storage sections has been fixed.
    - Support ``stat()`` in the root directory of a filesystem.
    - Support ``statvfs()`` and ``fstatvfs()``.

  - Avoid including the default keyboard data if it isn't used.
  - Allow setting the duration of the lid sleep check, and to disable it
    completely.
  - Build release versions of the library as well as debug.

- ``ndstool``:

  - Support multiple languages in the banner.
  - Support more file formats for icons (GIF, PNG).
  - Support animated icons (from GIF files).

- SDK:

  - Refactor ``install`` targets of the SDK components. Now, all components can
    be installed on their own, and they copy the licenses of the components to 
    the installation directory.
  - Emulate behaviour of ``bin2s`` of devkitPro more closely with ``bin2c``.
  - Use SPDX license identifiers in all libraries and components that end up in
    the NDS application binary.
  - Some cleanup of code formatting.
  - Added a DLDI driver template.

Version 0.5 (2023-03-31)
========================

- Define a default location for BlocksDS: ``/opt/blocksds/``
- Use ``mkfatimg`` (distributed with FatFs) instead of ``imgbuild.sh`` to reduce
  the number of dependencies.
- Fix ``mmutil`` target in Makefiles in parallel builds.
- Cleanup of GBA slot peripherals drivers.
- Integrate ``libxm7`` as a core library.
- Fix exit to loader code from the ARM7. It has been simplified a bit.
- Document exit to loader code.

Version 0.4 (2023-03-26)
========================

- Use Wonderful Toolchains to get full C++ standard library support.
- Remove ``picolibc`` and ``avr-libstdcpp`` as submodules (all previous history
  has been condensed to one commit).
- Multithreading:
  - Add cooperative multithreading scheduler.
  - Enable scheduler in the ARM9 by default.
  - Add examples of having multiple threads, mutexes, and asynchronous file
    loading.
  - Support thread local storage.
  - Added mutexes to problematic parts of ``libnds`` and FatFs.
- Add initial support and example of DSi camera (thanks, asie!).
- Support ``malloc()`` in the ARM7.
- Simplify build system of tests and examples.
- Bugfixes.

Version 0.3.1 (2023-03-20)
==========================

- Hotfix.

Version 0.3 (2023-03-20)
========================

- FatFs performance improvements (like adding a disk cache).
- Support DLDI in the ARM7 as well as the ARM9.
- Add function for the ARM9 to request the ARM7 to read the cartridge.
- Add some missing definitions of DSi registers (SCFG/NDMA).
- General cleanup of ``libnds`` code (like replacing magic numbers by defines).
- Build system improvements (support two line app titles, remove old makefiles).
- ``libsysnds`` has been integrated in ``libnds``.
- Bugfixes in libc and`` libnds``.
  - EEPROM handling functions.
  - Data cache handling bugs.
  - Fix transparency in keyboard of ``libnds``.
- Added some tests.

Version 0.2 (2023-03-15)
========================

- Improve C++ support (now the C++ standard library it is actually usable).
- Improve C library support.
- Integrate agbabi as ``ndsabi`` (provides fast ``memcpy``, coroutines, etc).
- Fix ``install`` target.

Version 0.1 (2023-03-14)
========================

First beta release of BlocksDS. Features:

- Supports ``libnds``, ``maxmod``, ``dswifi``.
- Supports a lot of the standard C library.
- Very early support of the standard C++ library.
- Supports DLDI, DSi SD slot and NitroFAT (open source alternative of NitroFS)
  through Elm's FatFs.
- Documentation on how to migrate projects to BlocksDS.
- Docker image provided.

