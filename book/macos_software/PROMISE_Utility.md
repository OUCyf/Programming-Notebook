# PROMISE Utility

- Author: *{{Fu}}*
- Update: *Dec 18, 2022*
- Reading: *60 min*

---

## Introduction
- My disk's version is `Pegasus32-R4`, the product's website is https://www.promise.com/Products/Pegasus/Pegasus32

- Resources (drivers, utilities, and manuals) can be downloaded via https://www.promise.com/Support/DownloadCenter/Pegasus/Pegasus32/R4#Drivers



```{figure} ./files/promise32-R4.jpg
---
scale: 15%
align: center
name: promise32-R4
---
My Disk
```


## Dirvers and Utilities

Please consider to install the following drivers and utilities:

- `Pegasus32 /3 Series DEXT Driver for Apple-Silicon Macs`: the driver in M1 chip. (I install it in M1 but not loaded...due to some problems)


```{figure} ./files/promise-driver.jpg
---
scale: 30%
align: center
name: promise-driver
---
Driver
```


- `PROMISE Utility Pro for Mac`: the utility for Intel Macbook.

- `Pegasus32 Series Utility for Mac`: the utility for Apple-M1 Mac, and will generate the `promiseutil` command-line tool after installation.


```{figure} ./files/promiseutil.jpg
---
scale: 30%
align: center
name: promiseutil
---
Utilities
```



:::{admonition} A common problem is:  eject one of the drives in Pegasus R4 system when it is working, when plug it back in, it came up with a red light instead of blue, which will show as "Dead" in the Promise utility. How to recover it?

Open the Terminal and type `promiseutil`(based on `Pegasus32 Series Utility for Mac`), and hit Return to log into the CLI
Force the drives back online with the following commands:


```bash
# open `cliib` mode
promiseutil

# input in `cliib` mode
phydrv -a online -p1
phydrv -a online -p2
phydrv -a online -p3
phydrv -a online -p4
```

After forcing the PDs (Physical Disks) back online, the LEDs will turn back to blue and your volume should be accessible after forcing the (3) PDs back online.

**Reference with same problem:**
- https://forum.promise.com/thread/r4-array-bad/
- https://forum.promise.com/thread/pegasus-r4-multiple-drive-failures/
:::

