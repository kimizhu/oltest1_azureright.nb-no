---
description: na
keywords: na
title: Helping Users to Protect Files by Using Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
---
# Hjelpe brukere til &#229; beskytte filer ved hjelp av Azure Rights Management
Etter at du har distribuert og konfigurert Azure Rights Management (Azure RMS) for din organisasjon, kan du få hjelp og veiledning for brukere, administratorer og brukerstøtteavdelingen:

-   **Sluttbruker-informasjon:**

    La brukere vite når og hvordan du beskytter dokumenter og e-postmeldinger som inneholder sensitiv informasjon. Når det er mulig, må du oppgi denne informasjonen for sine eksisterende arbeidsflyter slik at de kan ta forholdsregler for å en allerede kjent prosess i stedet for å introdusere helt nye prosesser. Husk å fortelle dem fordelene (og risikoer) som er spesifikke for virksomheten din, i tillegg til å gi retningslinjer for når de skal beskytte filer og epost. Hvis du har konfigurert [egendefinerte maler](http://technet.microsoft.com/library/dn642472.aspx), gi instruksjoner om hvilke av å velge hvis malen navnet og beskrivelsen ikke er nok for dem å velge riktig.

    > [!TIP]
    > Eksempel videoer for sluttbrukere:
    > 
    > -   [Azure RMS-brukeropplevelsen](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Azure RMS-dokumentet sporing og opphevelse](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Administratorinformasjon:**

    Noen programmer bruker automatisk informasjonsbeskyttelse av ved hjelp av policyer og innstillinger som administratorer konfigurerer. For disse programmene må du kanskje gi instruksjoner for andre administratorer som administrerer disse programmene og tjenestene. Hvis du vil ha mer informasjon, se [Hvordan programmer støtter Azure rettighetsbehandling](../Topic/How_Applications_Support_Azure_Rights_Management.md) og [Konfigurere programmer for Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

-   **Hjelpeinformasjon for skrivebord:**

    En av de mest nyttige verktøyene for brukerstøtteavdelingen er den [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).   Hjelp desk operatorer kan kjøres med alternativet Azure RMS-administratoren, og de kan be brukerne å kjøre den med alternativet Azure RMS-bruker. Dette verktøyet kan ikke bare bidra til å identifisere problemer, men også løse problemer som oppdages, og hvis fortsatt ikke løst, registrere sporingslogger.

    Hvis det finnes lovlige forespørsler har fulle rettigheter for tilgang til beskyttede dokumenter, for eksempel en forespørsel fra den juridiske avdelingen eller prosjektleder når en ansatt har forlatt organisasjonen, kontrollerer brukerstøtteavdelingen har prosesser for å be om dette ved å bruke RMS Azure [super bruker funksjonen](https://technet.microsoft.com/en-us/library/mt147272.aspx).

    Dette er dessuten noen av de vanlige problemene som brukere kan rapportere:

    -   **Logg i Hjelp:**

        Brukere kan bli bedt om påloggingsinformasjon når Azure RMS trenger for å godkjenne en bruker og ikke bruker bufret legitimasjon. Dette blir brukerens arbeid eller skole konto og passord som er knyttet til Office 365 leier eller leier Azure Active Directory. Det vil ikke være en Microsoft-konto (tidligere Microsoft Live ID) eller deres personlige e-postkonto, fordi disse ikke støttes av Azure RMS. Gi brukere og brukerstøtteavdelingen instrukser om hvilken konto som skal brukes når brukerne blir bedt om legitimasjon når de bruker disse programmene med Azure RMS.

    -   **Problemer med å beskytte eller bruker innholdstyper:**

        Kontroller at brukerne har de riktige instruksjonene for programmene de bruker, og bruker programmer og enheter som støttes av Azure RMS. Hvis du vil ha mer informasjon om støttede programmer og enheter, se [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

        Hvis brukere får en feilmelding når du prøver å beskytte eller forbruker innhold, be dem om å kjøre den [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) som bruker RMS Azure.

        Hvis brukere rapporterer at de kan åpne beskyttet innhold, men ikke har rettighetene de trenger, be dem om å kjøre den [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) som bruker RMS Azure og laste ned og vise malene. Dette bekrefter at de har fullført lastet ned malene og hvilke rettigheter malene inneholder. Problemet kan være at brukeren ikke er i riktig gruppe som er konfigurert for malen, eller malen må rekonfigurere for brukeren.

Bruk følgende deler for programspesifikk informasjon til å hjelpe brukere med å beskytte sensitive dokumenter og e-post.

## Ved hjelp av informasjon om beskyttelse med deling Rights Management-programmet
Av RMS (Rights Management) deler av programmet er nødvendig å beskytte og forbruker beskyttet innhold hvis de bruker Office 2010-brukere, men også anbefalt for alle datamaskiner og mobile enheter som støtter Azure RMS.

I tillegg til å gjøre det enklere for brukerne å beskytte viktige dokumenter, kan RMS deling program brukere spore dokumenter som de er beskyttet og oppheve tilgang til dem hvis det er nødvendig.

For instruksjoner for å bruke dette programmet for Windows-datamaskiner, kan du se den [Rights Management deling Brukerhåndbok for programmet](http://technet.microsoft.com/library/dn339006.aspx).

For mobile enheter, kan du se den [Vanlige spørsmål om Microsoft Rights Management program for deling for Mobile plattformer](http://technet.microsoft.com/dn451248).

> [!TIP]
> For et høyt nivå eksempelscenario med skjermbilder, kan du se den [Brukere dele trygt vedlegg med mobile brukere](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Example_SharingApp) delen i den [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emnet.

## Ved hjelp av informasjon om beskyttelse med Office 365, 2016 for Office eller Office-2013
Hvis du bruker Azure RMS og ikke har installert rettighetsadministrasjon deling av programmet, vil ikke brukerne se det **del beskyttet** -knappen på båndet eller **beskytte på stedet** fra File Explorer som gjør det enklere for dem å beskytte filene. Disse brukerne må de følge instruksjonene som er lik disse.

> [!TIP]
> Hvis du vil finne programspesifikk hjelp og instruksjoner for bruk av informasjon om beskyttelse med disse programmene, kan du søke etter **IRM** og application navn og versjon.

#### Du beskytter et dokument i Word 2013

1.  I Microsoft Word, kan du opprette et nytt dokument.

2.  Fra den **Fil** -menyen klikker du **Info**, klikker du **Beskytt dokument**, klikker du **begrense tilgang**, og deretter velger du en mal for å raskt bruke riktige bruksrettigheter, eller velg **begrense tilgang** og velg bruksrettighetene selv.

    > [!NOTE]
    > Hvis dette er første gang du bruker Rights Management, skal du kontakte den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] service og vil bli bedt om påloggingsinformasjon for å konfigurere IRM i Office-klient.

3.  Lagre dokumentet.

Når andre åpner dokumentet, godkjente de først. Hvis de ikke har tillatelse til å åpne dokumentet, åpnes ikke dokumentet. Hvis de er autorisert til å åpne dokumentet, åpnes det med de begrensede bruksrettighetene som ble angitt for denne brukeren. En Bruk høyre for bare tillater for eksempel ikke til å redigere eller lagre dokumentet, selv om det først er overført til en annen plassering. Bruksrettighetene vises øverst i dokumentet ved å bruke et banner for begrensningen. Banneret kan vise tillatelsene som er brukt i dokumentet, eller det kan inneholde en kobling for å vise dem.

#### Beskytte en e-postmelding ved hjelp av Outlook 2013 og Exchange Online

1.  I Outlook, kan du opprette en ny e-postmelding som er adressert til en mottaker i din organisasjon.

2.  Fra den **Alternativer** klikk **tillatelse**, og velg deretter et alternativ. For eksempel: **Ikke videresender**, **&lt; firmanavn &gt; - konfidensiell** eller **&lt; firmanavn &gt; - konfidensiell Vis bare**.

3.  Send meldingen.

På samme måte til å vise et beskyttet dokument, godkjennes når mottakerne mottar i e-postmeldingen de først. Hvis de er autorisert til å vise e-postmeldingen, åpnes med begrensede bruksrettighetene som ble angitt for denne brukeren. Hvis du valgte for eksempel **ikke Videresend**, frem-knappen på båndet er ikke tilgjengelig.

#### Beskytte en e-postmelding ved hjelp av Outlook Web App

1.  I Outlook Web App, kan du opprette en ny e-postmelding som er adressert til en mottaker i din organisasjon.

2.  Klikk  **...**,  klikker du **Angi tillatelse**, og velg deretter et alternativ. For eksempel: **Ikke videresender**, **ikke svar til alle**, **&lt; firmanavn &gt; - konfidensiell** eller **&lt; firmanavn &gt; - konfidensiell Vis bare**.

3.  Send meldingen.

På samme måte til å vise et beskyttet dokument, godkjennes når mottakerne mottar i e-postmeldingen de først. Hvis de er autorisert til å vise e-postmeldingen, åpnes med begrensede bruksrettighetene som ble angitt for denne brukeren. Hvis du valgte for eksempel **gjør ikke svar til alle**,  **Svar til alle** alternativet i meldingsvinduet er ikke tilgjengelig.

## Se også
[Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

