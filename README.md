# Scripts Backup &amp; Restore container for LXD

Before backup or restore container you must to stop container
```
lxc stop test
```


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



# Import backup as LXD image

```
lxc image import /backup/lxc/test/snap-test-2016-08-19.tar.bz2 --alias my-new-image
```

Run image:
```
lxc launch me-new-image test2
```