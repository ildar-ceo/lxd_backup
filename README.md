# lxc_backup
Scripts for LXC Backup &amp; Restore


# For backend type dir

## Backup LXC container


```bash
lxc stop test
lxc-backup test
```


## Restore LXC container


```bash
lxc stop test
lxc-restore test /backup/lxc/test/snap-test-2016-08-19.tar.bz2
```



# For backend type lxc


## Backup LXC container


```bash
lxc stop test
lxc-backup test.zfs
```


## Restore LXC container


```bash
lxc stop test
lxc-restore test /backup/lxc/test.zfs/snap-test.zfs-2016-08-19.tar.bz2
```
