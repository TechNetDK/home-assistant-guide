# 01 – Opret en LXC-container med Docker

Home Assistant kører i sin **egen LXC-container** med Docker. Så kan den genstartes,
opdateres og tages backup af uden at røre noget andet.

## 1. Opret containeren (på Proxmox-værten)
Jeg bruger ID **102**. Brug et ledigt ID, og hold Proxmox opdateret (9.1 eller nyere).
Har du ikke en Ubuntu-skabelon endnu, så hent den først (se kapitel 03 i [proxmox-guide](https://github.com/TechNetDK/proxmox-guide)). Skriv dens fulde navn i stedet for `ubuntu-<version>-…`.
```bash
pct create 102 local:vztmpl/ubuntu-<version>-standard_<version>_amd64.tar.zst \
  --hostname homeassistant --ostype ubuntu --unprivileged 1 \
  --cores 2 --memory 2048 --swap 1024 --rootfs local-lvm:16 \
  --net0 name=eth0,bridge=vmbr0,ip=10.0.0.14/24,gw=10.0.0.1 \
  --nameserver 1.1.1.1 --features nesting=1,keyctl=1 \
  --onboot 1
pct start 102
```

| Valg | Hvorfor |
|---|---|
| `--unprivileged 1` | Root i containeren er ikke root på værten. |
| `--features nesting=1,keyctl=1` | Kræves, for at Docker kan køre i containeren. |
| Fast IP | Så telefonen og enhederne altid kan finde Home Assistant. |

## 2. Installer Docker (inde i containeren)
```bash
pct enter 102
apt update && apt upgrade -y
apt install -y curl
curl -fsSL https://get.docker.com | sh
docker run --rm hello-world
```
Ser du "Hello from Docker!", er alt klar.
