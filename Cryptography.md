##### A great place to find more hash formats and password prefixes is the hashcat example page, available here: https://hashcat.net/wiki/doku.php?id=example_hashes.
#### RSA tools
```
https://github.com/RsaCtfTool/RsaCtfTool
```
```
https://github.com/ius/rsatool
```
#### SSH - key generating 
```
ssh-keygen -t rsa -b 4096
```
- The private key --`~/.ssh/id_rsa`
- The public key -- `~/.ssh/id_rsa.pub`

#### GPG- encrypt decrypt the files
```
gpg --output decrypted_file.txt --decrypt encrypted_file.gpg
```