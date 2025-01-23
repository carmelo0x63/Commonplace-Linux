# `sed`: Stream EDitor
The sed utility reads the specified files, or the standard input if no files are specified, modifying the input as specified by a list of commands.  The input is then written to the standard output.

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
The commands are issued to produce an immediate output. To edit the file in place add the switch `-i`.

### Replace one word
```
$ sed "s/aaa/AAA/" test.txt
AAA = 111    ### "aaa" has been substituted with "AAA"
bbb = 222
abc = 333
...
```

### Replace one line
```
$ sed "s/aaa.*/AAA = 444/" test.txt
AAA = 444    ### the whole line has been replaced
bbb = 222
abc = 333
...
```

### Add text after a specific line
```
$ sed "/bbb/a ccc = 444" test.txt
aaa = 111
bbb = 222
ccc = 444    ### "ccc..." has been inserted between "bbb..." and "abc..."
abc = 333
...
```

### Add text before a specific line
```
$ sed "/bbb/i ccc = 444" test.txt
aaa = 111
ccc = 444    ### "ccc..." is now before "bbb..."
bbb = 222
abc = 333
...
```

### Delete line containing a string
```
$ sed "/abc.*/d" test.txt
aaa = 111
bbb = 222
ccc = 333
ddd = 444
```

----

### Capture groups
```
echo 'Hello baby!' | sed 's/\(Hello\) \(baby!\)/\1 world! Bye \2/'
Hello world! Bye baby!
```

#### Explanation:
1. the string `Hello baby!` is piped into `sed`
2. `sed` searches (`s/???/.../`) both `Hello` and `baby!` strings (within the escaped parentheses `\(` and `\)`)
3. the following internal variables are created `\1 = Hello` and `\2 = baby!`
4. the final output is `\1 world! Bye \2` (determined by the second set of slashes, `s/.../???/`), corresponding to `Hello world! Bye baby!`

----

### Useful links
- [Sed Command in Linux/Unix with examples](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/)
- [50 sed Command Examples](https://linuxhint.com/50_sed_command_examples/)
- [sed examples of capture groups](https://linuxhint.com/sed-capture-group-examples/)
- [These 10 Sed Examples Will Make You a Linux Power User](https://www.makeuseof.com/sed-examples/)
- [How to Use sed Command to Delete a Line](https://phoenixnap.com/kb/sed-delete-line)

