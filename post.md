# Post-installation

## Create user

```
# useradd -m krzysztof
# passwd krzysztof
```

## Add user to sudoers

```
# EDITOR=vim visudi
```

```
/etc/sudoers.tmp

# Uncomment this line
wheel      ALL=(ALL:ALL) ALL
```

```
# usermod -aG wheel krzysztof
```


## Set up wi-fi connection

```
# systemctl enable NetworkManger.service
# sudo nmcli device wifi connect NETWORK_NAME password PASSWORD
```
