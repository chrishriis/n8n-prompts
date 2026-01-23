# Format for erfaringsbank-output

Denne filen beskriver hvordan lærdommer skal formateres i output.

## Output-format

Du skal produsere **to deler** i din respons:

1. **Markdown-rapport** — Lesbar dokumentasjon av alle lærdommer fra batchen
2. **JSON-blokk** — Maskinlesbar struktur som kan prosesseres automatisk

---

## Del 1: Markdown-rapport

Skriv en lesbar rapport med følgende struktur:

```markdown
# Erfaringsbank — [dato]

## Sammendrag

- Antall vedtak analysert: [n]
- Antall lærdommer identifisert: [n]

---

## Lærdommer

[Alle lærdommer i rekkefølge]
```

### Format per lærdom

```markdown
### [Saks-ID]: [Kort tittel]

**Hovedtema:** [Hovedtema]
**Undertema:** [Undertema]
**Kilde:** Avsnitt [nummer]

**Faktum:** [Kort beskrivelse av det faktiske forholdet]

**Lærdom:** [Generell lærdom for fremtidige anskaffelser]

---
```

---

## Del 2: JSON-blokk

Etter markdown-rapporten, inkluder **alltid** en JSON-blokk med alle lærdommer. Denne MÅ starte med ` ```json ` og slutte med ` ``` `.

### JSON-struktur

```json
[
  {
    "sak_id": "2024/2005",
    "hovedtema": "Kravspesifikasjon",
    "undertema": "Krav til brukt utstyr",
    "laerdom": "Konkurransebegrensende krav kan aksepteres når de er saklig begrunnet i legitime formål som miljøhensyn eller økonomi.",
    "kilde_avsnitt": "18-23"
  }
]
```

### Feltbeskrivelser

| Felt | Beskrivelse | Eksempel |
|------|-------------|----------|
| `sak_id` | Saksnummer fra vedtaket | `"2024/2005"` |
| `hovedtema` | Hovedkategori fra fast liste (se nedenfor) | `"Kravspesifikasjon"` |
| `undertema` | Mer spesifikk underkategori | `"Krav til brukt utstyr"` |
| `laerdom` | Generell, gjenbrukbar lærdom (maks 500 tegn) | `"Krav som begrenser..."` |
| `kilde_avsnitt` | Avsnittsnummer i vedtaket | `"18-23"` eller `"42"` |

### Hovedtemaer (fast liste)

Bruk én av disse hovedkategoriene:

- Kravspesifikasjon
- Kvalifikasjonskrav
- Tildelingskriterier
- Evaluering
- Avvisning
- Avlysning
- Protokollføring
- Habilitet
- Taushetsplikt
- Rammeavtaler
- Direkte anskaffelse
- Forhandlinger
- Frister
- Kunngjøring
- Annet

---

## Eksempel på komplett output

```markdown
# Erfaringsbank — 2024-01-15

## Sammendrag

- Antall vedtak analysert: 3
- Antall lærdommer identifisert: 4

---

## Lærdommer

### 2024/2005: Krav om brukt maskin godkjent

**Hovedtema:** Kravspesifikasjon
**Undertema:** Krav til brukt utstyr
**Kilde:** Avsnitt 18-23

**Faktum:** Oppdragsgiver krevde brukt/demokjørt maskin med under 2000 timer. Klager mente kravet var konkurransebegrensende.

**Lærdom:** Konkurransebegrensende krav i kravspesifikasjonen kan aksepteres når de er saklig og objektivt begrunnet i legitime formål som miljøhensyn eller økonomi.

---

### 2024/2010: Manglende begrunnelse for avvisning

**Hovedtema:** Avvisning
**Undertema:** Begrunnelsesplikt
**Kilde:** Avsnitt 31-35

**Faktum:** Tilbyder ble avvist uten tilstrekkelig begrunnelse for hvorfor kvalifikasjonskravene ikke var oppfylt.

**Lærdom:** Ved avvisning må oppdragsgiver gi konkret begrunnelse som viser hvilke krav som ikke er oppfylt og hvorfor.

---
```

```json
[
  {
    "sak_id": "2024/2005",
    "hovedtema": "Kravspesifikasjon",
    "undertema": "Krav til brukt utstyr",
    "laerdom": "Konkurransebegrensende krav i kravspesifikasjonen kan aksepteres når de er saklig og objektivt begrunnet i legitime formål som miljøhensyn eller økonomi.",
    "kilde_avsnitt": "18-23"
  },
  {
    "sak_id": "2024/2010",
    "hovedtema": "Avvisning",
    "undertema": "Begrunnelsesplikt",
    "laerdom": "Ved avvisning må oppdragsgiver gi konkret begrunnelse som viser hvilke krav som ikke er oppfylt og hvorfor.",
    "kilde_avsnitt": "31-35"
  }
]
```

---

## Kvalitetssikring

Før du leverer output, kontroller at:

1. [ ] Markdown-rapporten er lesbar og velstrukturert
2. [ ] JSON-blokken starter med ` ```json ` og slutter med ` ``` `
3. [ ] JSON er gyldig (kan parses)
4. [ ] Alle lærdommer har alle fem påkrevde felter
5. [ ] `hovedtema` er fra den faste listen
6. [ ] `laerdom` er generell nok til å være anvendelig i andre saker (maks 500 tegn)
7. [ ] `kilde_avsnitt` kan verifiseres i vedtaket
8. [ ] Antall lærdommer i JSON matcher antall i markdown-rapporten

## VIKTIG

JSON-blokken er **obligatorisk** og må alltid inkluderes, selv om du bare finner én lærdom. Uten JSON-blokken kan ikke systemet prosessere lærdommene automatisk.
