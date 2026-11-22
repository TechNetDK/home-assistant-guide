# 02 – Første opsætning

## 1. Opret din konto
Åbn adressen fra konsollen (fx `http://<ip>`), og følg guiden:
- Lav en **admin-bruger** med et stærkt password.
- Vælg hjemmets placering, tidszone (`Europe/Copenhagen`), enhedssystem (metrisk) og valuta (DKK).
- Home Assistant finder selv mange enheder på netværket. Tilføj dem, du vil bruge.

## 2. Giv serveren en fast IP
**Indstillinger → System → Netværk** → vælg netkortet → **IPv4: Statisk**:

| Felt | Eksempel |
|---|---|
| IP-adresse | 10.0.0.14/24 |
| Gateway | 10.0.0.1 |
| DNS | 10.0.0.1 |

Alternativ: Lav en fast adresse (DHCP-reservation) til VM'en i din router.

## 3. Opdater
**Indstillinger → System → Opdateringer** → installer alle opdateringer.

## 4. Lav en bruger til hvert familiemedlem
**Indstillinger → Personer** → **Tilføj person** → slå **Tillad login** til. Giv dem ikke admin-rettigheder.
