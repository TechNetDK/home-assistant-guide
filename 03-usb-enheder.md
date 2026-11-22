# 03 – USB-enheder: Bluetooth og Zigbee

En USB-dongle til Bluetooth eller Zigbee sættes i Proxmox-serveren og gives videre til VM'en.

## 1. Find enhedens ID (på Proxmox-værten)
```bash
lsusb
```
Eksempel på en linje:
```
Bus 001 Device 004: ID 10c4:ea60 Silicon Labs CP210x UART Bridge
```
ID'et er `10c4:ea60` (producent:produkt).

## 2. Giv den til VM'en
```bash
qm set 102 --usb0 host=10c4:ea60
qm reboot 102
```
Brug ID'et – **ikke** bus-nummeret. Så virker det, selvom du flytter donglen til en anden port.
Har du flere enheder, så brug `--usb1`, `--usb2` osv.

## 3. Bluetooth
Indbygget Bluetooth er normalt også en USB-enhed. Find den med `lsusb`, og giv den til VM'en som ovenfor.
Efter genstart finder Home Assistant den selv:
**Indstillinger → Enheder og tjenester** → **Bluetooth** → **Konfigurer**.

Mange enheder kan derefter tilføjes direkte, fx Bluetooth-pærer og -sensorer.

## 4. Zigbee
**Indstillinger → Enheder og tjenester** → **Tilføj integration** → **Zigbee Home Automation (ZHA)**.
Vælg donglen på listen. Derefter kan du parre Zigbee-enheder, fx pærer, kontakter og sensorer.

> Bluetooth-dongler er ikke altid stabile i en VM. Virker det dårligt, så prøv en anden dongle,
> eller brug en Bluetooth-proxy (fx en ESP32 med ESPHome) tættere på enhederne.
