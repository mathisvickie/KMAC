# KMAC
KernelMode AntiCheat

Just to see of what you should be aware when dealing with KMAC

Looks like in ci.dll are some undocumented structures that leave some traces about (un)loaded drivers, see this example:
[https://github.com/TheCruZ/kdmapper/blob/master/kdmapper/intel_driver.cpp#L626](https://github.com/TheCruZ/kdmapper/blob/master/kdmapper/intel_driver.cpp#L626)
