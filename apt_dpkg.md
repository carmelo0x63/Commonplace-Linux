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
<br/>

#### apt-cache
```
$ apt-cache policy curl
curl:
  Installed: 7.88.1-10+deb12u8
  Candidate: 7.88.1-10+deb12u8
  Version table:
     8.11.1-1~bpo12+1 100
        100 http://ftp.linux.it/debian bookworm-backports/main amd64 Packages
 *** 7.88.1-10+deb12u8 500
        500 http://ftp.linux.it/debian bookworm/main amd64 Packages
        100 /var/lib/dpkg/status
     7.88.1-10+deb12u5 500
        500 http://security.debian.org bookworm-security/main amd64 Packages
```
<br/>

```
$ apt-cache depends curl
curl
  Depends: libc6
  Depends: libcurl4
  Depends: zlib1g
```
<br/>

```
$ apt-cache rdepends libcurl4
libcurl4
Reverse Depends:
  curl
  ...
```
<br/>

### dpkg and dpkg-query: examples
- `dpkg -l|--list [<pattern>...]`: list packages
```
$ dpkg -l | grep curl
ii  curl                                       7.88.1-10+deb12u8                      amd64        command line tool for transferring data with URL syntax
ii  libcurl3-gnutls:amd64                      7.88.1-10+deb12u8                      amd64        easy-to-use client-side URL transfer library (GnuTLS flavour)
ii  libcurl4:amd64                             7.88.1-10+deb12u8                      amd64        easy-to-use client-side URL transfer library (OpenSSL flavour)
ii  python3-pycurl                             7.45.2-3                               amd64        Python bindings to libcurl (Python 3)
```
<br/>

- `dpkg -S|--search <pattern>...`: find package(s) owning file(s)
```
$ dpkg -S curl
libcurl3-gnutls:amd64: /usr/share/doc/libcurl3-gnutls/changelog.Debian.gz
papirus-icon-theme: /usr/share/icons/Papirus/64x64/apps/curlew.svg
bash-completion: /usr/share/bash-completion/completions/curl
libcurl4:amd64: /usr/share/doc/libcurl4
python3-pycurl: /usr/share/doc/python3-pycurl
...
```
<br/>

- `$ dpkg-query -W <pattern>`: show information on package(s)
```
$ dpkg-query -W curl
curl	7.88.1-10+deb12u8
```
