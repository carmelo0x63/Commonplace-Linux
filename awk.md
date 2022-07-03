# `awk`: pattern-directed scanning and processing language
Awk scans each input file for lines that match any of a set of patterns specified either on the command line or in multiple file(s). With each pattern there can be an associated action that will be performed when a line of a file matches the pattern. Each line is matched against the pattern portion of every pattern-action statement; the associated action is performed for each matched pattern.
</br>
AWK is, in fact, an acronym. It takes its name from the initial of its inventors: Alfred Aho, Peter Weinberger, and Brian Kernighan.

----

### Test file
The file we'll be testing against is below.
```
aaa = 111
bbb = 222
abc = 999
ccc = 333
ddd = 444
```

### Show lines between pattern(s)
```
$ awk '/bbb/,/ccc/' test.txt
bbb = 222    ### only lines between "bbb"
abc = 999
ccc = 333    ### ... and "ccc" are displayed
```

### Re-format stream on-the-fly
```
$ awk '{ print $3 ": " $1}' test.txt
111: aaa
222: bbb
999: abc
333: ccc
444: ddd
```
**NOTE**: `$0` is the whole line

----

### Useful links
- [The Linux AWK Command – Linux and Unix Usage Syntax Examples](https://www.freecodecamp.org/news/the-linux-awk-command-linux-and-unix-usage-syntax-examples/)
- [AWK - Basic Examples](https://www.tutorialspoint.com/awk/awk_basic_examples.htm#)
- [AWK command in Unix/Linux with examples](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
- [30 Examples for Awk Command in Text Processing](https://likegeeks.com/awk-command/)
- [10 Awesome Awk Command Examples](https://linuxhint.com/awk-command-examples/)

