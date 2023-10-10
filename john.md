# JohnTheRipper
install
sudo apt install john

john [options] [path to file]

### Automatic Cracking
john --wordlist=[path to wordlist] [path to file]

john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt

### Format-Specific Cracking
john --format=[format] --wordlist=[path to wordlist] [path to file]

john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt

# wordlist
https://github.com/danielmiessler/SecLists

## Identifying Hashes
hash-id.py

john --list=formats and either check manually, or grep for your hash type using something like john --list=formats | grep -iF "md5"

john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt

john --format=raw-sha1 --wordlist=/usr/share/wordlists/rockyou.txt hash2.txt

john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash3.txt

john --format=Whirlpool --wordlist=/usr/share/wordlists/rockyou.txt hash4.txt

## For Windows ntlm
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt ntlm.txt

## Shadow file Cracking Hashes from /etc/shadow

FILE 1 - local_passwd

Contains the /etc/passwd line for the root user:

root:x:0:0::/root:/bin/bash

FILE 2 - local_shadow

Contains the /etc/shadow line for the root user:
root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::

john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt etchashes.txt

## Single Crack Mode
file content:
mike:1efee03cdcb96d90ad48ccc7b8666033

john --single --format=[format] [path to file]
find the format of hash

john --single --format=raw-md5 hash7.txt

## Zip file
zip2john [options] [zip file] > [output file]
zip2john zipfile.zip > zip_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt

## Rar2john
rar2john [rar file] > [output file]
rar2john rarfile.rar > rar_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt

## ssh cracking
ssh2john [id_rsa private key file] > [output file]
ssh2john id_rsa > id_rsa_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt