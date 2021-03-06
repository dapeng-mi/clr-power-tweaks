## SYNOPSIS

**`clr-power-tweaks.conf`** is an optional configuration file for the
clr_power(1) utility.

`/etc/clr-power-tweaks.conf`

## DESCRIPTION

**`clr-power-tweaks.conf`** is an optional configuration file for the
clr_power(1) utility. The configuration file contains kernel and device
parameter values used by the clr_power(1) utility. 

Configuration parameter values placed in **`clr-power-tweaks.conf`** will
supersede the built-in defaults configured by clr_power(1). New parameters can
be added to the configuration to supplement the built-in values. Built-in
parameters can be changed by defining them in **`clr-power-tweaks.conf`** with
a different value. Parameters can be excluded from being modified by
clr_power(1) by adding them in **`clr-power-tweaks.conf`** without a value.

## FILE FORMAT

**`clr-power-tweaks.conf`** uses a key-value pairs to define parameter values.

Each line contains one parameter-value pair, delimited by a space character.

Parameters are paths from the proc(5) filesystem. Parameters paths can include
glob(n) wildcards to match multiple paths. 

Acceptable values are determined by the parameter being set. Any parameter
listed in the configuration file without a value will be excluded by
clr_power(1) and the parameter will inherit the kernel's built-in default
parameter value.

## EXAMPLES

1. **`clr-power-tweaks.conf`** entry to override the default value in
   clr_power(1) for CPU governor with **powersave**. All other values built-in
   to clr_power(1) would still get applied.

   Note the globbing used with `*` to target all CPU cores. 
   
   ```
   /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor powersave
   ```

2.  **`clr-power-tweaks.conf`** entry to exclude a parameter causing it to use
    the kernel's built-in default value (60). All other values built-in to
    clr_power(1) would still get applied.

    Note the omission of a value.

    ```
    /proc/sys/vm/swappiness
    ```

3. **`clr-power-tweaks.conf`** entry to add two new parameters to increase UDP
   buffers All other values built-in to clr_power(1) would still get applied.

   ```
   /proc/sys/net/ipv4/udp_rmem_min 8192
   /proc/sys/net/ipv4/udp_wmem_min 8192
   ```

## BUGS

The default clr-power-tweaks.conf(5) aims to have reasonable defaults for
achieving power and performance efficiency. Default values may not be optimal
for all systems and environments. 

See GitHub Issues: <https://github.com/clearlinux/clr-power-tweaks/issues>

## SEE ALSO

**clr_power.conf(5)**, **proc(5)**, **sysctl(2)**

For parameters understood by the kernel, please see
https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html