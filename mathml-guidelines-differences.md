# MathML: Forskjeller mellom NLB production og Nordic checklist

Dette dokumentet beskriver hvordan **NLB production**-kravene (202202-mathml-requirements-nlb-production.tex fra mathml-guidelines) avviker fra **Nordic MathML Guidelines Checklist** (mathml-checklist.md). Brukes for å forstå avvik mellom de to valideringene og i rapporten.

Kilder:
- NLB production: [202202-mathml-requirements-nlb-production.tex](https://github.com/nlbdev/mathml-guidelines/blob/main/archive/202202-mathml-requirements-nlb-production.tex)
- Nordic checklist: [mathml-checklist.md](mathml-checklist.md)

---

## Struktur og semantics

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Struktur** | Krever `<math>` med `<semantics>` og inner `<mrow>`; `alttext` (AsciiMath) og `altimg` på `<math>`. | Ingen semantics/alttext/altimg; eksplisitt «No alttext attribute», «No altimg attribute». |
| **Namespace** | Eksempler bruker `m:` prefix (`<m:math>`). | «No m: prefix (deprecated practice)». |

---

## Display

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **display** | Må være eksplisitt `block` eller `inline`; regler for når (søsken inline → inline, alene i blokk → block). | Inline: ingen display-attributt (default er inline); block: `display="block"`. |

---

## Parenteser og fences

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Parenteser** | **Krever** `<mfenced open="(" close=")">` (og tilsvarende for `[]`, `{}`). | **Forbyr** `<mfenced>`; bruk `<mo>` for fences. |
| **Absoluttverdi** | `<mfenced open="\|" close="\|">`. | Ikke spesifisert. |

---

## Usynlige operatorer

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Entiteter** | Numeriske entiteter (&#8289;, &#8290;, &#8291;, &#8292); **obligatorisk** ved multiplikasjon/funksjonsanvendelse. | Hex (&#x2061;, &#x2062;, etc.); «for disambiguation». |
| **Krav** | Eksplisitt krav om å bruke dem der det er relevant. | Tilsvarende konsept, mindre strengt formulert. |

---

## Sammenligningsoperatorer

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **&lt;, &gt;, ≤, ≥** | Numeriske entiteter &#60;, &#62;, &#8804;, &#8805; i `<mo>`. | Ikke nevnt. |

---

## Tusen-separator

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Tusen-separator** | **Ikke** bruk tusen-separator (TTS splitter); én `<mn>164000</mn>`. | **Bruk** tusen-separator i samme `<mn>` med `&nbsp;` (f.eks. `89 000`). |

---

## Desimaler

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Desimal** | Hele desimal i én `<mn>` (f.eks. `<mn>20,0</mn>`). | Samme krav. |

---

## Identifikatorer og tekst

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **mi vs mtext** | `<mi>` for identifikatorer, `<mtext>` for tekst; referanse til text-identifiers.json. | Tilsvarende prinsipp, uten ekstern liste. |
| **Ord** | Ikke dele åpenbare ord i enkeltbokstaver (m, e, a, n); bruk mtext. | «Text split into individual mi instead of mtext» som vanlig feil. |

---

## xml:lang

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Språk** | Krever forfader med `xml:lang`; `<math>` kan ikke ha xml:lang. | Ikke nevnt. |

---

## Navngitte funksjoner

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Struktur** | Nøyaktig tre barn i mrow: `mi` (funksjon), `mo` &#8289;, argument(er); argument som «cos 2x» må wrappes i `mrow`. | Mindre streng struktur. |

---

## Grader

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Grader** | Spesifikk struktur: mrow med mn + &#176;; negativ med indre mrow for minus; gradian med msup. | Ikke detaljert. |

---

## Kjemi, fysikk og kode

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Kjemi** | `class="chemistry"` på `<math>`; kjemi med `<mtext>` for elementer. | Kjemi med `<mi>` for elementer; ingen class. |
| **Fysikk** | `class="physics"` på `<math>`. | Ikke nevnt. |
| **Kode** | `class="code"` for math inne i kodeblokker. | Ikke nevnt. |

---

## Tabeller

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **Math i tabeller** | Math i tabeller skal ha `display="inline"`. | Ikke eksplisitt. |

---

## AsciiMath / alttext

| | NLB production | Nordic checklist |
|---|----------------|------------------|
| **alttext** | alttext skal speile MathML (AsciiMath); kort alttext vs. lang MathML = ugyldig. | Ingen alttext (forbyr alttext). |

---

## Oppsummering

- **NLB production** er tilpasset NLB-produksjon (talebok, TTS, Braille) og krever semantics, alttext/altimg, mfenced, eksplisitt display, strenge regler for funksjoner/grader/identifikatorer, og class for kjemi/fysikk/kode.
- **Nordic checklist** følger nyere MathML-anbefalinger (unngår mfenced og alttext) og har andre valg for tusen-separator og noen strukturkrav.
- Rapporten viser resultat for **begge** valideringene og kan bruke denne filen for å forklare avvik.
