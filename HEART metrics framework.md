---
created: 2025-12-29T13:01
updated: 2025-12-29T13:06
source: https://storage.googleapis.com/gweb-research2023-media/pubtools/pdf/36299.pdf
type: resource
---


# Measuring the User Experience on a Large Scale (Rodden, Hutchinson & Fu, 2010)

Bron: "Measuring the User Experience on a Large Scale: User-Centered Metrics for Web Applications" (CHI 2010). :contentReference[oaicite:0]{index=0}

## Doel van de paper
De paper beschrijft hoe je gebruikerservaring (UX) op grote schaal kunt meten voor webapplicaties met metrics die user-centered zijn. De auteurs introduceren:
1) het HEART-framework (categorieën UX-metrics)
2) het Goals–Signals–Metrics-proces (van doelen naar meetbare dashboard-metrics)

## Probleem met gangbare web analytics
Veelgebruikte metrics zijn vaak business- of systeemgericht en lastig te vertalen naar UX-impact. Voorbeelden:
- Page views kunnen omhoog gaan door populariteit, maar ook door verwarring (meer “zoekkliks” om eruit te komen).
- Seven-day active users telt unieke gebruikers, maar zegt weinig over betrokkenheid of terugkeer (nieuw vs. terugkerend).
- Omzet kan op korte termijn stijgen terwijl UX verslechtert op lange termijn.

## PULSE-metrics
De auteurs noemen veelgebruikte "product health" metrics PULSE:
- Page views
- Uptime
- Latency
- Seven-day active users
- Earnings

Deze zijn belangrijk, maar indirect en soms ambigu als UX-indicator.

## HEART-framework
HEART is een set categorieën om user-centered metrics te definiëren:

### Happiness
Attitudinale metrics (wat gebruikers voelen/denken), zoals:
- tevredenheid
- perceived ease of use
- likelihood to recommend
Meestal gemeten via (periodieke) surveys.

### Engagement
Gedragsmatige betrokkenheid (frequentie/intensiteit/diepte van gebruik), bijv.:
- bezoeken per gebruiker per week
- uploads per gebruiker per dag
Bij voorkeur genormaliseerd (gemiddeld per gebruiker), niet als ruwe totalen.

### Adoption
Instroom: hoeveel nieuwe gebruikers starten met het product/feature, bijv.:
- accounts aangemaakt in de afgelopen 7 dagen
- eerste succesvolle voltooiing van een kernactie

### Retention
Vasthouden: hoeveel gebruikers blijven terugkomen, bijv.:
- % gebruikers uit week X dat na 3 maanden nog actief is
Nuttig om nieuw vs. bestaand gebruik te onderscheiden, vooral bij spikes door events of redesigns.

### Task Success
Succes in kerntaken (traditionele UX-metrics opgeschaald), zoals:
- succesratio/taakvoltooiing
- tijd om een taak te voltooien
- foutpercentage
Kan via remote usability/benchmarking of via logs (als taken/paden detecteerbaar zijn).

## Goals–Signals–Metrics proces
De auteurs stellen een praktische workflow voor om van doelen naar dashboard-metrics te komen:

1. Goals
- Formuleer expliciet de UX-doelen van product/feature.
- Gebruik HEART als checklist om te bepalen welke soorten doelen relevant zijn.

2. Signals
- Bepaal welke gedragingen of attitudes succes/falen aangeven.
- Bepaal databronnen (logs, surveys, eventueel andere bronnen).
- Kies signalen die specifiek en gevoelig zijn voor het doel.

3. Metrics
- Vertaal signalen naar concrete meetwaarden.
- Normaliseer waar nodig (ratio’s, percentages, gemiddelden per gebruiker).
- Let op meetkwaliteit: bots/crawlers, incomplete logging (AJAX/Flash), definities van “actief”.

## Belangrijkste takeaways
- HEART vult PULSE aan: minder ambigu en beter gekoppeld aan UX.
- Metrics moeten gekoppeld zijn aan doelen; anders zijn ze niet actiegericht.
- Trianguleer metrics met andere onderzoeksmethoden; metrics vervangen geen vroeg/fase UX research.
- Grote schaal maakt nieuwe UX-dimensies beter meetbaar (Engagement, Adoption, Retention).

## Conclusie
HEART + Goals–Signals–Metrics biedt een herbruikbaar raamwerk om UX op schaal te meten met zowel attitudinale als gedragsdata en helpt teams om data-gedreven én user-centered beslissingen te nemen.
