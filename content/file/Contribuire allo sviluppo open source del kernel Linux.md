#seminar 
# How to compile and install the Linux kernel
## How to compile the kernel
### First, which Linux Kernel?
See [kernel.org](https://kernel.org) for more.
Linux main line (the one from [[Linus Torvalds]]), is the frequently updated, unstable release.
The stable release is found on the github page of the user `gregkh`. Here we also find lots of versions, the one with `rc` are the `release candidates`.
### Compiling
A simple `make` doesn't work: [[Linux]] supports multiple architectures, we need to specify for which one we want to build:
```shell
make menuconfig
```
Questo comando offre una GUI per visualizzare tutte le opzioni per la compilazione.
Items selected with `M` are *modularized*, they are built apart from the kernel and are loaded on the disk when needed.
With `lsmod` we can see which modules are currently loaded.

> In `/boot/config-version` we find every option selected for the compilation.

After we have decided the options:
```shell
make -j$(nproc)
```
## How to install the kernel
```shell
make binrpm-pkg
# or
make install # this installes the kernel on the CURRENT machine
# or 
make modules_install # for installing the modules
```
This generates RPMs: packets for the kernel
```shell
dnf install *rpm
```
## Finding the aliases for the modules
```shell
less modules.alias # non so dove sia sto file
```
## Out-of-tree compilation
This is compiling single modules without recompiling the entire kernel, this is done by compiling these modules using another kernel.
This way we can distribute compiled drivers, without revealing the source files.
# What is virtio-vsock
## What is VirtIO
VirtIO is a standard for creating virtual devices.
When virtualizing, we do not need to emulate every part of a machine, so we use **para-virtualization**: the guest knows it is a vm, and doesn't utilize every part of the computer.
## virtio-vsock
Create by VMware, it is a driver for sockets for virtual machines, it is need for the communication between virtual and physical machine.
# How does the virtio-vsock driver work
-
# How to contribute to Linux
It is not as simple as opening PRs on Torvald's GitHub.
Linux contribution goes via email (lol). 
We use [[Git]] to create the change log, and send the change log via email to `address`.
Why? [[GitHub]] is owned by [[Microsoft]], email is open.

Linux is divided into subtrees.
There is a MAINTAINERS File (can be found directly in the Kernel), containing emails of maintainers.
There are maintainers for every subtree.
## How
```shell
git diff
git add -u
git commit -s -m "commit bellissimo"
git log
git send-email
git format-patch -1
git send-email --to=email nomecommit
~/.gitconfig # contiene i file per le informazioni da includere nelle mail automatiche
# client gmail da terminale: neomutt

```