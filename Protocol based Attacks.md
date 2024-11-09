### SMB(Server Message Block):- 
##### file sharing protocol windows

Enum
```
enum4linux -a <ip>
```
```
nmap --script smb-enum-users.nse,smb-enum-shares.nse,smb-enum-groups.nse 10.10.247.153 -p 445
```

connect
```
smbclient //<ip>/<share> -U <username> -p <port>
```
recursively download share
```
smbget -R smb://<ip>/<share>
```


### NFS(Network File System) 
##### common in linux, windows to linux etc

mount a share 
```
sudo mount -t nfs ip:share /tmp/mount/ -nolock
```

list visible nfs shares
```
/usr/sbin/showmount -e <ip>
```