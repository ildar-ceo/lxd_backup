# Создание бэкапов
Данный метод создает бэкапы контейнеров как LXD образы, готовые к импорту. В идеале нужно создавать снимки и отправлять их в приватный репозиторий LXD. Но иногда, этого сделать нельзя. Например, у небольшой компании нет возможности покупать еще один сервер. В этом случае можно обойтись простым решением tar + Amazon S3. 

Скачайте готовые скрипты для создания и восстановления бэкапов:

```bash
wget https://github.com/vistoyn/lxd_backup/raw/1.2/scripts/lxc-backup -O "/usr/local/bin/lxc-backup"
wget https://github.com/vistoyn/lxd_backup/raw/1.2/scripts/lxc-restore -O "/usr/local/bin/lxc-restore"
```
Установите флаг выполнения для скриптов:

```bash
chmod +x /usr/local/bin/lxc-restore
chmod +x /usr/local/bin/lxc-backup
```
Перед созданием и восстановлением бэкапов нужно остановить работающий контейнер. Можно, в принципе, делать бэкап на работающем контейнере, но при создании бэкапа возможна потеря некоторых данных (зависит от установленных программ в контейнере).

## Для dir

Данная команда создаст бэкап контейнера test, сожмет файл в архив и сохранит его на диске в папке /backup/lxc/test:

```bash
lxc stop test
lxc-backup test
```
Восстановление бэкапа из снимка:

```bash
lxc-restore test /backup/lxc/test/snap-test-2016-08-19.tar.bz2
```
## Для zfs
Для ZFS после имени контейнера нужно добавлять «.zfs»

Создание бэкапа:

```bash
lxc stop test
lxc-backup test.zfs
```

Восстановление бэкапа из снимка:
```bash
lxc-stop test
lxc-restore test.zfs /backup/lxc/test/snap-test.zfs-2016-08-19.tar.bz2
```
# Импорт бэкапа
На новом хосте иногда потребуется создать контейнер из бэкапа. Для этого нужно сначала импортировать образ, а затем его запустить как контейнер.

Команда импорта бэкапа как образа LXD:

```bash
lxc image import /backup/lxc/test/snap-test-2016-08-19.tar.bz2 --alias my-new-image
```
Команда запуска образа как контейнера:

```bash
lxc launch me-new-image test2
```
