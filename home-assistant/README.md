# Home-Assistant

Run Home Assistant image from [linuxserver.io](https://hub.docker.com/r/linuxserver/homeassistant)

## Manually Backup and Restore

Stop the service

```shell
dc stop
```

Runa bash shell on the service

```shell
docker-compose run --rm --entrypoint /bin/bash homeassistant
```

Copy all files from /config to separate location

```shell
cp -rp config/. config-new/
```

or

```shell
cp -rpT config/. config-new/
```

:warning: If you use an asterisk, the backup will not work

```shell
cp -rp config/* config-new
```

The default globbing in bash does not include filenames starting with a `.` (e.g. `.cloud` and
`.storage` dirs, and `.HA_VERSION`). So with `*`, you are asking to copy all files recursively
from this directory that can be expanded using `*`.

## Update Version

To update the version of home-assistant:

1) Update the desired version in the docker-compose.yaml file
1) Pull the new image (`docker-compose pull homeassistant`)
1) Update the container (docker-compose up -d homeassistant)
