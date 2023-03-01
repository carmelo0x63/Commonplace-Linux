# This note groups a few commands focusing on disks and filesystems
- `findmnt`: find a filesystem
   `findmnt` will list all mounted filesystems or search for a filesystem.
- `lsblk`: list block devices
   `lsblk` lists information about all available or the specified block devices.

----

<a href="#findmnt">
### `findmnt`: simple usage
```
$ findmnt 
TARGET                       SOURCE         FSTYPE          OPTIONS
/                            /dev/sda2      ext4            rw,relatime

 ... truncated...
```

### `findmnt` usage with options
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

<a href="#lsblk">
### `lsblk` simple usage
```
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 119.2G  0 disk
├─sda1   8:1    0     8G  0 part [SWAP]
└─sda2   8:2    0 111.2G  0 part /
```

#### `lsblk` with `-f|--fs` option, to show info about filesystems
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

### Useful links
- []()

