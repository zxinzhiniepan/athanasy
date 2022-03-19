# 安装Gentoo
## 准备工作
### 分区
> 1.`lsblk`查看接入到系统中的块设备
> ```shell
livecd ~ # lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0   4.8G  1 loop /mnt/livecd
sda      8:0    0 447.1G  0 disk
├─sda1   8:1    0   529M  0 part
├─sda2   8:2    0   100M  0 part
├─sda3   8:3    0    16M  0 part
├─sda4   8:4    0   100G  0 part
├─sda5   8:5    0   512M  0 part
└─sda6   8:6    0  55.1G  0 part
sdb      8:16   0 465.8G  0 disk
├─sdb1   8:17   0    16M  0 part
├─sdb2   8:18   0   100G  0 part
├─sdb3   8:19   0     8G  0 part
├─sdb4   8:20   0    20G  0 part
├─sdb5   8:21   0    50G  0 part
├─sdb6   8:22   0    50G  0 part
└─sdb7   8:23   0   6.3G  0 part
sdc      8:32   1  28.9G  0 disk /mnt/cdrom
├─sdc1   8:33   1   4.9G  0 part
└─sdc2   8:34   1  10.5M  0 part
> ```

> 2.`df`查看硬盘的使用情况
>```shell
livecd ~ # df -h
Filesystem      Size  Used Avail Use% Mounted on
none            3.5G  1.5M  3.5G   1% /run
udev             10M     0   10M   0% /dev
tmpfs           3.5G     0  3.5G   0% /dev/shm
/dev/sdc        4.9G  4.9G     0 100% /mnt/cdrom
overlay         3.5G   65M  3.5G   2% /
none            3.5G   65M  3.5G   2% /mnt/overlay
/dev/loop0      4.8G  4.8G     0 100% /mnt/livecd
cgroup_root      10M     0   10M   0% /sys/fs/cgroup
tmpfs           712M   16K  712M   1% /run/user/1000
tmpfs           712M     0  712M   0% /run/user/0
>```

> 3.`lsscsi`打印SCSI硬盘信息
> ```shell
livecd ~ # lsscsi
[0:0:0:0]    disk    ATA      GLOWAY STK480GS3 1.00  /dev/sda
[1:0:0:0]    disk    ATA      WDC WD5000LPVX-0 1A03  /dev/sdb
[2:0:0:0]    disk    Kingston DataTraveler 3.0 0000  /dev/sdc
> ```

> 4.`blkid`打印块设备信息
>```shell
livecd ~ # blkid
/dev/sdb4: UUID="4db21b81-8837-460c-ab29-cd6f682a56d4" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="var" PARTUUID="b86bd5aa-82cc-472b-a093-f0cc89aba49e"
/dev/sdb2: LABEL="home" BLOCK_SIZE="512" UUID="CC0AA4770AA45FE6" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="5c6f237d-9dc6-46ba-8942-d656b6637322"
/dev/sdb7: UUID="59b683c4-8b37-4655-b206-912dcf72449d" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="tmp" PARTUUID="8dad841c-1121-408b-a39a-5ea1a40906d7"
/dev/sdb5: UUID="3563a105-788e-4243-925e-b55f709199da" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="home" PARTUUID="004f91cd-9293-44e1-b531-f50b1294bfe1"
/dev/sdb3: UUID="0af692ab-f0d6-42da-90a1-b1e87814b15a" TYPE="swap" PARTLABEL="swap" PARTUUID="66e3afc3-6872-49c1-af20-7e793bd4f0ad"
/dev/sdb1: PARTLABEL="Microsoft reserved partition" PARTUUID="e36dbfa1-78c7-4350-a75c-f953b52ce183"
/dev/sdb6: UUID="d830a7d0-79bb-497e-b556-ff62487072c0" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="opt" PARTUUID="11064dcb-d639-43f2-b087-b5291f73daa1"
/dev/loop0: TYPE="squashfs"
/dev/sdc2: SEC_TYPE="msdos" LABEL_FATBOOT="GENTOOLIVE" LABEL="GENTOOLIVE" UUID="3A2F-02C8" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="4d4a293b-02"
/dev/sdc1: BLOCK_SIZE="2048" UUID="2022-03-15-14-33-07-27" LABEL="Gentoo amd64 LiveGUI 20220315T09" TYPE="iso9660" PTUUID="4d4a293b" PTTYPE="dos" PARTUUID="4d4a293b-01"
/dev/sda4: BLOCK_SIZE="512" UUID="A05276BB527695AE" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="9682df9e-9009-42f4-91ff-6e3672491119"
/dev/sda2: UUID="7838-23EA" BLOCK_SIZE="512" TYPE="vfat" PARTLABEL="EFI system partition" PARTUUID="cbe57e36-c732-44dc-9177-e5910fb8b6de"
/dev/sda5: UUID="DC60-850E" BLOCK_SIZE="512" TYPE="vfat" PARTLABEL="boot" PARTUUID="538d0b0f-b148-4faa-9a35-f7752ac7ce36"
/dev/sda3: PARTLABEL="Microsoft reserved partition" PARTUUID="eb82a348-f68a-4f63-81dc-96ee599c02a7"
/dev/sda1: BLOCK_SIZE="512" UUID="B66AC8016AC7BBFD" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="f963ba68-908b-4e0a-9aa9-134170f6f3f6"
/dev/sda6: UUID="7f1cee7b-5f15-45f9-84b2-cd9aa907011e" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="rootfs" PARTUUID="563a623f-4a37-4bcc-8d8a-2667480bef85"
>```

> 5.`lshw`打印硬件详细信息
>```shell
livecd ~ # lshw
  *-input:8
       product: Power Button
       physical id: a
       logical name: input8
       logical name: /dev/input/event7
       capabilities: platform
>```

#### 

## 配置安装环境

## 安装

## 配置基础系统

## 使用gentoo

## 完成基础配置

## 使用portage

## 配置无线网络

## 配置tmux

## 设置桌面环境(i3wm)




