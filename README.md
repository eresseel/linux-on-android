# linux-on-android

## Install Alpine Linux on Termux using QEMU

```bash
wget https://raw.githubusercontent.com/eresseel/linux-on-android/main/alpine/install-qemu-and-run-vm.sh
bash install-qemu-and-run-vm.sh
```

Login with user `root` (no password)

## Setup network (press Enter to use defaults)

```
localhost:~# setup-interfaces
 Available interfaces are: eth0.
 Enter '?' for help on bridges, bonding and vlans.
 Which one do you want to initialize? (or '?' or 'done') [eth0] 
 Ip address for eth0? (or 'dhcp', 'none', '?') [dhcp] 
 Do you want to do any manual network configuration? [no] 
 localhost:~# ifup eth0
```

## Setting google dns

```
echo "nameserver 8.8.8.8" > /etc/resolv.conf
echo "nameserver 8.8.4.4" >> /etc/resolv.conf
```

## Download an answerfile to speed up installation

```bash
wget https://raw.githubusercontent.com/eresseel/linux-on-android/main/alpine/answerfile
```

## Patch setup-disk to enable serial console output on boot

```bash
sed -i -E 's/(local kernel_opts)=.*/\1="console=ttyS0"/' /sbin/setup-disk
```

## Run setup to install to disk

```bash
setup-alpine -f answerfile
```

## Poweroff VM

```bash
poweroff
```

## Download run-vm.sh file

```bash
wget https://raw.githubusercontent.com/eresseel/linux-on-android/main/alpine/run-vm.sh
bash run-vm.sh
```

### Install docker and enable on boot

```bash
apk update && apk add docker
service docker start
rc-update add docker
```
