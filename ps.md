# `ps`: report a snapshot of the current processes
`ps` displays information about a selection of the active processes. Several versions of `ps` exist, each of them may accept different options:
1. UNIX options, which may be grouped and must be preceded by a dash, e.g. `ps -abc`
2. BSD options, which may be grouped and must not be used with a dash, e.g. `ps abc`
3. GNU long options, which are preceded by two dashes, e.g. `ps --aaa --bbb --ccc`

**NOTE**: the two standards are not directly comparable. For instance, here are two _similar_ options sets:
-UNIX: all processes + extra full format
```
$ ps -AF | head -n1
UID          PID    PPID  C    SZ   RSS PSR STIME TTY          TIME CMD
```

- BSD: all processes + user-oriented format
```
$ ps aux | head -n1
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
```

----

### Useful examples

- all processes + extra full format (UNIX)
```
$ ps -AF
UID          PID    PPID  C    SZ   RSS PSR STIME TTY          TIME CMD
root           1       0  0 42114 11572   0 12:10 ?        00:00:00 /sbin/init
root           2       0  0     0     0   5 12:10 ?        00:00:00 [kthreadd]
...
root         941       2  0     0     0   1 12:16 ?        00:00:00 [kworker/1:0]
root         973       2  0     0     0   7 12:20 ?        00:00:00 [kworker/7:2-mm_percpu_wq]
root        1041       2  0     0     0   0 12:25 ?        00:00:00 [kworker/0:1]
root        1042       2  0     0     0   7 12:25 ?        00:00:00 [kworker/7:0-events]
toor        1045     887 99  2785  4112   5 12:28 pts/0    00:00:00 ps -AF

```

- as above + ASCII hierarchy (UNIX)
```
$ ps -AFH | head
UID          PID    PPID  C    SZ   RSS PSR STIME TTY          TIME CMD
root           2       0  0     0     0   5 12:10 ?        00:00:00 [kthreadd]
root           3       2  0     0     0   0 12:10 ?        00:00:00   [rcu_gp]
root           4       2  0     0     0   0 12:10 ?        00:00:00   [rcu_par_gp]
...
rtkit        642       1  0  5699  1608   3 12:10 ?        00:00:00   /usr/libexec/rtkit-daemon
toor         850       1  0  4867 10312   1 12:16 ?        00:00:00   /lib/systemd/systemd --user
toor         851     850  0 42651  4664   5 12:16 ?        00:00:00     (sd-pam)
toor         866     850  0 92437 25744   5 12:16 ?        00:00:00     /usr/bin/pulseaudio --daemonize=no --log-target=journal
toor         908     850  0  2302  3780   6 12:16 ?        00:00:00     /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
```

**NOTE**: in case lines are truncated, the display can be widened with `-w` or `-ww`<br/>

- all processes + user-oriented format (BSD)
```
$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.5 168456 11572 ?        Ss   12:10   0:00 /sbin/init
root           2  0.0  0.0      0     0 ?        S    12:10   0:00 [kthreadd]
...
root         941  0.0  0.0      0     0 ?        I    12:16   0:00 [kworker/1:0]
root         973  0.0  0.0      0     0 ?        I    12:20   0:00 [kworker/7:2-mm_percpu_wq]
root        1041  0.0  0.0      0     0 ?        I    12:25   0:00 [kworker/0:1]
root        1042  0.0  0.0      0     0 ?        I    12:25   0:00 [kworker/7:0-mm_percpu_wq]
toor        1050  100  0.2  11140  4112 pts/0    R+   12:29   0:00 ps aux
```

- as above + ASCII hierarchy (BSD)
```
$ ps auxf
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           2  0.0  0.0      0     0 ?        S    12:10   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   12:10   0:00  \_ [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   12:10   0:00  \_ [rcu_par_gp]
...
rtkit        642  0.0  0.0  22796  1608 ?        SNsl 12:10   0:00 /usr/libexec/rtkit-daemon
toor         850  0.0  0.5  19468 10312 ?        Ss   12:16   0:00 /lib/systemd/systemd --user
toor         851  0.0  0.2 170604  4664 ?        S    12:16   0:00  \_ (sd-pam)
toor         866  0.0  1.2 369748 25744 ?        Ssl  12:16   0:00  \_ /usr/bin/pulseaudio --daemonize=no --log-target=journal
toor         908  0.0  0.1   9208  3780 ?        Ss   12:16   0:00  \_ /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
```

----

### Useful links
- [Linux ps command - 20 Real Life Examples](https://www.digitalocean.com/community/tutorials/linux-ps-command)

