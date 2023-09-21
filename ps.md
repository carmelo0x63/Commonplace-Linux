# `ps`: report a snapshot of the current processes
`ps` displays information about a selection of the active processes. Several versions of `ps` exist, each of them may accept different options:
1. UNIX options, which may be grouped and must be preceded by a dash, e.g. `ps -abc`
2. BSD options, which may be grouped and must not be used with a dash, e.g. `ps abc
3. GNU long options, which are preceded by two dashes, e.g. `ps --aaa --bbb --ccc`

----

```
$  ps -auxwf
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           2  0.0  0.0      0     0 ?        S    08:02   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   08:02   0:00  \_ [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   08:02   0:00  \_ [rcu_par_gp]
root           5  0.0  0.0      0     0 ?        I    08:02   0:00  \_ [kworker/0:0-events]
root           6  0.0  0.0      0     0 ?        I<   08:02   0:00  \_ [kworker/0:0H-events_highpri]
...
root         721  0.1  0.7 882876 59712 tty7     Ssl+ 08:02   0:05  \_ /usr/lib/xorg/Xorg :0 -seat seat0 -auth /var/run/lightdm/root/:0 -nolisten tcp vt7 -novtswitch
root        1494  0.0  0.1 166292  9408 ?        Sl   08:03   0:00  \_ lightdm --session-child 12 21
<user>      1527  0.0  0.3 379520 26320 ?        Ssl  08:03   0:00      \_ cinnamon-session --session cinnamon
<user>      1649  0.0  0.0   6024   468 ?        Ss   08:03   0:00          \_ /usr/bin/ssh-agent /usr/bin/im-launch cinnamon-session-cinnamon
...
```

----

### Useful links
- []()

