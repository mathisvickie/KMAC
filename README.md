# UPDATE
Okay guys, so I have pushed here some more vulnerable drivers in special-package.zip which some has even ioctl codes in their file name so you know where to look for treats. Anyway you will probably not need them lol because of secret.rar which is password protected but anyone with three digit iq will figure out the password (name of archive will help you) and what the content of that archive is used for. Then look into that batch script located inside. You will need to change your local time in order to use it because it already expired long time ago but window$ will load anyway expired drivers so no worries. Just hope (better backup) they will not take down my whole repo/account for sharing this. You can thank me later <3 and remember to also seed, not just feed.

# KMAC
KernelMode AntiCheat

Just to see of what you should be aware when dealing with KMAC on Windows.

Many people are fighting with KMAC in ring0 and its cool to have some vulnerable signed driver that opens for you a door to windows kernel. You may either try to exploit some CVE: https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=driver or find yourself a 0-day which is not that easy but it's less detectable by anticheats. Here is a nice tool which enumerates x64 driver imports: https://gist.github.com/adrianyy/9c481c9b3b115a910985ce310d948534
I will add archive with some publicly well known drivers (signed & vulnerable), password for extraction is just simply 'password'. Nice talk about vulnerable drivers: https://eclypsium.com/2019/08/10/screwed-drivers-signed-sealed-delivered/

Looks like in ci.dll are some undocumented structures that leave some traces about (un)loaded drivers, see this:
https://github.com/TheCruZ/kdmapper/blob/master/kdmapper/intel_driver.cpp#L626 https://key08.com/index.php/2021/02/06/902.html

about BE see: https://secret.club/

Recently I dived into EAC (working on game Enlisted because its cool & free2play) and it looks like game calls eac.dll!CreateGameClient to get [this interface](https://github.com/mathisvickie/EAC-Emulator/blob/main/dllmain.cpp#L4). To note: real interface is larger but Enlisted does not use those functions after offset 0x50 (also doesnt use 0x30, 0x38, 0x40 and 0x48 vfuncs)

## Blacklisted
Most likely all vulnerable drivers in 'git' directory inside that huge zip are blacklisted by popular anticheats (avoid using all versions of them).

100% blacklist by f4ceit and v4nguard:
- winring
- msio64
- ene
- inpoutx64
- glckio2
- ntiolib_x64
- asio

V4nguard is scanning for this devices (i bet 4 bl4cklist -> b4n):
- \Device\ATSZIO
- \Device\genericdrv
- \DosDevices\AIDA64Driver
- \DosDevices\ALSysIO
- \DosDevices\AsUpdateio
- \DosDevices\Asusgio
- \DosDevices\BS_Def
- \DosDevices\CITMDRV
- \DosDevices\EneTechIo
- \DosDevices\GLCKIo2
- \DosDevices\Global\CPUZ
- \DosDevices\HOSTNT
- \DosDevices\NTIOLib
- \DosDevices\NVFLASH
- \DosDevices\RTCore
- \DosDevices\SE64
- \DosDevices\WinIoB
- \DosDevices\WinRing0
- \DosDevices\ZemanaAntiMalware
- \DosDevices\driveragent%d
- \DosDevices\inpout

# CVEs
As you may see many known bad drivers are blacklisted by BE/EAC and others because they were already used in public game cheats (and released on uc). Here are listed most recent  interesting CVEs: (i will try to keep this list updated)

## CVE-2021-36276 (dbutil version2)
Dell DBUtilDrv2.sys driver (versions 2.5 and 2.6) contains an insufficient access control vulnerability which may lead to escalation of privileges, denial of service, or information disclosure. Local authenticated user access is required.
Note: it is WDF driver so I won't make any PoC - feel free to analyze it, search for imports MmMapIoSpace and MmUnmapIoSpace.

## CVE-2021-31728 & CVE-2021-31727 (zemana again)
Not recommended to use because zemana was already detected in past even if these are new CVEs. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-31728 & https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-31727 POC: https://github.com/irql0/CVE-2021-31728

## CVE-2021-28685 (AsIO2_64.sys + AsIO2_32.sys)
Looks like this is second version of infamous AsIO and they just can't learn from own mistakes. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-28685
//todo: more info

## CVE-2021-27965 (MsIo64.sys)
For PoC see: https://github.com/mathisvickie/CVE-2021-27965

## CVE-2021-21551 (dbutil_2_3.sys)
Local Privilege Escalation to nt authority/system PoC: https://github.com/mathisvickie/CVE-2021-21551

## CVE-2020-0796 aka SMBGhost
RCE in microsoft SMB v3 protocol (when using compression) which can be used on localhost or remotely on LAN (arbitrary kernel memory read/write). Exploiting requires Windows10 1903 or 1909. Advantage is that nothing suspicious is running on target system because attack vector is network and bug happens in srv2.sys - microsoft windows file. See POC: https://github.com/ZecOps/CVE-2020-0796-LPE-POC (write_what_where - write arbitrary kernel memory over local network)
