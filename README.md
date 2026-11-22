# Home Assistant-guide: styr dit hjem fra din egen server

En dansk trin-for-trin-guide til at køre **Home Assistant i Docker** i en LXC-container
på Proxmox. Den bygger på mit eget homelab, men alle navne og IP-adresser er eksempler.

**Forudsætning:** En kørende Proxmox-server. Se [proxmox-guide](https://github.com/TechNetDK/proxmox-guide).

## Hvorfor Docker i en LXC-container?

En LXC-container bruger meget lidt RAM og CPU, og Home Assistant styres med de samme
`docker compose`-kommandoer som andre tjenester. Containeren har kun Home Assistant,
så den kan genstartes og opdateres for sig selv.

## Det jeg bruger

| Del | Værdi |
|---|---|
| Container | CT 102 |
| CPU | 2 kerner |
| RAM | 2 GB |
| Disk | 16 GB |
| Mappe | `/opt/homeassistant` |
| IP (eksempel) | 10.0.0.14 |

## Indhold

| # | Kapitel |
|---|---|
| 01 | [Opret en LXC-container med Docker](01-container-og-docker.md) |
| 02 | [Home Assistant i Docker](02-home-assistant-i-docker.md) |
| 03 | [Backup og opdatering](03-backup-og-opdatering.md) |
| 04 | [Fejl jeg har ramt, og løsningerne](04-fejl-og-loesninger.md) |
