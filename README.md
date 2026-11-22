# Home Assistant-guide: styr dit hjem fra din egen server

En dansk trin-for-trin-guide til at køre **Home Assistant i Docker** i den samme LXC-container
som medieserveren på Proxmox. Den bygger på mit eget homelab, men alle navne og IP-adresser er eksempler.

**Forudsætning:** En kørende Proxmox-server og en LXC-container med Docker.
Se [proxmox-guide](https://github.com/TechNetDK/proxmox-guide) og [medieserver-guide](https://github.com/TechNetDK/medieserver-guide).

## Hvorfor Docker i medieserverens container?

Docker kører allerede i medieserverens LXC-container, så Home Assistant kører ved siden af.
Det bruger kun lidt ekstra RAM og CPU, og det styres med de samme `docker compose`-kommandoer.

## Det jeg bruger

| Del | Værdi |
|---|---|
| Container | CT 101 (samme som medieserveren) |
| Ekstra RAM | ca. 1 GB |
| Mappe | `/opt/homeassistant` |
| IP (eksempel) | 10.0.0.13 |

## Indhold

| # | Kapitel |
|---|---|
| 01 | [Brug medieserverens container](01-container-og-docker.md) |
| 02 | [Home Assistant i Docker](02-home-assistant-i-docker.md) |
| 03 | [Backup og opdatering](03-backup-og-opdatering.md) |
| 04 | [Fejl jeg har ramt, og løsningerne](04-fejl-og-loesninger.md) |
