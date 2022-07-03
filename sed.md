# `sed`: Stream EDitor
The sed utility reads the specified files, or the standard input if no files are specified, modifying the input as specified by a list of commands.  The input is then written to the standard output.

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
