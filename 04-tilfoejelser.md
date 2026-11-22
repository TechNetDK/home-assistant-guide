# 04 – Apps (tilføjelser)

Apps (tidligere kaldt tilføjelser eller add-ons) er ekstra programmer, der kører inde i Home Assistant OS.
**Indstillinger → Apps** → **Installer app**.

## Dem jeg bruger

| App | Opgave |
|---|---|
| **File editor** | Ret konfigurationsfiler (fx `configuration.yaml`) i browseren. |
| **Terminal & SSH** | Kommandolinje direkte i Home Assistant. |
| **Mosquitto broker** | MQTT – til enheder, der taler MQTT. |
| **Tailscale** | Sikker adgang, når du er ude (se kapitel 05). |

## Installer en app
1. Klik på appen → **Installer**.
2. Slå **Start ved opstart** og **Vagthund** (watchdog) til.
3. Klik **Start**, og se **Log**, hvis noget ikke virker.

## Ret konfigurationen sikkert
- Tjek altid konfigurationen, før du genstarter:
  **Indstillinger → Værktøjer → YAML → Tjek konfiguration**.
- Lav en backup, før du ændrer noget stort (se kapitel 06).

> **HACS** (Home Assistant Community Store) giver adgang til flere integrationer og kort, men
> er ikke officielt. Installer kun det, du har brug for, og tag backup først.
