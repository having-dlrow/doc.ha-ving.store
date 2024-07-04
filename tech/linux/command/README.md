# Command

## Kernel

```
cat /etc/redhat-release
```

## Network

```
$ nmcli connection show
$ nmcli device show 
```

## lsattr

```
lsattr /usr/ | more
chattr -i /usr/bin
```

## Quota

```
quota -u {username}
Disk quotas for user ectaud2001 (uid 65541):
Filesystem blocks quota limit grace files quota limit grace
/dev/sda7 207092* 0 200000 14269 0 0
```

```
requota -a
```
