# `openssl`: OpenSSL command line tool
OpenSSL is a cryptography toolkit implementing the Transport Layer Security (TLS v1) network protocol, as well as related cryptography standards.
The `openssl` program is a command line tool for using the various cryptography functions of openssl's crypto library from the shell.

----

### Display version, basic info
```
$ openssl version
```

```
$ openssl list-standard-commands
asn1parse
ca
certhash
ciphers
...
```
**NOTE**: `openssl list-standard-commands | list-message-digest-commands | list-cipher-commands | list-cipher-algorithms | list-message-digest-algorithms | list-public-key-algorithms`

----

### Private key
#### Generate a private key with algorithm = RSA, bits = 2048
```
$ openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out private-key.pem
```

A new file will appear with the following contents:
```
 cat private-key.pem 
-----BEGIN PRIVATE KEY-----
MIIEvwIBADANBgkqhkiG9w0BAQEFAASCBKkwggSlAgEAAoIBAQDB3Bj2yINMkC93
...
-----END PRIVATE KEY-----
```

### Verify private key
```
$ openssl pkey -in private-key.pem -text -noout
RSA Private-Key: (2048 bit)
modulus:
    00:c1:dc:18:f6:c8:83:4c:90:2f:77:4c:86:bf:cb:
    d5:5b:28:57:43:ac:c8:19:e5:65:f9:07:cc:cc:03:
    ...
publicExponent: 65537 (0x10001)
privateExponent:
    ...
```

----

### Public key
#### Generate public key from private key
```
$ openssl pkey -in private-key.pem -out public-key.pem -pubout
```

### Verify public key
```
$ openssl pkey -in public-key.pem -pubin -text -noout
RSA Public-Key: (2048 bit)
Modulus:
    00:c1:dc:18:f6:c8:83:4c:90:2f:77:4c:86:bf:cb:
    ...
Exponent: 65537 (0x10001)
```

----

### Verify match between private key and public key
```
$ openssl rsa -in private-key.pem -modulus -noout | md5
d5f4ea26228f53c3259ed82060e7eb33

$ openssl rsa -in public-key.pem -pubin -modulus -noout | md5
d5f4ea26228f53c3259ed82060e7eb33
```

----

### Links
- [OpenSSL - Command Line Utilities](https://wiki.openssl.org/index.php/Command_Line_Utilities)
- [The Most Common OpenSSL Commands](https://www.sslshopper.com/article-most-common-openssl-commands.html)

