---
description: na
keywords: na
title: Configuring Usage Rights for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
---
# Konfigurere bruksrettigheter for Azure Rights Management
Når du angir beskyttelse på filer eller e-post ved hjelp av Azure Rights Management (Azure RMS), og du ikke bruker en mal, må du konfigurere bruksrettighetene selv. Når du konfigurerer egendefinerte maler for Azure RMS, velger du i tillegg bruksrettigheter som deretter brukes automatisk når malen er valgt av brukere, administratorer, eller konfigurert tjenester. For eksempel i Azure portal kan du velge roller som konfigurerer en logisk gruppering av bruksrettigheter, eller du kan konfigurere individuelle rettigheter.

Bruke dette emnet til å hjelpe deg med å konfigurere bruksrettigheter du vil bruke for programmet du bruker, og forstå hvordan disse rettighetene tolkes av programmer.

## Bruksrettigheter og beskrivelser
Følgende tabell viser og beskriver bruksrettigheter som støtter rettighetsbehandling, og hvordan de brukes og tolkes. I denne tabellen, den **vanlig navn** er vanligvis hvor du kan se Bruk høyre vises eller referert til som en mer brukervennlig versjon av ettordsverdi som brukes i koden (den **koding i policyen** verdi). Den **API konstant eller verdien** er navnet på SDK for et MSIPC API-kall, brukes når du skriver et RMS-enlightened program som ser etter en Bruk høyre, eller legger til en høyre mot en policy.

|Fellesnavn|Koding i policy|Beskrivelse|Implementering i egendefinerte Office-rettigheter|Navn i Azure portal|Navn i AD RMS-maler|API-konstant eller verdi|Tilleggsinformasjon|
|--------------|-------------------|---------------|-----------------------------------------------------|-----------------------|-----------------------|----------------------------|-----------------------|
|Rediger innhold, Rediger|DOCEDIT|Lar brukeren endre, ordne, formatere eller filtrere innholdet i programmet. Den gir ikke rett til å lagre den redigerte versjonen.|Som en del av den **endre** og **Full kontroll** alternativer.|**Rediger innhold**|**Rediger**|Ikke tilgjengelig|Denne rettigheten kan også brukeren å lagre dokumentet i Office-programmer.|
|Lagre|REDIGER|Tillater brukeren å lagre dokumentet i gjeldende plassering.|Som en del av den **endre** og **Full kontroll** alternativer.|**Lagre fil**|**Lagre**|IPC_GENERIC_WRITEL "REDIGER"|Denne rettigheten kan også brukeren å endre dokumentet i Office-programmer.|
|Kommentar|KOMMENTAR|Aktiverer alternativet for å legge til merknader eller merknader i innholdet.|Ikke implementert|Ikke implementert|Ikke implementert|IPC_GENERIC_COMMENTL "KOMMENTAR"|Denne rettigheten er tilgjengelig i SDK er tilgjengelig som en ad hoc-policy i RMS-beskyttelse-modul for Windows PowerShell og er implementert i noen programmer for leverandøren. Men det er ikke særlig utbredt, og støttes ikke av Office-programmer.|
|Lagre som, eksport|EKSPORTER|Aktiverer alternativet for å lagre innholdet på et annet filnavn (Lagre som). Avhengig av applikasjonen, kan filen lagres uten beskyttelse.|Som en del av den **endre** og **Full kontroll** alternativer.|**Eksportere innhold (Lagre som)**|**Eksportere (Lagre som)**|IPC_GENERIC_EXPORTL "EKSPORT"|Denne rettigheten kan også til å utføre andre eksportalternativer i programmer, for eksempel **Send til OneNote**.|
|Fremover|FREMOVER|Aktiverer alternativet å videresende en e-postmelding og legge til mottakere i **til** og **kopi** linjer.|Nektet ved hjelp av den **ikke Videresend** standard policy.|**Fremover**|**Fremover**|IPC_EMAIL_FORWARDL "FREMOVER"|Tillater videresending til å gi rettigheter til andre brukere som en del av Videresend-handlingen.|
|Full kontroll|EIER|Gir alle rettigheter til dokumentet og alle tilgjengelige handlinger kan utføres.|Som den **Full kontroll** egendefinerte alternativet.|**Full kontroll**|**Full kontroll**|IPC_GENERIC_ALLL "EIER"|Inkluderer muligheten til å fjerne beskyttelsen.|
|Skriv ut|SKRIV UT|Aktiverer alternativer for utskrift av innhold.|Som den **Skriv ut innhold** alternativ i egendefinerte tillatelser. Ikke en per mottaker-innstilling.|**Skriv ut**|**Skriv ut**|IPC_GENERIC_PRINTL SKRIV UT"|Ingen tilleggsinformasjon|
|Svar|SVAR|Aktiverer alternativet svar i e-postklient, uten å tillate endringer i den **til** eller **kopi** linjer.|Ikke tilgjengelig|**Svar**|**Svar**|IPC_EMAIL_REPLY|Ingen tilleggsinformasjon|
|Svar til alle|REPLYALL|Gjør det mulig for **Svar til alle** alternativ i e-postklient, men ikke la brukeren legge til mottakere som skal til **til** eller **kopi** linjer.|Ikke tilgjengelig|**Svar til alle**|**Svar til alle**|IPC_EMAIL_REPLYALLL "REPLYALL"|Ingen tilleggsinformasjon|
|Vis åpne, Les|VIS|Lar brukeren til å åpne dokumentet og vise innholdet.|Som den **lese** egendefinert policy, **Vis** alternativet.|**Vis innhold**|**Vis**|IPC_GENERIC_READL "VIS"|Ingen tilleggsinformasjon|
|Kopier|TREKK UT|Aktiverer alternativene for å kopiere data fra dokumentet til den samme eller et annet dokument.|Som den **Tillat brukere med lesetilgang å kopiere innhold** alternativet egendefinert policy.|**Kopier og Trekk ut innhold**|**Trekk ut**|IPC_GENERIC_EXTRACTL "EXTRACT"|I noen programmer kan også hele dokumentet lagres ubeskyttet.|
|Visningsrettigheter|VIEWRIGHTSDATA|Lar brukeren se policyen som er brukt i dokumentet.|Ikke implementert|**Vis tilordnet rettigheter**|**Visningsrettigheter**|IPC_READ_RIGHTSL "VIEWRIGHTSDATA"|Ignorert av noen programmer.|
|Endre rettigheter|EDITRIGHTSDATA|Tillater brukeren å endre policyen som er brukt i dokumentet. Inkluderer blant annet fjerne beskyttelsen.|Ikke implementert|**Endre rettigheter**|**Rediger rettigheter**|IPC_WRITE_RIGHTSL "EDITRIGHTSDATA"|Ingen tilleggsinformasjon|
|Tillater at makroer|OBJMODEL|Gir mulighet til å kjøre makroer eller utføre andre programmatisk eller ekstern tilgang til innholdet i et dokument.|Som den **Tillat programmatisk tilgang** alternativet egendefinert policy. Ikke en per mottaker-innstilling.|**Tillater at makroer**|**Tillater at makroer**|Ikke tilgjengelig|Ingen tilleggsinformasjon|

