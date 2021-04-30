# KMAC
KernelMode AntiCheat

Just to see of what you should be aware when dealing with KMAC

Many people are fighting with KMAC in ring0 and its cool to have some vulnerable signed driver that opens for you a door to windows kernel. You may either try to exploit some CVE: https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=driver or find yourself a 0-day which is not that easy but it's less detectable by anticheats. Here is a nice tool which enumerates x64 driver imports: https://gist.github.com/adrianyy/9c481c9b3b115a910985ce310d948534
I will add zip with some publicly well known drivers (signed & vulnerable)

Looks like in ci.dll are some undocumented structures that leave some traces about (un)loaded drivers, see this:
https://github.com/TheCruZ/kdmapper/blob/master/kdmapper/intel_driver.cpp#L626

https://key08.com/index.php/2021/02/06/902.html

about BE see: https://secret.club/

Recently I dived into EAC (working on game Enlisted because its cool & free2play) and it looks like game calls eac.dll!CreateGameClient to get [this interface](https://github.com/mathisvickie/EAC-Emulator/blob/main/dllmain.cpp#L4). To note: real interface is larger but Enlisted does not use those functions after offset 0x50 (also doesnt use 0x30, 0x38, 0x40 and 0x48 vfuncs)
