# 07 – Fejl jeg har ramt, og løsningerne

| Problem | Årsag | Løsning |
|---|---|---|
| VM'en starter ikke, og konsollen viser "Access Denied" eller UEFI-skærm | Secure Boot-nøgler er slået til | Opret EFI-disken med `pre-enrolled-keys=0`, eller slå Secure Boot fra i VM'ens UEFI-menu (tryk Esc ved opstart) |
| VM'en starter fra den forkerte disk | Boot-rækkefølgen er forkert | `qm set 102 --boot order=scsi0` |
| Kan ikke åbne Home Assistant i browseren | Første opstart er ikke færdig, eller forkert adresse | Vent 10–20 min., og brug adressen i VM'ens konsol (nye installationer: uden `:8123`) |
| USB-donglen virker ikke efter genstart | Donglen er sat på via bus-nummer | Brug ID'et: `qm set 102 --usb0 host=<producent:produkt>` |
| Home Assistant starter ikke efter en ændring | Fejl i `configuration.yaml` | Ret filen i File editor, eller rul snapshot tilbage. Tjek altid konfigurationen før genstart |
| Disken er fuld | Mange gamle backups eller databasen er vokset | Slet gamle backups, og gør disken større: `qm resize 102 scsi0 +16G` |
| Proxmox viser ikke VM'ens IP | QEMU Guest Agent er slået fra | `qm set 102 --agent enabled=1` og genstart VM'en |

## Nyttige kommandoer
På Proxmox-værten:
```bash
qm list                 # alle VM'er
qm config 102           # VM'ens opsætning
qm terminal 102         # konsol (kræver serial port), ellers brug Console i webgrænsefladen
```
I Home Assistants terminal (appen **Terminal & SSH**):
```bash
ha core check           # tjek konfigurationen
ha core restart         # genstart Home Assistant
ha core logs            # se loggen
```
