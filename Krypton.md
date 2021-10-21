# [KRYPTON](https://overthewire.org/wargames/krypton)

## Level 0 -> Level 1
```bash
$ echo S1JZUFRPTklTR1JFQVQ= | base64 -d
KRYPTONISGREAT
```

## Level 1 -> Level 2
```bash
$ cat /krypton/krypton1/krypton2 | tr 'A-Za-z' 'N-ZA-Mn-za-m'
LEVEL TWO PASSWORD ROTTEN
```

## Level 2 -> Level 3
```bash
$ ln -s /krypton/krypton2/keyfile.dat 
$ echo 'ABCDEFGHIJKLMNOPQRSTUVWXYZ' > alphabet
$ chmod 777 .
$ /krypton/krypton2/encrypt alphabet 
$ cat ciphertext 
MNOPQRSTUVWXYZABCDEFGHIJKL #ROT 12
$ $ cat /krypton/krypton2/krypton3 | tr ‘m-za-lM-ZA-L’ ‘a-zA-Z’
CAESARISEASY
```

## Level 3 -> Level 4
**Ciphertext  : a b c d e f g h i j k l m n o p q r s t u v w x y z**
**Plaintext     : b o i h g k n q v t w y u r x z a j e m s l d f p c**

**Decrypt :** *WELL DONE THE LEVEL FOUR PASSWORD IS BRUTE*

## Level 4 -> Level 5
Decoder : **https://www.dcode.fr/vigenere-cipher**
Key : **FREKEY**
Password : **CLEARTEXT**

## Level 5 -> Level 6
Key: **KEYLENGTH**
Password: *RANDOM*

## Level 6 -> Level 7
```bash
$ ln -s /krypton/krypton6/keyfile.dat 
$ python3 -c "print('A'*100)" > test1
$ chmod 777 .
$ /krypton/krypton6/encrypt6 test1 cipher1
$ cat cipher1 
EICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZ
```
```python
#!/usr/bin/env python3
key = 'EICTDGYIYZKTHNSIRFXYCPFUEOCKRN'
cipher = 'PNUKLYLWRQKGKBE'

for i in range(len(cipher)):
    k = ord(cipher[i]) - ord(key[i])
    if k < 0: k += 26
    k += ord('A')
    print(chr(k), end='')
```

```bash
$ python3 decrypt.py
LFSRISNOTRANDOM
```
