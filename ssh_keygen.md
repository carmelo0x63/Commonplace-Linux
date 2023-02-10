# `ssh-keygen`: OpenSSH authentication key utility
`ssh-keygen` generates, manages and converts authentication keys for `ssh`

----

### Generate a new key
```
$ ssh-keygen -t rsa -b 4096 -f <filename> -C "<comment>" -N "" -q
```

**NOTE**:
  `-t`: key type, e.g. `rsa`, `ed25519`
  `-b`: number of bits
  `-f`: filename
  `-C`: helpful comment
  `-N`: passphrase
  `-q`: quiet mode

Two files will be generated in the current directory, namely, <filename> and <filename>.pub:
```
-rw-------  1 <user>  <group>   3.3K Feb 10 12:15 <filename>
-rw-r--r--  1 <user>  <group>   750B Feb 10 12:15 <filename>.pub
```

### Verify a key
The typical scenario, one tries to ssh into a remote host and the following message pops up:
```
The authenticity of host '<ip_address>' can't be established.
ED25519 key fingerprint is SHA256:a1b***Zk9.
```
How can that `a1b***Zk9` fingerprint be validated?</br>
Well, evidently, we need to get support from the remote host admin. What if we are that persons? What are we supposed to do?</br>
`ssh-keygen` comes to the rescue in that we can invoke it with the `-l` ("show fingerprint of specified public key file") option. For instance:
```
$ ssh-keygen -lf /etc/ssh/ssh_host_ed25519_key.pub -E sha256
256 SHA256:a1b***Zk9 <comment> (ED25519)
```

If the two fingerprints match, we rest assured the server we're trying to connect to is the right one.

----

### Useful links
- []()

