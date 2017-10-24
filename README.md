# armv6l-unknown-linux-gnueabihf

GNU cross compiler for little-endian processors with the ARMv6 architecture using the hard-float ABI.

## How do I use this toolchain?

- Add the `bin` folder (in the toolchain) to your path.
- For ease of use, export the cross compiler's prefix (the hyphen at the end is important! Also you can call it anything you like, not necessarily CCPREFIX)

```bash
export CCPREFIX=armv6l-unknown-linux-gnueabihf-
```

- **Direct usage:** You can call `${CCPREFIX}{binary-name}` directly (where `binary-name` is the name of the tool you want to use). For example, `${CCPREFIX}gcc` will execute the GCC from the cross compiler. Otherwise usage is the same as normal.

- **Usage with make:** If you are using make, you need to specify the target architecture (ARM) and the cross compiler's prefix.

```bash
make ARCH=arm CROSS_COMPILE=${CCPREFIX} # The rest of the make command is as usual
```

## What does any of this mean?

### It's (part of) a toolchain

Toolchains are...chains of tools. They're a set of tools that perform a complex software development task, usually building a binary or package from source code. Usually the host (the platform on which the toolchain runs) and the target (the platform on which the executable will be run) are the same, but you can use a special toolchain called a _cross toolchain_ to build for a different target - for example, building Windows libraries on Linux, or building ARM binaries on x86.

This repo contains _part_ of the [GNU toolchain](https://en.wikipedia.org/wiki/GNU_toolchain) - specifically the GNU Compiler Collection (C and C++ only) and GNU Binutils (a suite for working with libraries, object files, binaries and assembly code) - as well as the GNU C Library and headers from the Linux kernel.

| Source             | Version | Release Date |
|--------------------|---------|--------------|
| gcc                | 7.2.0   | 2017-08-14   |
| binutils           | 2.29    | 2017-07-24   |
| eglibc*            | 2.18    | 2014-09-29   |
| kernel (headers)** | 4.9.22  | 2017-04-12   |

*Currently this toolchain uses the Embedded GNU C Library, a fork of glibc designed for embedded systems that has not been in active development since 2014. There are plans to migrate it to the mainline GNU C library.

**Version 4.9 of the Linux kernel is a long-term release, with a projected EOL of January 2019. This toolchain will remain on 4.9.x until then.

### Target triplet: armv6l-unknown-linux-gnueabihf

Executables built with this crosscompiler will only run on platforms that meet these specifications:

| Property               | Specification    |
|------------------------|------------------|
| Endianness             | Little-endian    |
| Processor architecture | ARMv6 (embedded) |
| Userland/Kernel        | GNU/Linux        |
| Floating-point unit    | Hard float       |

#### Endianness

Endianness refers to the order in which bytes are transferred or stored in memory/secondary storage. _Words_ (the unit of data used by a particular processor, usually 8, 16, 32 or 64 bits long) may be represented in memory either most significant bit first (big-endian) or least significant bit first (little-endian).

#### Processor architecture

Processors vary in their architecture (or _instruction set_), which is the set of very low-level commands for accessing memory addresses, reading and writing data, and performing arithmetic that a given processor understands. Programs written in higher-level languages such as C++ or Python must be translated to this instruction set (through either compilation or interpretation) before they can be run.

Most laptops and desktops use x86 (or x86_64, a 64-bit x86 architecture) processors; most mobile devices and other embedded systems use ARM processors. There are several ARM microarchitectures designed to run on different ARM processor cores, from ARMv1 to the latest ARMv8.x-A. Processors and systems-on-a-chip that have an ARM11 core (e.g the Broadcom BCM2835 SoC, which has an ARM1176 core) use the ARMv6 instruction set.

#### Userland/Kernel

Together these make up a software system, usually an operating system. Most Linux operating systems use the [GNU userland](https://www.gnu.org/) in combination with the [Linux kernel](https://www.kernel.org/); a notable exception is Android, whose userland is a combination of Bionic, Toybox and the Korn shell. Of the other major (desktop) operating systems, macOS is based on the open-source Darwin (which uses a hybrid XNU kernel and a custom userland with GNU and BSD elements) and Windows uses the Windows NT (hybrid) kernel.

#### Floating-point emulation

Floating point numbers are notoriously difficult for computers to work with. Their range and precision can be almost impossible to express in base two. Most computers have a _floating point unit_ to handle floating-point arithmetic. An FPU may be _soft_ (i.e. emulated via a floating-point library) or _hard_ (a physical math coprocessor, either integrated with the CPU or as an add-on).

## Happy building! :)
