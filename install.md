# Installation

## Connecting to wi-fi

Enable DHCP

```
# vim /etc/iwd/main.conf
```

```
/etc/iwd/main.conf

[General]
EnableNetworkConfiguration=true
```

```
# iwctl
```

```
[iwd]# device list
[iwd]# station wlan0 scan
[iwd]# station wlan0 get-networks
[iwd]# station wlan0 connect SSID
[iwd]# station wlan0 show
```


## Set timezone

```
# timedatectl set-ntp true
# timedatectl set-timezone Europe/Warsaw
# timedatectl status.
```

## Partition disk

```
# fdisk /dev/nvme0n1
```

### Create new table

```
> g
```

### Create EFI system partition

```
> n
> 
>
> +300M
```

Change type:

```
> t
> 1
```

### Create swap

```
> n
>
>
> +8G
```

Change type:

```
> t
> 2
> 19
```

### Main partition

```
> n
>
>
>
```

### Save changes and quit

```
> w
```

## Format the partitions

```
# mkfs.ext4 /dev/nvme0n1p3
```

```
# mkswap /dev/nvme0n1p2
```

```
# mkfs.fat -F 32 /dev/nvme0n1p1
```

## Mount volumes

```
# mount /dev/nvme0n1p3 /mnt
# mount /dev/nvme0n1p1 /mnt/efi --mkdir
# swapon /dev/nvme0n1p2
```

## Installation

```
# pacstrap /mnt base linux linux-firmware vim
# genfstab -U /mnt >> /mnt/etc/fstab
# arch-chroot /mnt
```

### Set time zone

```
[root@archiso /]# ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime
[root@archiso /]# hwclock --systohc
[root@archiso /]# vim /etc/locale.gen
[root@archiso /]# locale-gen
[root@archiso /]# echo "LANG=en_US.UTF-8" > /etc/locale.conf
[root@archiso /]# echo "KEYMAP=pl" > /etc/vconsole.conf
```

### Hostname

```
[root@archiso /]# echo "thinkpad" > /etc/hostname
```

### Create root password

```
[root@archiso /]# passwd
```

### Bootloader

```
[root@archiso /]# pacman -S grub efibootmgr
[root@archiso /]# grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
[root@archiso /]# grub-mkconfig -o /boot/grub/grub.cfg
```

### Exit chroot

```
[root@archiso /]# exit
# umount -R /mnt
# reboot
```

