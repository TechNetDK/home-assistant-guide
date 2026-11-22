# Home Assistant-guide: styr dit hjem fra din egen server

En dansk trin-for-trin-guide til at sætte **Home Assistant OS** op som en virtuel maskine
på Proxmox. Den bygger på mit eget homelab, men alle navne og IP-adresser er eksempler.

**Forudsætning:** En kørende Proxmox-server. Se [proxmox-guide](https://github.com/TechNetDK/proxmox-guide).

## Hvorfor en VM og ikke en container?

| | Home Assistant OS (VM) | Home Assistant i Docker |
|---|---|---|
| Apps (tidligere tilføjelser/add-ons) | Ja, med ét klik | Nej |
| Indbygget backup og opdatering | Ja | Delvist |
| USB-enheder (Bluetooth, Zigbee) | Nemt via Proxmox | Mere besvær |
| Officielt anbefalet | Ja | Kun til erfarne |

Jeg bruger derfor **Home Assistant OS i en VM**.

## Det jeg bruger

| Del | Værdi |
|---|---|
| VM-ID | 102 |
| CPU | 2 kerner |
| RAM | 4 GB |
| Disk | ca. 48 GB |
| IP (eksempel) | 10.0.0.14 |

## Indhold

| # | Kapitel |
|---|---|
| 01 | [Installer Home Assistant OS](01-installer-haos.md) |
| 02 | [Første opsætning](02-foerste-opsaetning.md) |
| 03 | [USB-enheder: Bluetooth og Zigbee](03-usb-enheder.md) |
| 04 | [Apps (tilføjelser)](04-tilfoejelser.md) |
| 05 | [Adgang udefra](05-adgang-udefra.md) |
| 06 | [Backup og opdatering](06-backup-og-opdatering.md) |
| 07 | [Fejl jeg har ramt, og løsningerne](07-fejl-og-loesninger.md) |
