---
# type: docs 
title: Linux From Scratch
date: 2023-03-07T13:05:41Z
featured: false
draft: false
comment: true
toc: true
reward: true
pinned: false
carousel: false
series: [linux-from-scratch]
categories: [linux]
tags: []
images: []
---

Summary.

<!--more-->

# Preparing the Host System
## Hardware:
- CPU 4 cores
- RAM 16GB RAM
- OS: Ubuntu Server 18.04.6 LTS
## Software:
```
    bash>=3.2
    binutils>=2.13.1
    bison>=2.7
    coreutils>=6.9
    diffutils>=2.8.1
    findutils>=4.2.31
    gawk>=4.0.1
    gcc>=5.1
    grep>=2.5.1
    gzip>=1.3.12
    linux-kernel>=3.2
    m4>=1.4.10
    make>=4.0
    patch>=2.5.4
    perl>=5.8.8
    python>=3.4
    sed>=4.1.5
    tar>=1.22
    texinfo>=4.7
    xz>=5.0.0
```
- Run the following script to see whether the host system has all the appropriate packages
```
#!/bin/bash
# Simple script to list version numbers of critical development tools
export LC_ALL=C
bash --version | head -n1 | cut -d" " -f2-4
MYSH=$(readlink -f /bin/sh)
echo "/bin/sh -> $MYSH"
echo $MYSH | grep -q bash || echo "ERROR: /bin/sh does not point to bash"
unset MYSH

echo -n "Binutils: "; ld --version | head -n1 | cut -d" " -f3-
bison --version | head -n1

if [ -h /usr/bin/yacc ]; then
    echo "/usr/bin/yacc -> `readlink -f /usr/bin/yacc`";
elif [ -x /usr/bin/yacc ]; then
    echo yacc is `/usr/bin/yacc --version | head -n1`
else
    echo "yacc not found"
fi

echo -n "Coreutils: "; chown --version | head -n1 | cut -d")" -f2
diff --version | head -n1
find --version | head -n1
gawk --version | head -n1

if [ -h /usr/bin/awk ]; then
    echo "/usr/bin/awk -> `readlink -f /usr/bin/awk`";
elif [ -x /usr/bin/awk ]; then
    echo awk is `/usr/bin/awk --version | head -n1`
else
    echo "awk not found"
fi

gcc --version | head -n1
g++ --version | head -n1
grep --version | head -n1
gzip --version | head -n1
cat /proc/version
m4 --version | head -n1
make --version | head -n1
patch --version | head -n1
echo Perl `perl -V:version`
python3 --version
sed --version | head -n1
tar --version | head -n1
makeinfo --version | head -n1 # texinfo version
xz --version | head -n1

echo 'int main(){}' > dummy.c && g++ -o dummy dummy.c
if [ -x dummy ]
    then echo "g++ compilation OK";
    else echo "g++ compilation failed"; fi
rm -f dummy.c dummy
```
Since I'm using ubuntu-server-18.04.6 lts, We'll have to install few more packages
```
    sudo apt install -y g++ gcc texinfo make m4 bison
```
Also, We need to create a symbolic link (or hard link) for /bin/sh to /bin/bash
```
    sudo unlink /bin/sh
    sudo ln -s /bin/bash /bin/sh
```

Test