#### Start metasploit
```
msfconsole
```
#### Payloads Creation(msfvenom)
```
msfvenom -p <payload> <options>
```
#### Search
```
search <name>
```
#### Module Info/Options/Sessions
```
info
```
```
show options
```
```
sessions -h
```

### Setting up a Data Base for results
```
systemctl start postgresql;
msfdb init;
msfconsole;
```
#### Select Workspace
```
workspace <name>
```
#### Add/delete workspace
```
workspace -a <name>
```
```
workspace -d <name>
```
#### Runs nmap in Workspace
```
db_nmap -sC -sV <ip> -p-
```
