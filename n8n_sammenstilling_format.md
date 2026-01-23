# Format for erfaringsbank-output

Denne filen beskriver hvordan nøkkelpunkter skal formateres i output-filene.

## Output-filer

For hver batch med vedtak skal du produsere:

1. **erfaringer.md** – Lesbar dokumentasjon av alle nøkkelpunkter fra batchen
2. **erfaringer.csv** – Maskinlesbar tabell som kan akkumuleres over tid

---

## erfaringer.md

### Filstruktur

```markdown
# Erfaringsbank – [Batch-identifikator/dato]

## Sammendrag

- Antall vedtak analysert: [n]
- Antall nøkkelpunkter identifisert: [n]
- Fordeling: [n] GODKJENT, [n] PROBLEMATISK

---

## Nøkkelpunkter

[Alle nøkkelpunkter i rekkefølge etter ID]
```

### Format per nøkkelpunkt

```markdown
### [ID]: [Kort tittel]

| Metadata | |
|----------|---|
| **Saks-ID** | [Saks-ID] |
| **Hovedkategori** | [Hovedkategori] |
| **Underkategori** | [Underkategori] |
| **Avsnitt** | [Avsnittsnummer] |
| **Kategori** | [GODKJENT/PROBLEMATISK] |

#### Faktum

[Beskrivelse av det faktiske forholdet som ble vurdert]

#### Vurdering

[Nemndas juridiske vurdering og begrunnelse]

#### Lærdom

[Generell lærdom for fremtidige anskaffelser]

---
```

### Eksempel på nøkkelpunkt i erfaringer.md

```markdown
### 2024/2005-1: Krav om brukt/demokjørt maskin

| Metadata | |
|----------|---|
| **Saks-ID** | 2024/2005 |
| **Hovedkategori** | Krav til ytelsen/teknisk spesifikasjon |
| **Underkategori** | Krav til brukt/demokjørt |
| **Avsnitt** | 18-23 |
| **Kategori** | GODKJENT |

#### Faktum

Oppdragsgiver stilte krav i kravspesifikasjonen om at tilbudte maskiner skulle være brukt eller demokjørt med timetall under 2000 driftstimer, og være 2022-modell eller nyere. Klager anførte at kravet var urimelig og avskårte leverandører fra å delta.

#### Vurdering

Nemnda viste til at oppdragsgiver selv definerer behovet og bestemmer hva som skal inngå i anskaffelsen. Kravet var begrunnet i miljøhensyn, økonomi og ønske om kort leveringstid. Nemnda fant at kravet fremstod saklig og objektivt begrunnet, og at det derfor ikke var i strid med anskaffelsesforskriften § 15-1 eller de grunnleggende prinsippene i anskaffelsesloven § 4.

#### Lærdom

Krav i kravspesifikasjonen som begrenser konkurransen kan aksepteres når de er saklig og objektivt begrunnet i legitime formål som miljøhensyn, økonomi eller andre forretningsmessige behov. Oppdragsgiver har vid frihet til å definere sitt eget behov.

---
```

---

## erfaringer.csv

### Kolonner

| Kolonne | Beskrivelse |
|---------|-------------|
| ID | Unik identifikator (Saks-ID + løpenummer) |
| Saks_ID | Saksnummer |
| Hovedkategori | Kategori fra fast liste |
| Underkategori | Organisk utviklet underkategori |
| Avsnitt | Avsnittsnummer i vedtaket |
| Kategori | GODKJENT eller PROBLEMATISK |
| Faktum | Kort beskrivelse (maks 500 tegn) |
| Vurdering | Kort beskrivelse (maks 500 tegn) |
| Laerdom | Kort beskrivelse (maks 500 tegn) |

### Format

- Skilletegn: Semikolon (;)
- Tekstkvalifiserer: Doble anførselstegn (")
- Encoding: UTF-8
- Linjeskift i tekst: Erstattes med ` | ` (mellomrom-pipe-mellomrom)

### Header-rad

```csv
ID;Saks_ID;Hovedkategori;Underkategori;Avsnitt;Kategori;Faktum;Vurdering;Laerdom
```

### Eksempel på rad

```csv
"2024/2005-1";"2024/2005";"Krav til ytelsen/teknisk spesifikasjon";"Krav til brukt/demokjørt";"18-23";"GODKJENT";"Oppdragsgiver stilte krav om brukt eller demokjørt maskin med under 2000 driftstimer. Klager anførte at kravet var urimelig og konkurransebegrensende.";"Nemnda fant at kravet var saklig og objektivt begrunnet i miljøhensyn, økonomi og kort leveringstid. Oppdragsgiver definerer selv sitt behov.";"Konkurransebegrensende krav kan aksepteres når de er saklig begrunnet i legitime formål. Oppdragsgiver har vid frihet til å definere behovet."
```

---

## Regler for CSV-felter

### Forkorting av tekst

Dersom Faktum, Vurdering eller Lærdom overstiger 500 tegn i erfaringer.md, skal de forkortes til maks 500 tegn i CSV-filen. Behold det viktigste innholdet og avslutt med "..." om nødvendig.

### Escaping

- Doble anførselstegn i tekst: Escapes med dobbelt anførselstegn ("")
- Semikolon i tekst: Trenger ikke escapes når feltet er i anførselstegn
- Linjeskift: Erstattes med ` | `

### Eksempel på escaping

Tekst med anførselstegn:
```
Nemnda viste til at kravet om "brukt eller demokjørt" var saklig.
```

Blir i CSV:
```csv
"Nemnda viste til at kravet om ""brukt eller demokjørt"" var saklig."
```

---

## Kvalitetssikring

Før du leverer output, kontroller at:

1. [ ] Alle nøkkelpunkter har unik ID
2. [ ] Hovedkategori er fra den faste listen
3. [ ] Avsnittsnummer er korrekte og kan verifiseres i vedtaket
4. [ ] Kategori er enten GODKJENT eller PROBLEMATISK
5. [ ] Lærdommen er generell nok til å være anvendelig i andre saker
6. [ ] CSV-filen har korrekt antall kolonner per rad
7. [ ] Ingen uescapede spesialtegn i CSV

