# alpinewine

Wine with xvfb/x11/noVNC over alpine in docker

## Image

```bash
docker pull seancheung/alpinewine:<tag>
```

## Tags

| tag     | description                         |
| ------- | ----------------------------------- |
| wine    | wine x86 + xvfb                     |
| wine64  | wine x86_64 + xvfb                  |
| x11     | wine x86 + xvfb + x11vnc            |
| x1164   | wine x86_64 + xvfb + x11vnc         |
| novnc   | wine x86 + xvfb + x11vnc + novnc    |
| novnc64 | wine x86_64 + xvfb + x11vnc + novnc |

## Environments

| Name             | default         |
| ---------------- | --------------- |
| WINEDLLOVERRIDES | mscoree,mshtml= |
| WINEPREFIX       | /root/wine      |
| SCREEN           | 0 1280x1024x8   |
| DISPLAY          | :1              |
| LANG             | en_US.UTF-8     |
| LC_ALL           | en_US.UTF-8     |

> WINEDLLOVERRIDES: Wine DLL overrides.

> SCREEN: This option creates screen screennum and sets its width, height, and depth to W, H, and D respectively. By default, only screen 0 exists and has the dimensions 1280x1024x8.

## Custom build Args

### Base Image

| Name      | default |
| --------- | ------- |
| ARCH      | x86     |
| CN_MIRROR | false   |

> ARCH: x86, x86_64

> CN_MIRROR: Use AliCloud registry mirror

### Extended Image

| Name     | default |
| -------- | ------- |
| ARCH_TAG |         |

> ARCH: 64

## Usage

### Wine

> `wine` and `wine64` tags are used as base images. But you can still run programs headlessly with them.

To run a program in foreground:

```bash
docker run -d --name mywine -v /var/opt/myprogram:/path/to/myprogram seancheung/alpinewine:wine
docker exec mywine wine /var/opt/myprogram/myprogram.exe
```
> For `x86_64` use `wine64`

To run a program in background:

```bash
docker run -d --name mywine seancheung/alpinewine:wine

cat > myprogram.conf <<EOF
[program:myprogram]
command=/usr/bin/wine /path/to/myprogram.exe
priority=100
stdout_logfile=/var/log/myprogram.stdout.log
stderr_logfile=/var/log/myprogram.stderr.log
EOF

docker cp myprogram.conf mywine:/etc/supervisor/conf.d/
docker exec mywine supervisorctl reload
```
> For `x86_64` use `/usr/bin/wine64`

> For debugging purpose, add `environment=WINEDEBUG=warn+all`

### X11

| port | description   |
| ---- | ------------- |
| 5900 | x11vnc server |

### noVNC

| port | description   |
| ---- | ------------- |
| 5900 | x11vnc server |
| 8080 | noVNC         |
