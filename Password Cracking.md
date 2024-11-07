### Hash-Identifier
```
hash-identifier <hash>
```


### John the Ripper(Jumbo john)

```
john --format=<hashformat> --wordlist=<path> <hash.txt>
```

show cracked pass
```
john --show <hash.txt>
```

##### Unshadow(merge passwd and shadow files)
```
unshadow </etc/passwd> </etc/shadow> > unshadow.txt
```

##### Single Crack Mode(makes wordlist  based on username filed in hash.txt and cracks hash)
```
john --format=<hashtype> --single <hash.txt>
```
hash.txt
```
<username>:<hash>
```

##### Custom Rules
```Rules
https://www.openwall.com/john/doc/RULES.shtml
```
In john.conf add--
```
[List.Rules:<rule_name>]
<___Rules__to be_Typed here>
```
usage
```
john --wordlist=<path> --rule=<rule_name> hash.txt
```

##### Zip2John(zip to john readable hash)
```
zip2john <path_to_zip> > hash.txt
```
##### Rar2John(rar file to hash)
```
rar2john <path_to_zip> > hash.txt
```


### Hashcat

```
hashcat -m<hash number> <hash.txt> <wordlistspath> --force
```