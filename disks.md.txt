# This note groups a few commands focusing on disks and filesystems
- `findmnt`: find a filesystem</br>
   `findmnt` will list all mounted filesystems or search for a filesystem.
- `lsblk`: list block devices</br>
   `lsblk` lists information about all available or the specified block devices. The lsblk command reads the sysfs filesystem and udev db to gather information.
- `fdisk`: manipulate disk partition table<br/>
   `fdisk -l` lists the partition tables for the specified devices and then exits. If no devices are given, those mentioned in /proc/partitions (if that file exists) are used.
- `parted`: a partition manipulation program<br/>
   `parted -l` lists partition layout on all block devices

----

<a href="#findmnt"></a>

### `findmnt`: simple usage
```
$ findmnt 
TARGET                       SOURCE         FSTYPE          OPTIONS
/                            /dev/sda2      ext4            rw,relatime
├─/sys                       sysfs          sysfs           rw,nosuid,nodev,noexec,relatime
│ ├─/sys/kernel/security     securityfs     securityfs      rw,nosuid,nodev,noexec,relatime
│ ├─/sys/fs/cgroup           cgroup2        cgroup2         rw,nosuid,nodev,noexec,relatime,...
... truncated...
├─/proc                      proc           proc            rw,relatime
│ └─/proc/sys/fs/binfmt_misc systemd-1      autofs          rw,relatime,fd=29,pgrp=1,timeout=0,...
... truncated...
```

### `findmnt`: usage with options
#### `--real`: print only real filesystems
```
$ findmnt --real
TARGET       SOURCE      FSTYPE      OPTIONS
/            /dev/sda2   ext4        rw,relatime
```

#### `-D`: imitate the output of `df`
```
$ findmnt -D
SOURCE    FSTYPE        SIZE  USED  AVAIL USE% TARGET
udev      devtmpfs      1.9G     0   1.9G   0% /dev
tmpfs     tmpfs       389.8M  1.2M 388.6M   0% /run
/dev/sda2 ext4         19.5G 11.1G   7.4G  57% /
tmpfs     tmpfs         1.9G     0   1.9G   0% /dev/shm
tmpfs     tmpfs           5M    4K     5M   0% /run/lock
tmpfs     tmpfs       389.8M  112K 389.7M   0% /run/user/1000
portal    fuse.portal                          /run/user/1000/doc
```

----

<a href="#lsblk"></a>

### `lsblk`: simple usage
```
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 119.2G  0 disk
├─sda1   8:1    0     8G  0 part [SWAP]
└─sda2   8:2    0 111.2G  0 part /
```

### `lsblk`: usage with options
#### `lsblk`: with `-f|--fs` option, to show info about filesystems
```
NAME   FSTYPE FSVER LABEL UUID      FSAVAIL FSUSE% MOUNTPOINT
sda
├─sda1 swap   1           ********                 [SWAP]
└─sda2 ext4   1.0         ********    73.4G    28% /
```

#### Same as above, after plugging in an USB key
```
NAME   FSTYPE FSVER LABEL   UUID      FSAVAIL FSUSE% MOUNTPOINT
sda
├─sda1 swap   1             ********                 [SWAP]
└─sda2 ext4   1.0           ********    73.4G    28% /
sdb
└─sdb1 exfat  1.0   extdsk  AAFA-54B1   50.4G    58% /media/user/extdsk
```

----

<a href="#fdisk"></a>

### `fdisk -l`
```
$ sudo fdisk -l
Disk /dev/sda: 119.24 GiB, 128035676160 bytes, 250069680 sectors
Disk model: SanDisk SD5SB212
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xe80546f2

Device     Boot    Start       End   Sectors   Size Id Type
/dev/sda1           3906  16800781  16796876     8G 83 Linux
/dev/sda2       16801792 250068991 233267200 111.2G 83 Linux
```

----

<a href="#parted"></a>

### `parted -l`
```
$ sudo parted -l
Model: ATA SanDisk SD5SB212 (scsi)
Disk /dev/sda: 128GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type     File system     Flags
 1      2000kB  8602MB  8600MB  primary  linux-swap(v1)
 2      8603MB  128GB   119GB   primary  ext4
```

----

### Useful links
- []()

