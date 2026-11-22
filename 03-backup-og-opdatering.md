# 03 – Backup og opdatering

## 1. Automatisk backup i Home Assistant
**Indstillinger → System → Sikkerhedskopiering** → **Opsæt automatisk sikkerhedskopiering**:
- Dagligt
- Opbevaring: fx 7 sikkerhedskopier
- Gem **krypteringsnøglen** et sikkert sted (fx din password-manager).

> Uden krypteringsnøglen kan backuppen **ikke** gendannes. Gem den, før du har brug for den.

## 2. Backup af hele containeren i Proxmox
Tag container 101 med i Proxmox' egen backup (se kapitel 07 i Proxmox-guiden).
Al opsætning ligger i `/opt/homeassistant` inde i containeren, så den kommer med
(i modsætning til medieserverens `/mnt/media`, som er et bind-mount).
Kopier backupperne til en anden disk – eller ud af huset.

## 3. Opdatering
> Snapshot i Proxmox virker ikke her, fordi containeren har medieserverens bind-mount.

1. Læs udgivelsesnoterne for **breaking changes**.
2. Lav en backup lige før: **Indstillinger → System → Sikkerhedskopiering → Sikkerhedskopiér nu**.
   Skriv den version ned, du kører nu (**Indstillinger → Om**).
3. Opdater inde i containeren:
   ```bash
   cd /opt/homeassistant
   docker compose pull
   docker compose up -d
   docker image prune -f
   ```
4. Gik det galt, så sæt den gamle version ind i compose-filen, fx
   `image: ghcr.io/home-assistant/home-assistant:<gammel version>`, og kør `docker compose up -d`.
   Virker det stadig ikke, så gendan backuppen fra trin 2.

> Vil du selv bestemme, hvornår der opdateres, så lås versionen i compose-filen,
> fx `image: ghcr.io/home-assistant/home-assistant:<version>`.

## 4. Gendan en backup
Backupperne ligger i `/opt/homeassistant/config/backups`. Kopier backup-filen et sikkert sted hen,
og start Home Assistant med en tom `config`-mappe. Vælg **Gendan fra sikkerhedskopi** i den første
opsætning, og indtast krypteringsnøglen.
