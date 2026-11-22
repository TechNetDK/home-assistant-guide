# 02 – Home Assistant i Docker

Alt ligger i én mappe inde i containeren: `/opt/homeassistant`.

## 1. docker-compose.yml
```bash
mkdir -p /opt/homeassistant/config && cd /opt/homeassistant
nano docker-compose.yml
```
```yaml
name: homeassistant

services:
  homeassistant:
    container_name: homeassistant
    image: ghcr.io/home-assistant/home-assistant:stable
    restart: unless-stopped
    network_mode: host
    environment:
      - TZ=Europe/Copenhagen
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
```

| Del | Hvorfor |
|---|---|
| `network_mode: host` | Home Assistant kan selv finde enheder på netværket (fx TV, Chromecast og Hue). |
| `./config:/config` | Al opsætning gemmes i `/opt/homeassistant/config`. |
| `:stable` | Den nyeste stabile version. |

## 2. Start
```bash
docker compose up -d
docker compose logs -f homeassistant    # Ctrl+C for at stoppe visningen
```

## 3. Første opsætning
Åbn `http://10.0.0.13:8123` i browseren, og følg guiden:
- Lav en **admin-bruger** med en stærk adgangskode.
- Vælg hjemmets placering, tidszone (`Europe/Copenhagen`), enhedssystem (metrisk) og valuta (DKK).
- Home Assistant finder selv mange enheder på netværket. Tilføj dem, du vil bruge.

## 4. Lav en bruger til hvert familiemedlem
**Indstillinger → Personer** → **Tilføj person** → slå **Tillad login** til. Lad **Administrator** være slået fra.
