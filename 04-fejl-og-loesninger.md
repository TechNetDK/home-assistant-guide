# 04 – Fejl jeg har ramt, og løsningerne

| Problem | Årsag | Løsning |
|---|---|---|
| Docker vil ikke starte i containeren | Mangler `nesting`/`keyctl` | På værten: `pct set 102 --features nesting=1,keyctl=1` og genstart containeren |
| Port 8123 er optaget | En anden tjeneste i containeren bruger porten | `ss -tlnp` i containeren – flyt den anden tjeneste |
| Kan ikke åbne `:8123` | Home Assistant starter stadig, eller den er stoppet | `docker compose logs homeassistant` – første start tager et par minutter |
| Enheder bliver ikke fundet automatisk | Mangler `network_mode: host` | Tilføj det i compose-filen (kapitel 02) |
| Home Assistant starter ikke efter en ændring | Fejl i `configuration.yaml` | Se loggen og ret filen, rul snapshot tilbage, eller gendan seneste backup. Tjek altid konfigurationen før genstart: **Værktøjer** (tidligere Udviklerværktøjer) → **YAML** → **Tjek konfiguration** |
| Docker fejler med `ip_unprivileged_port_start ... permission denied` | Fejl i ældre Proxmox efter en opdatering af containerd | Opdater Proxmox til 9.1 eller nyere |

## Nyttige kommandoer
```bash
cd /opt/homeassistant                    # altid først
docker compose ps                        # kører den?
docker compose logs -f homeassistant     # se loggen
docker compose restart homeassistant     # genstart
docker exec -it homeassistant bash       # kommandolinje inde i containeren
```
