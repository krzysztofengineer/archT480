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


