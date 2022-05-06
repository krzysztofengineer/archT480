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
