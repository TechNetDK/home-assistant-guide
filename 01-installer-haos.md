# 01 – Installer Home Assistant OS

Alle kommandoer køres på **Proxmox-værten**.

## 1. Hent billedet
Find den nyeste version på Home Assistants GitHub-side
(`home-assistant/operating-system` → **Releases**), og hent filen `haos_ova-<version>.qcow2.xz`:
```bash
cd /var/lib/vz/template
wget https://github.com/home-assistant/operating-system/releases/download/<version>/haos_ova-<version>.qcow2.xz
xz -d haos_ova-<version>.qcow2.xz
```

## 2. Opret VM'en
```bash
qm create 102 --name homeassistant --ostype l26 \
  --machine q35 --bios ovmf \
  --efidisk0 local-lvm:1,efitype=4m,pre-enrolled-keys=0 \
  --cores 2 --memory 4096 \
  --net0 virtio,bridge=vmbr0 \
  --scsihw virtio-scsi-pci \
  --agent enabled=1 --onboot 1
```

| Valg | Hvorfor |
|---|---|
| `--bios ovmf` + `efidisk0` | Home Assistant OS kræver UEFI. |
| `pre-enrolled-keys=0` | Uden Secure Boot-nøgler – ellers vil HAOS ikke starte. |
| `--agent enabled=1` | Proxmox kan se VM'ens IP og lukke den pænt ned. |
| `--onboot 1` | Starter automatisk, når serveren booter. |

## 3. Importer disken og gør den større
```bash
qm disk import 102 /var/lib/vz/template/haos_ova-<version>.qcow2 local-lvm
qm set 102 --scsi0 local-lvm:vm-102-disk-1 --boot order=scsi0
qm resize 102 scsi0 +16G   # billedet er 32 GB – giv lidt ekstra plads
qm start 102
```
`disk-0` er EFI-disken, så den importerede disk hedder `disk-1`.
Tjek navnet med `qm config 102`, hvis du er i tvivl.

## 4. Find IP-adressen
Åbn **Console** for VM 102 i Proxmox. Efter et par minutter står adressen på skærmen.
Gå derefter til adressen, der står i konsollen, fx `http://<ip>`.
Nye installationer (fra 2026.8) bruger ikke længere `:8123`.

Den første opstart kan tage op til 20 minutter, fordi Home Assistant henter de sidste dele.
