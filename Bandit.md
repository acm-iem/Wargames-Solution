# [BANDIT](https://overthewire.org/wargames/bandit/)

## Level 0
```bash
$ ssh bandit0@bandit.labs.overthewire.org -p 2220 #Pass: bandit0
```

## Level 0 -> Level 1
```bash
$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

## Level 1 -> Level 2
```bash
$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

## Level 2 -> Level 3
```bash
$ cat spaces\ in\ this\ filename 
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
$ ssh bandit3@bandit.labs.overthewire.org -p 2220 
```

## Level 3 -> Level 4
```bash
$ cat inhere/.hidden 
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

## Level 4 -> Level 5
```bash
$ $ strings inhere/*
!TQO
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

## Level 5 -> Level 6
```bash
$ strings $(find ./ -type f -readable ! -executable -size 1033c)
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

## Level 6 -> Level 7
```bash
$ cat $(find / -size 33c -user bandit7 -group bandit6 2>/dev/null)
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

## Level 7 -> Level 8
```bash
$ $ cat data.txt | grep millionth
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

## Level 8 -> Level 9
```bash
$ sort data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

## Level 9 -> Level 10
```bash
$ strings data.txt | grep '=='  
========== the*2i"4
========== password
Z)========== is
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

## Level 10 -> Level 11
```bash
$ cat data.txt | base64 -d
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

## Level 11 -> Level 12
```bash
$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

## Level 12 -> Level 13
###  Script
```bash
#!/bin/bash
# cd $(mktemp -d)
xxd -r ~/data.txt > data.raw

decompress_gzip()
{
	echo -e "[+] Unzipping Gzip File: $@"
	mv $@ $@.gz
	gzip -d $@.gz
}

decompress_bzip2()
{
	echo -e "[+] Unzipping Bzip2 File: $@"
	mv $@ $@.bz2
	bzip2 -d $@.bz2
}

decompress_tar()
{
	echo -e "[+] Unzipping Tar File: $@"
	mv $@ $@.tar
	tar -xf $@.tar -O > $@
	rm $@.tar
}

decompress_gzip data.raw
decompress_bzip2 data.raw
decompress_gzip data.raw
decompress_tar data.raw
decompress_tar data.raw
decompress_tar data.raw
decompress_gzip data.raw
cat data.raw
```

### Output
```bash
[+] Unzipping Gzip File: data.raw
[+] Unzipping Bzip2 File: data.raw
[+] Unzipping Gzip File: data.raw
[+] Unzipping Tar File: data.raw
[+] Unzipping Tar File: data.raw
[+] Unzipping Tar File: data.raw
[+] Unzipping Gzip File: data.raw
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

## Level 13 -> Level 14
```bash
$ ssh -i sshkey.private bandit14@127.0.0.1
$ cat /etc/bandit_pass/bandit14 
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

## Level 14 -> Level 15
```bash
$ nc 127.0.0.1 3000
(UNKNOWN) [127.0.0.1] 3000 (?) : Connection refused
bandit14@bandit:~$ nc 127.0.0.1 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

## Level 15 -> Level 16
```bash
$ openssl s_client -connect 127.0.0.1:30001 -quiet
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
```

## Level 16 -> Level 17
```bash
$ nc -zv 127.0.0.1 31000-32000 2>&1 | cut -d " " -f3 | while read line; do echo '---Port:' $line '---'; echo cluFn7wTiGryunymYOu4RcffSxQluehd | openssl s_client -connect 127.0.0.1:$line -quiet  ; done
---Port: 31960 ---
140437173682240:error:141A10F4:SSL routines:ossl_statem_client_read_transition:unexpected message:../ssl/statem/statem_clnt.c:284:
---Port: 31790 ---
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

## Level 17 -> Level 18
```bash
$ diff passwords.old passwords.new 
42c42
< w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd  # This One
```

## Level 18 -> Level 19
```bash
$ scp -P 2220 bandit18@bandit.labs.overthewire.org:/home/bandit18/readme .
$ cat readme
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

## Level 19 -> Level 20
```bash
$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

## Level 20 -> Level 21
### Terminal 1
```bash
$ ./suconnect  6969
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```

### Terminal 2
```bash
$ nc -lnvp 6969
listening on [any] 6969 ...
connect to [127.0.0.1] from (UNKNOWN) [127.0.0.1] 56456
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

## Level 21 -> Level 22
```bash
$ cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

## Level 22 -> Level 23
```bash
$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
$ cat /tmp/$(echo I am user bandit23 | md5sum | cut -d ' ' -f 1)
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```
 
 ## Level 23 -> Level 24
 
```bash
$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
$ ls -lah /var/spool
drwxrwx-wx 41 root bandit24 4.0K Sep 28 07:54 bandit24
$ mkdir /tmp/whokilleddb
$ chmod 777 /tmp/whokilleddb
$ cd /tmp/whokilleddb
$ vi index.sh
$ cat index.sh
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/whokilleddb/bandit24
chmod 777 /tmp/whokilleddb/bandit24
$ chmod 777 index.sh
$ cp index.sh /var/spool/bandit24/
$ cat bandit24 
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

## Level 24 -> Level 25
```bash
$ for i in {0000..9999}; do  echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i" >> /tmp/whokilleddb; done
$ nc localhost 30002 < /tmp/whokilleddb | grep -i "password"
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```

## Level 25 -> Level 26
### Resize Window
```bash
$ ssh -i bandit26.sshkey bandit26@127.0.0.1
```
![](Images/Bandit-L26-L27.png)

```vi
V
```

```vim
:e /etc/bandit_pass/bandit26
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
:set shell=/bin/bash
:shell
```

## Level 26 -> Level 27
```bash
$ ./bandit27-do cat /etc/bandit_pass/bandit27
3ba3118a22e93127a4ed485be72ef5ea
```

## Level 27 -> Level 28
```bash
$ cd $(mktemp -d)
$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
$ cd repo
$ cat README 
The password to the next level is: 0ef186ac70e04ea33b4c1853d2526fa2
```

## Level 28 -> Level 29
```bash
$ cd $(mktemp -d)
$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
$ cd repo
$ git log | grep commit | cut -d " " -f2 | xargs git show
....
 - username: bandit29
-- password: bbc96594b4e001778eee9975372716b2
....
```

## Level 29 -> Level 30
```bash
$ cd $(mktemp -d)
$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
$ cd repo
$ git checkout origin/dev
$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf
```

## Level 30 -> Level 31
```bash
$ cd $(mktemp -d)
$ git clone ssh://bandit30-git@localhost/home/bandit30-git/repo
$ git tag 
list
secret
$ git show secret
47e603bb428404d265f59c42920d81e5
```

## Level 31 -> Level 32
```bash
$ cd $(mktemp -d)
$ git clone ssh://bandit31-git@localhost/home/bandit31-git/repo
$ cd repo
$ echo 'May I come in?' > key.txt
$ git add -f key.txt 
$ git commit -m "Commit"
$ git push origin master
....
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
....
```

## Level 32 -> Level 33
```bash
>> $0
$ cat /etc/bandit_pass/bandit33 
c9c3199ddf4121b10cf581a98d51caee
```

