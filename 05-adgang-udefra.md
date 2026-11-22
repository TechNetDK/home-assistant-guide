# 05 – Adgang udefra

**Åbn ikke porte til Home Assistant i din router.** Brug i stedet **Tailscale** – det er gratis til
privat brug, og der skal ikke åbnes nogen porte.

## 1. Installer Tailscale
1. **Indstillinger → Apps** → **Installer app** → **Tailscale** → **Installer** → **Start**.
2. Åbn appen, og log ind med din Tailscale-konto.
3. Home Assistant dukker nu op i din Tailscale-oversigt med en `100.x.x.x`-adresse.

## 2. Installer Tailscale på telefonen
Hent Tailscale-appen, og log ind med samme konto.
Så kan du åbne `http://<tailscale-ip>` (eller `:8123` på ældre installationer), når du er ude –
også i Home Assistant-appen.

## 3. Home Assistant-appen
I appen: **Indstillinger → Companion-app → Server** → sæt **Ekstern URL** til `http://<tailscale-ip>`
og **Intern URL** til `http://10.0.0.14`, og vælg dit hjemme-Wi-Fi.
Så skifter appen selv mellem hjemme og ude.

## Sikkerhed
- Stærkt password og **to-faktor**: Klik på dit navn → **Sikkerhed** → **Multifaktorgodkendelse**.
- Kun admin-rettigheder til dig selv.
- Hold Home Assistant opdateret (kapitel 06).

> Alternativ: **Home Assistant Cloud** (Nabu Casa) giver nem adgang udefra og støtter projektet,
> men koster et månedligt beløb.