## Rettighetene som er inkludert i tillatelsesnivåene
Noen programmer gruppere bruksrettigheter til tillatelsesnivåer for å gjøre det enklere å velge bruksrettigheter som vanligvis brukes sammen. Disse permisisons hjelper til abstrakt et nivå av kompleksitet fra brukere, slik at de kan velge alternativer som er rollebasert.  For eksempel **redaktør** og **medforfatter**. Selv om disse alternativene vises ofte brukere et sammendrag av rettighetene, kan de ikke ta hver rettighet som er oppført i tabellen ovenfor.

Bruk tabellen nedenfor for en oversikt over disse tillatelsesnivåene og en fullstendig liste over rettighetene de inneholder.

|Tillatelsesnivået|Programmer|Rettighetene som er inkludert (felles navn)|
|---------------------|--------------|-----------------------------------------------|
|Viewer|Azure portal<br /><br />Rettighetsadministrasjon deling av programmer for Windows|Vis åpne, Les<br /><br />Svar<br /><br />Svar til alle|
|Redaktør|Azure portal<br /><br />Rettighetsadministrasjon deling av programmer for Windows|Vis åpne, Les<br /><br />Lagre<br /><br />Rediger innhold, Rediger<br /><br />Reply<sup>*</sup><br /><br />Svar til alle<sup>*</sup><br /><br />Fremover<sup>*</sup>|
|Medforfatter|Azure portal<br /><br />Rettighetsadministrasjon deling av programmer for Windows|Vis åpne, Les<br /><br />Lagre<br /><br />Rediger innhold, Rediger<br /><br />Kopier<br /><br />Visningsrettigheter<br /><br />Endre rettigheter<br /><br />Tillater at makroer<br /><br />Lagre som, eksport<br /><br />Skriv ut<br /><br />Reply<sup>*</sup><br /><br />Svar til alle<sup>*</sup><br /><br />Fremover<sup>*</sup>|
|Medeier|Azure portal<br /><br />Rettighetsadministrasjon deling av programmer for Windows|Vis åpne, Les<br /><br />Lagre<br /><br />Rediger innhold, Rediger<br /><br />Kopier<br /><br />Visningsrettigheter<br /><br />Endre rettigheter<br /><br />Tillater at makroer<br /><br />Lagre som, eksport<br /><br />Skriv ut<br /><br />Reply<sup>*</sup><br /><br />Svar til alle<sup>*</sup><br /><br />Fremover<sup>*</sup><br /><br />Full kontroll|
<sup>*</sup> Gjelder ikke for rettighetsadministrasjon deling av programmer for Windows

## Rettighetene som er inkludert i standardmaler
Rettighetene som er inkludert i standardmaler er som følger:

|Visningsnavn|Rettighetene som er inkludert (felles navn)|
|----------------|-----------------------------------------------|
|&lt; navn &gt; organisasjon - bare konfidensiell|Vis åpne, Les|
|&lt; navn &gt; organisasjon - konfidensiell|Vis åpne, Les<br /><br />Lagre<br /><br />Rediger innhold, Rediger<br /><br />Visningsrettigheter<br /><br />Tillater at makroer<br /><br />Fremover<br /><br />Svar<br /><br />Svar til alle|

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

