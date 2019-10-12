# alpinewine

Wine with xvfb/x11/noVNC over alpine in docker

## Image

```bash
docker pull seancheung/alpinewine:<tag>
```

## Tags

| tag    | description        |
| ------ | ------------------ |
| wine32 | wine x86 + xvfb    |
| wine64 | wine x86_64 + xvfb |

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

| Name      | default |
| --------- | ------- |
| ARCH      | x86     |
| CN_MIRROR | false   |

> ARC: x86, x86_64

> CN_MIRROR: Use AliCloud registry mirror