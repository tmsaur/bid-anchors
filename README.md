# BareBud — offentlige bud-ankere

Dette repoet inneholder daglige **rot-hashes** av budloggen til alle
avsluttede auksjoner på [BareBud](https://barebud.no).

## Hva er det?

Hvert bud på BareBud får et digitalt fingeravtrykk (sha256) som er
kryptografisk lenket til forrige bud sin fingeravtrykk. Én gang i døgnet
publiseres en **rot-hash** som oppsummerer alle avsluttede auksjoner den
dagen — her, offentlig på GitHub.

Fordi vi ikke kan endre historikken i dette repoet uten at det synes
(GitHub logger alle commits), fungerer det som et **eksternt anker**:
en bevisføring på at BareBud ikke har skrevet om budhistorikken i
ettertid.

Les mer i [forklaringen for vanlige folk](https://barebud.no/verify).

## Format

Hver dag publiseres en JSON-fil:

```
YYYY-MM-DD.json
```

Innhold:
```json
{
  "date": "YYYY-MM-DD",
  "rootHash": "sha256-hex-av-alle-avsluttede-auksjoner-den-dagen",
  "auctions": [
    {
      "id": "auction-uuid",
      "seedHash": "sha256-hex",
      "finalHash": "sha256-hex",
      "bidCount": 12,
      "endedAt": "ISO-8601"
    }
  ]
}
```

## Verifisering

For å verifisere en auksjon:

1. Gå til `https://barebud.no/verify/<auction-id>`
2. Klikk "Verifiser kjede" — nettleseren regner ut hashene lokalt
3. Sammenlign `finalHash` med det som ligger publisert her

## Status

Publisering starter **automatisk** når BareBud går fra ventliste-modus
til produksjon (Vipps eCom aktivert). Frem til da inneholder repoet
kun denne README-en.

---

Drives av **Capp AS** (org.nr 918 432 973, Steinkjer) —
kontakt: hei@barebud.no
