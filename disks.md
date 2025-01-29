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
TARGET                         SOURCE      FSTYPE      OPTIONS
/                              /dev/sda1   ext4        rw,relatime,...
├─/sys                         sysfs       sysfs       rw,nosuid,...
│ ├─/sys/kernel/security       securityfs  securityfs  rw,nosuid,...
  ... truncated...
├─/proc                        proc        proc        rw,relatime
│ └─/proc/sys/fs/binfmt_misc   systemd-1   autofs      rw,relatime,...
  ... truncated...
├─/dev                         udev        devtmpfs    rw,nosuid,...
│ ├─/dev/pts                   devpts      devpts      rw,nosuid,...
  ... truncated...
└─/run                         tmpfs       tmpfs       rw,nosuid,...
  ├─/run/lock                  tmpfs       tmpfs       rw,nosuid,...
  ... truncated...
```

### `findmnt`: usage with options
#### `--real`: print only real filesystems
```
$ findmnt --real
TARGET    SOURCE    FSTYPE    OPTIONS
/         /dev/sda1 ext4      rw,relatime,errors=remount-ro
... truncated...
```

#### `-D`: imitate the output of `df`
```
$ findmnt -D
SOURCE    FSTYPE        SIZE  USED  AVAIL USE% TARGET
/dev/sda1 ext4        112.9G 46.9G  60.2G  42% /
udev      devtmpfs      3.8G     0   3.8G   0% /dev
tmpfs     tmpfs       784.3M  1.5M 782.8M   0% /run
... truncated...
```

----

<a href="#lsblk"></a>

### `lsblk`: simple usage
```
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:0    0 119.2G  0 disk
├─sda1   8:1    0 115.2G  0 part /
└─sda2   8:2    0     4G  0 part [SWAP]
```

### `lsblk`: usage with options
#### `lsblk`: with `-f|--fs` option, to show info about filesystems
```
$ lsblk -f
NAME   FSTYPE FSVER LABEL UUID          FSAVAIL FSUSE% MOUNTPOINTS
sda
├─sda1 ext4   1.0         7b905903...    60.2G    42% /
└─sda2 swap   1           b144cb2b...                 [SWAP]
```

#### Same as above, after plugging in an USB key
```
NAME   FSTYPE FSVER LABEL UUID          FSAVAIL FSUSE% MOUNTPOINTS
sda
├─sda1 ext4   1.0         7b905903...    60.2G    42% /
└─sda2 swap   1           b144cb2b...                 [SWAP]
sdb
└─sdb1 exfat  1.0   extdsk  AAFA-54B1   50.4G    58% /media/user/extdsk
```

----

<a href="#fdisk"></a>

### `fdisk -l`
```
$ sudo fdisk -l
...
Device     Boot     Start       End   Sectors   Size Id Type
/dev/sda1            2048 241666047 241664000 115.2G 83 Linux
/dev/sda2       241666048 250068991   8402944     4G 82 Linux swap / Solaris

```

----

<a href="#parted"></a>

### `parted -l`
```
$ sudo parted -l
...
Number  Start   End    Size    Type     File system     Flags
 1      1049kB  124GB  124GB   primary  ext4
 2      124GB   128GB  4302MB  primary  linux-swap(v1)  swap
```

----

$ ls -l /dev/disk/by-uuid
total 0
lrwxrwxrwx 1 root root 10 Jan 26 17:32 7b905903... -> ../../sda2
lrwxrwxrwx 1 root root 10 Jan 26 17:32 b144cb2b... -> ../../sda1


$ cat /etc/fstab
proc	          /proc	proc	defaults	0	0
UUID=7b905903...	/	ext4	rw,errors=remount-ro	0	1
UUID=b144cb2b...	swap	swap	sw	0	0


% sudo blkid
/dev/sda1: UUID="7b905903..." BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="bb9b2ea5-01"
/dev/sda2: UUID="b144cb2b..." TYPE="swap" PARTUUID="bb9b2ea5-02"

----

### Useful links
- []()

