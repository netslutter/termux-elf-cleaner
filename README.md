
# termux-elf-cleaner
Utility for Android ELF files to remove unused parts that the linker warns about.
<h1><b>WARNING: This repo is strictly for Android 5.x</b></h1>
This repo is targated for Android 5.x , hence it removes dynamic section entries that are not supported in Android 5.x.
Some of which are supported/may be required in Android 6.0 and later versions. So it is advised not to use this tool
IF you are running Android version 6.0 or higher.

# Description
When loading ELF files, the Android linker warns about unsupported dynamic section entries with warnings such as:

    WARNING: linker: /data/data/org.kost.nmap.android.networkmapper/bin/nmap: unused DT entry: type 0x6ffffffe arg 0x8a7d4
    WARNING: linker: /data/data/org.kost.nmap.android.networkmapper/bin/nmap: unused DT entry: type 0x6fffffff arg 0x3

This utility strips away the following dynamic section entries:

- `DT_RPATH` -------- not supported in any Android version.
- `DT_RUNPATH` ----- supported from Android 7.0.
- `DT_VERDEF` ------ supported from Android 6.0.
- `DT_VERDEFNUM` -- supported from Android 6.0.
- `DT_VERNEEDED`--- supported from Android 6.0.
- `DT_VERNEEDNUM`-- supported from Android 6.0.
- `DT_VERSYM` ------- supported from Android 6.0.
- `DT_GNU_HASH` ---- causes warnings in Android 5.x
- `DF_1_NODELETE`-- supported from Android 6.0. Causes warnings in Android 5.x.

It also removes the three ELF sections of type:

- `SHT_GNU_verdef`
- `SHT_GNU_verneed`
- `SHT_GNU_versym`

# Usage
```sh
usage: termux-elf-cleaner <filenames>

Processes ELF files to remove unsupported section types and
dynamic section entries which the Android linker warns about.
```

# Author
Fredrik Fornwall ([@fornwall](https://github.com/fornwall)).
