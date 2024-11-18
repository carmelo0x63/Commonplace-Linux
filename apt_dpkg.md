# apt and dpkg
Both `apt` and `dpkg` are command line interfaces to Debian package management system. While `dpkg` is a medium-level tool, with many options, `apt` is intended as an end user interface enabling options better suited for interactive usage. 

----

### apt's most used options
```
  search        - Search for a package by name and/or expression

  update        - Download lists of new/upgradable packages
  upgrade       - Perform a safe upgrade
  dist-upgrade  - Fully upgrade the system by allowing other package changes
  full-upgrade  - Same as 'dist-upgrade'

  autoclean     - Erase cache for packages no longer available
  autoremove    - Remove dependency packages no longer required
  clean         - Erase downloaded archive files

  depends       - Show package dependency information
  install       - Install and/or upgrade packages
  purge         - Remove packages and their system-wide configuration files
  reinstall     - Reinstall packages or install if not yet installed
  remove        - Remove packages
```

### dpkg's most used options
- `dpkg -l|--list [<pattern>...]`: list packages
```
$ dpkg -l | grep wireshark
rc  libwireshark-data                          4.0.11-1~deb12u1                       all          network packet dissection library -- data files
rc  wireshark-common                           4.0.11-1~deb12u1                       amd64        network traffic analyzer - common files
```

- `dpks -S|--search <pattern>...`: find package(s) owning file(s)
```
$ dpkg -S nmap
nmap-common: /usr/share/nmap/scripts/http-apache-server-status.nse
papirus-icon-theme: /usr/share/icons/Papirus/16x16/apps/org.nmap.Zenmap.svg
nmap-common: /usr/share/nmap/scripts/http-auth.nse
nmap-common: /usr/share/nmap/scripts/pop3-capabilities.nse
...
```
