# `lsblk`: list block devices
`lsblk` lists information about all available or the specified block devices. The lsblk command reads the sysfs filesystem and udev db to gather information.

----

### Simple usage
```
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 119.2G  0 disk
├─sda1   8:1    0     8G  0 part [SWAP]
└─sda2   8:2    0 111.2G  0 part /
```

### With `-f|--fs` option, to show info about filesystems
```
NAME   FSTYPE FSVER LABEL UUID      FSAVAIL FSUSE% MOUNTPOINT
sda
├─sda1 swap   1           ********                 [SWAP]
└─sda2 ext4   1.0         ********    73.4G    28% /
```

### Same as above, after plugging in an USB key
```
NAME   FSTYPE FSVER LABEL   UUID      FSAVAIL FSUSE% MOUNTPOINT
sda
├─sda1 swap   1             ********                 [SWAP]
└─sda2 ext4   1.0           ********    73.4G    28% /
sdb
└─sdb1 exfat  1.0   extdsk  AAFA-54B1   50.4G    58% /media/user/extdsk
```

----

### Useful links
- []()

