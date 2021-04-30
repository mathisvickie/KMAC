# KMAC
KernelMode AntiCheat

Just to see of what you should be aware when dealing with KMAC

Looks like in ci.dll are some undocumented structures that leave some traces about (un)loaded drivers, see this:
https://github.com/TheCruZ/kdmapper/blob/master/kdmapper/intel_driver.cpp#L626

https://key08.com/index.php/2021/02/06/902.html

about BE see: https://secret.club/

Recently I dived into EAC (working on game Enlisted because its cool & free2play) and it looks like game calls eac.dll!CreateGameClient to get [this interface](https://github.com/mathisvickie/EAC-Emulator/blob/main/dllmain.cpp#L4). To note: real interface is larger but Enlisted does not use those functions after offset 0x50 (also doesnt use 0x30, 0x38, 0x40 and 0x48 vfuncs)
