# 01 – Brug medieserverens container

Jeg kører Home Assistant i **samme LXC-container som medieserveren** (CT 101), fordi Docker
allerede kører der. Så bruger det kun lidt ekstra RAM og CPU.

## 1. Har du ikke containeren endnu?
Følg kapitel 01 i [medieserver-guide](https://github.com/TechNetDK/medieserver-guide).
Den laver CT 101 med Docker (eksempel-IP 10.0.0.13).

## 2. Giv containeren lidt mere RAM (på Proxmox-værten)
Medieserver-guiden giver containeren 4096 MB. Home Assistant bruger ca. 1 GB ekstra:
```bash
pct set 101 --memory 5120
```

## 3. Gå ind i containeren
```bash
pct enter 101
docker --version
```
Home Assistant får sin **egen mappe og compose-fil** (`/opt/homeassistant`), adskilt fra
medieserveren (`/opt/medieserver`). Så kan de opdateres og genstartes hver for sig.
