# 06 – Backup og opdatering

## 1. Automatisk backup i Home Assistant
**Indstillinger → System → Backups** → **Konfigurer automatiske backups**:
- Hver dag
- Behold fx 7
- Gem **krypteringsnøglen** et sikkert sted (fx din password-manager).

> Uden krypteringsnøglen kan backuppen **ikke** gendannes. Gem den, før du har brug for den.

## 2. Gem backup uden for VM'en
En backup inde i VM'en hjælper ikke, hvis disken dør.
**Indstillinger → System → Lager** → **Tilføj netværkslager** (fx en NAS-mappe),
og vælg det som placering for backups.

## 3. Backup af hele VM'en i Proxmox
Tag VM 102 med i Proxmox' egen backup (se kapitel 07 i Proxmox-guiden).
Så kan hele VM'en gendannes på få minutter.

## 4. Opdatering
1. Læs udgivelsesnoterne for **breaking changes**.
2. Tag et snapshot på Proxmox-værten:
   ```bash
   qm snapshot 102 foer-opdatering
   ```
3. Opdater under **Indstillinger → System → Opdateringer**.
4. Virker alt, så slet snapshottet igen: `qm delsnapshot 102 foer-opdatering`.
   Gik det galt: `qm rollback 102 foer-opdatering`.

Gem ikke snapshots i lang tid – de fylder mere og mere.

## 5. Gendan på en ny installation
Installer Home Assistant OS igen (kapitel 01). Ved første opsætning vælger du
**Gendan fra backup**, uploader filen og indtaster krypteringsnøglen.
