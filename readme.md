# 123ZZPWebsite intake

Statische intake voor [intake.123zzpwebsite.nl](https://intake.123zzpwebsite.nl).

## Doel

Deze intake is een lage-frictie leadformulier en lichte onboarding. Bezoekers beantwoorden zes korte stappen. De antwoorden ondersteunen een persoonlijk vervolggesprek en vormen later de basis voor geautomatiseerde pakketadviezen of indicatieve offertes.

Er is nog geen automatische pakket- of prijscalculatie geïmplementeerd.

## Stack

- Eén zelfstandig bestand: `index.html`
- Geen build tooling, frameworks of externe JavaScript-dependencies
- Deploy via GitHub → Netlify
- Live domein: `https://intake.123zzpwebsite.nl`

## Netlify Forms

- Formuliernaam: `website-intake` (niet wijzigen)
- Attributen: `method="POST"`, `data-netlify="true"`, `netlify-honeypot="bot-field"`
- Hidden input: `form-name=website-intake`
- Honeypot: `bot-field`
- Verzending via AJAX als `application/x-www-form-urlencoded`

Belangrijk:

- Netlify Form Detection moet ingeschakeld blijven
- E-mailnotificaties worden apart in Netlify geconfigureerd
- Na elke structurele formwijziging altijd een echte testsubmission doen op de live site

## Intake versie

Hidden veld `Intake versie` met waarde `v2`, zodat nieuwe gestructureerde inzendingen te onderscheiden zijn van oudere formulierversies.

## Zes stappen

1. Projecttype
2. Bedrijf
3. Website-omvang
4. Website-functionaliteit
5. Beschikbare materialen
6. Contactgegevens

Voortgang: tekst `Stap X van 6` plus toegankelijke progressbar (`role="progressbar"`). Op stap 6 staat de balk op 100%.

## Ingezonden velden

| Veld | Verplicht | Type | Waarden |
|---|---|---|---|
| `form-name` | ja | hidden | `website-intake` |
| `bot-field` | honeypot | text | leeg laten |
| `Intake versie` | ja | hidden | `v2` |
| `Projecttype` | ja | single choice | `new_website`, `redesign`, `expand`, `unsure` |
| `Huidige website` | optioneel / conditioneel | URL | alleen bij `redesign` of `expand`, alleen als ingevuld |
| `Bedrijfsomschrijving` | ja | textarea | vrije tekst |
| `Doelgroep` | ja | single choice | `consumers`, `businesses`, `both`, `unsure` |
| `Website omvang` | ja | single choice | `one_page`, `three_to_five`, `six_plus`, `advice_needed` |
| `Website functies` | ja | multi select → 1 veld | CSV zonder spaties, zie hieronder |
| `Andere functionaliteit` | optioneel / conditioneel | text | alleen bij functie `other`, alleen als ingevuld |
| `Logo en huisstijl` | ja | single choice | `ready`, `partial`, `missing`, `unsure` |
| `Teksten` | ja | single choice | `ready`, `partial`, `missing`, `unsure` |
| `Foto's` | ja | single choice | `ready`, `partial`, `missing`, `unsure` |
| `Domeinnaam` | ja | single choice | `yes`, `no`, `unsure` |
| `Bedrijfsnaam` | ja | text | vrije tekst |
| `Contactpersoon` | ja | text | vrije tekst |
| `E-mailadres` | ja | email | e-mail |
| `Telefoonnummer` | optioneel | tel | alleen als ingevuld |
| `Gewenste start` | ja | single choice | `asap`, `one_two_months`, `later`, `unsure` |
| `Toelichting` | optioneel | textarea | alleen als ingevuld |
| `Privacy akkoord` | ja | checkbox | `yes` |

### Website functies

Zichtbaar als meervoudige keuze. Ingezonden als één veld `Website functies` met genormaliseerde waarden, komma-gescheiden zonder spaties.

Voorbeeld: `contact_quote,phone_whatsapp,portfolio`

Mogelijke waarden:

- `contact_quote`
- `phone_whatsapp`
- `services`
- `portfolio`
- `booking`
- `ecommerce`
- `information`
- `other`
- `unsure`

`unsure` is exclusief: selecteren wist andere keuzes; een andere keuze wist `unsure`.

## Conditioneel gedrag

- `Huidige website` verschijnt alleen bij projecttype `redesign` of `expand`. Bij wissel naar `new_website` of `unsure` wordt het veld verborgen en geleegd.
- `Andere functionaliteit` verschijnt alleen als `other` is gekozen. Bij deselecteren wordt het veld verborgen en geleegd.
- Optionele velden zonder waarde worden niet meegestuurd.

## Genormaliseerde waarden voor latere automatisering

De genormaliseerde keuzewaarden zijn bewust machineleesbaar gehouden, zodat later pakketadvies of een indicatieve offerte hierop kan aansluiten. Die logica zit nog niet in deze codebase.
