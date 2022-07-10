# `findmnt`: find a filesystem
`findmnt` will list all mounted filesystems or search for a filesystem.

----

### Simple usage
```
$ findmnt 
TARGET                       SOURCE         FSTYPE              OPTIONS
/                            /dev/sda2      ext4                rw,relatime
├─/sys                       sysfs          sysfs               rw,nosuid,nodev,noexec,relatime
│ ├─/sys/kernel/security     securityfs     securityfs          rw,nosuid,nodev,noexec,relatime
│ ├─/sys/fs/cgroup           cgroup2        cgroup2             rw,nosuid,nodev,noexec,relatime,nsdelegate,memory_recursiveprot
│ ├─/sys/fs/pstore           pstore         pstore              rw,nosuid,nodev,noexec,relatime
│ ├─/sys/fs/bpf              none           bpf                 rw,nosuid,nodev,noexec,relatime,mode=700
│ ├─/sys/kernel/debug        debugfs        debugfs             rw,nosuid,nodev,noexec,relatime
│ ├─/sys/kernel/tracing      tracefs        tracefs             rw,nosuid,nodev,noexec,relatime
│ ├─/sys/kernel/config       configfs       configfs            rw,nosuid,nodev,noexec,relatime
│ └─/sys/fs/fuse/connections fusectl        fusectl             rw,nosuid,nodev,noexec,relatime
├─/proc                      proc           proc                rw,relatime
│ └─/proc/sys/fs/binfmt_misc systemd-1      autofs              rw,relatime,fd=29,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=16406
 ... truncated...
```

### Usage with options
```
$ findmnt --real
TARGET               SOURCE    FSTYPE      OPTIONS
/                    /dev/sda2 ext4        rw,relatime
└─/run/user/1000/doc portal    fuse.portal rw,nosuid,nodev,relatime,user_id=1000,group_id=1000

```

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

### Useful links
- []()

