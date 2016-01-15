---
description: na
keywords: na
title: RMS for Individuals and Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
---
# RMS for enkeltpersoner og Azure Rights Management
RMS for enkeltpersoner er en gratis self service-abonnement for brukere i en organisasjon som har blitt sendt sensitive filer som er beskyttet av Microsoft Azure Rights Management (Azure RMS), men de kan ikke godkjennes fordi deres IT-avdelingen ikke behandler en konto for dem i Azure. Hvis du for eksempel ikke IT-avdelingen har Office 365 eller bruke Azure tjenester.

Disse brukerne kan registrere deg for en gratis arbeid eller skole konto for å bruke med Azure RMS, og laste ned og installere rettighetsadministrasjon deling av programmet. Disse brukerne kan derfor nå godkjenne for å bevise at de er personen de beskyttede filene ble sendt til, og deretter lese beskyttede filer på datamaskiner eller mobile enheter.

Ved hjelp av Rights Management er deling av programmer på datamaskiner med Windows, kan disse brukerne også beskytte filer på stedet eller sende beskyttede filer via e-post til personer i eller utenfor organisasjonen. Hvis mottakerne av e-post som de sender i en organisasjon som også ikke administrerer brukerkontoer i Azure, kan de for registrere seg for et RMS for kontoen for enkeltpersoner å lese beskyttet e-postvedlegget.

> [!IMPORTANT]
> Denne gratis abonnement sikrer at autoriserte personer kan alltid lese filer som er beskyttet. For øyeblikket, kan du også bruke dette gratis abonnement til å beskytte dokumenter og opprette nye beskyttede e-postmeldinger, men muligheten for å skrive nye beskyttet innhold er beregnet bare for prøveversjonen og kan bli fjernet i fremtiden. Hvis du vil ha mer informasjon og eventuelle endringer til å bruke RMS for enkeltpersoner for å beskytte innhold, kan du se den [Microsoft Rights Management vilkårene for Bruk](https://portal.aadrm.com/Legal/Service).

Hvis du vil ha mer informasjon om hvordan du kan beskytte filer ved å bruke den gratis Rights Management program for deling, se den [Rights Management deling program guide for brukere](http://technet.microsoft.com/library/dn339006.aspx).

RMS for enkeltpersoner er et eksempel på en selvbetjent registrering som støttes av Azure Active Directory. Hvis du vil ha mer informasjon om hvordan dette fungerer, kan du se [Hva er selvbetjent registreringen av Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/) i dokumentasjonen for Microsoft Azure. Bruk følgende deler for mer informasjon som er spesifikk for RMS for personer:

-   [Hvordan brukerne registrere seg for RMS for enkeltpersoner](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_SignUp)

    -   [Teknisk oversikt](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TechnicalOverview)

-   [Hvordan administratorer kan styre kontoer som er opprettet for RMS for enkeltpersoner](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts)

-   [Hvordan finne ut om brukerne har registrert deg for RMS for enkeltpersoner](#BKMK_Detect)

## <a name="BKMK_SignUp"></a>Hvordan brukerne registrere seg for RMS for enkeltpersoner
For å registrere deg for denne gratis konto, du ber om det. ved å gå til [Microsoft Rights Management side](https://portal.aadrm.com/), og gir arbeidet eller skolen e-postadresse. De vanligste slik at du vil bli dirigert til denne registreringssiden er Hvis du har mottatt en e-postmelding med en beskyttet vedlegg som inneholder instruksjoner for hvordan å registrere deg. Du vil motta en e-post svar fra Microsoft, og deretter fullføre registreringsprosessen ved å skrive inn detaljer for å opprette kontoen. Når du får en postbekreftelse på e-fra Microsoft, sender denne siste e-postmeldingen deg til en side der du kan laste ned programmet deling for forskjellige enheter, og en kobling til brukerhåndboken.

#### Abonnere på RMS for enkeltpersoner

1.  Ved hjelp av en Windows- eller Mac-datamaskin, kan du gå til den [Microsoft Rights Management side](https://portal.aadrm.com).

2.  Skriv inn e-postadressen som du bruker i organisasjonen, for eksempel **janetm@contoso.com** eller **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > Personlige e-postkontoer støttes ikke, så må du ikke angi en Microsoft-konto (tidligere kjent som Microsoft Live ID-konto) eller en annen personlig konto som du kan bruke hjemme fra Internett-leverandøren.

3.  Klikk **Komme i gang**.

    Microsoft bruker e-postadressen din til å kontrollere om organisasjonen allerede har en [betalt abonnement som inkluderer Azure RMS](https://technet.microsoft.com/library/dn655136.aspx). Hvis det er tilfellet, trenger du ikke RMS for enkeltpersoner slik at du må være logget på øyeblikkelig og selvbetjent fortegnet opp for RMS for enkeltpersoner er avbrutt. Hvis et betalt abonnement for Azure RMS ikke blir funnet, vil du fortsette til neste trinn.

4.  Vente på en bekreftelse på e-postmelding blir sendt til adressen du angav. Det vil være fra Microsoft (en DoNotReply@microsoft.com) og har emnet **Microsoft RMS**.

5.  Når du mottar e-postmeldingen, klikker du koblingen i instruksjonene for å fullføre påloggingsprosessen.

6.  Koblingen tar deg en ny **Microsoft Rights Management** -siden for å angi detaljer for kontoen din. Skriv inn fornavn, etternavn, Skriv inn og Bekreft et passord ved hjelp av, velger du landet ditt (eller nærmeste landet til ditt land ikke er oppført) fra rullegardinlisten, og klikk deretter **opprette**.

7.  Vent til en annen e-postmelding fra Microsoft som bekrefter nå at kontoen din er klar til bruk.

8.  Når du mottar e-postmeldingen, klikker du koblingen for å logge på og lese instruksjonene for å laste ned og installere programmet deling, eller klikk Hjelp-koblingen for å lese brukerhåndboken for deling program.

Nå kontoen er opprettet, er du klar til å starte beskyttelse av filer og lese filer andre har beskyttet. Når du blir bedt om å logge deg på å beskytte eller lese beskyttede filer, må du angi e-postadressen og passordet du brukte til å opprette kontoen for RMS for enkeltpersoner.

### <a name="BKMK_TechnicalOverview"></a>Teknisk oversikt
RMS for personer bruker en selvbetjent påloggingsprosessen som også brukes av andre tjenester som bruker Microsoft cloud-basert teknologi til å godkjenne brukere.

Dette er hva som skjer i bakgrunnen når en bruker abonnerer på RMS for enkeltpersoner og organisasjonen ikke har en Office 365-abonnementet eller Azure abonnement, og derfor ingen katalog i Azure til å godkjenne brukere:

1.  Når den første brukeren fra en organisasjon som ber om et abonnement for RMS for enkeltpersoner, kontrolleres domenenavnet som er oppgitt i e-postadressen til å se om det allerede er tilknyttet en Azure leier. Hvis det ikke finnes noen eksisterende leier, opprettes automatisk en ny leier og Azure katalog for organisasjonen, som inneholder en konto for denne første brukeren. I motsetning til er et betalt abonnement for Azure, første kontoen ikke en global administrator, men en standardbruker. Den nye kontoen bruker e-postadresse og passord som brukeren angav.

    > [!NOTE]
    > Noen domenenavn kan ikke brukes til å opprette mappen, og derfor kan ikke brukes for RMS for enkeltpersoner. Denne JavaScript Object Notation-filen du kan vise listen over blokkerte domenenavn: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Hvis det finnes en eksisterende leier, kontrolleres det for å se om det finnes allerede et abonnement for Azure RMS. Når ikke finnes uten abonnement, kan du legge gratis RMS for enkeltpersoner-abonnement.

2.  Organisasjonen er gitt RMS for enkeltpersoner-abonnement. Nå kan kan denne brukeren kan godkjennes av Azure beskytte filer og lese filer andre har beskyttet ved hjelp av Azure Rights Management. Hvis du vil beskytte, og lese beskyttede filer, brukeren må ha en RMS-enlightened program, for eksempel en kostnadsfri [Rights Management deling program](https://technet.microsoft.com/library/dn919648.aspx).

3.  Når den andre brukeren fra den samme organisasjonen ber om en RMS for abonnement for enkeltpersoner, legges en ny brukerkonto til tidligere opprettede Azure katalogen, ved hjelp av organisasjonens RMS for enkeltpersoner-abonnement. Denne andre brukeren kan gjøre alt som den første brukeren kunne utføre (beskytte filer og lese beskyttede filer), men i tillegg disse to brukere kan nå mer enkelt samarbeide sikkert fordi de raskt kan bruke standardmaler til filene som begrenser tilgangen til kontoer i organisasjonens Azure directory.

4.  Etterfølgende brukere fra den samme organisasjonen følger samme mønster, legge til brukerkontoer (når nye brukere registrerer) til organisasjonens Azure katalog. Flere kontoer som er lagt til katalogen, jo flere brukere kan nå samarbeide med kollegaer og partnere, og mer lett å hindre at uautoriserte personer leser sine filer når de ikke skal ha tilgang til dem.

Det er gratis for organisasjonen og ikke noe arbeid som kreves fra IT-avdelingen i denne prosessen. IT-avdelingen kan imidlertid velge å gjøre ett av følgende:

-   **Behandle kontoer og registreringsprosessen**: IT-administratorer kan ta eierskap over den automatisk opprettede mappen og kontoer i Azure. De kan deretter behandle kontoene ved å implementere directory integration-løsninger som synkronisering av passord og enkel pålogging. Eller de kan hindre brukere i å opprette kontoer eller registrere deg for RMS for enkeltpersoner.

    Hvis du vil ha mer informasjon, se delen nedenfor [Hvordan administratorer kan styre kontoer som er opprettet for RMS for enkeltpersoner](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts).

-   **Administrere Rights Management**: IT-administratorer kan konvertere RMS for enkeltpersoner abonnement for organisasjonen til et betalt abonnement som inkluderer Azure Rights Management. Når de gjør dette, beholdes eksisterende Azure katalog og kontoer for sømløs overgang for eksisterende brukere som bruker RMS for enkeltpersoner. Filer som brukere beskyttet tidligere vil fortsatt være beskyttet med de samme policyene og personer at de er gitt tillatelse til å bruke filene vil fortsatt kunne bruke filene på samme måte.

    Når du tar dette kurset for handling, organisasjonen fordelene ved å kunne integrere Rights Management i sin arbeidsflyter, tjenester og datalagre. I tillegg kan du nå behandle Rights Management fordi du har kontroll over organisasjonens leier nøkkel for Azure Rights Management. Nå kan du gjøre følgende:

    -   Konfigurere Exchange og SharePoint for å støtte Azure Rights Management, selv om disse kjører på lokaler. Exchange og SharePoint støttes internt for elektroniske tjenester, og de støttes av en kobling for lokale servere. Hvis du vil ha mer informasjon, se følgende:

        -   Exchange Online og SharePoint Online-inndelinger fra [Office 365: Konfigurasjon for klienter og elektroniske tjenester](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365) i den [Konfigurere programmer for Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) emnet

        -   [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)

    -   Utføre e-discovery firmaet eies av data slik at du kan, hvis nødvendig, dekryptere filer som er beskyttet ved hjelp av Rights Management. Hvis du vil ha mer informasjon, se [Konfigurere Superbrukere for Azure Rights Management og tjenester for oppdagelse eller gjenoppretting av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

    -   Logge all aktivitet for rettighetsadministrasjon som brukes i organisasjonen. Dette er en svært kraftig, fordi ikke bare kan du overvåke hvilke filer som beskyttes og hvem som er Klarer tilgang til de beskyttede filene, men du kan også identifisere potensielt mistenkelige oppførsel fra uautoriserte personer som prøver å få tilgang til beskyttede filer. Hvis du vil ha mer informasjon, se [Logging og analysere Azure Rights Management-forbruk](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

    -   Gi brukere muligheten til å spore og trekke tilbake sine beskyttede dokumenter, hvis disse funksjonene støttes av din [Azure RMS-abonnement](https://technet.microsoft.com/dn858608). Hvis du vil ha mer informasjon, se  [spore og oppheve filene](https://technet.microsoft.com/library/dn986611.aspx) fra den [RMS deling Brukerhåndbok for programmet](https://technet.microsoft.com/library/dn339006.aspx).

    -   Implementere en ta løsningen din egen nøkkel (BYOK) slik at leier nøkkelen for rettighetsadministrasjon Azure er generert på-lokaler i henhold til IT-policyer, og på en sikker måte overført til Microsoft ved hjelp av en Hardware Security Module (HSM). Hvis du vil ha mer informasjon, se [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

## <a name="BKMK_TakeControlofAccounts"></a>Hvordan administratorer kan styre kontoer som er opprettet for RMS for enkeltpersoner
Hvis du ikke vil konvertere organisasjonens RMS for enkeltpersoner abonnementet til et betalt abonnement, kan du bestemme brukerkontoer i Azure mappen som ble opprettet for organisasjonen på følgende måter:

-   Implementere directory integration-løsninger for Azure Active Directory og Active Directory Domain Services-infrastruktur. Du kan synkronisere brukerkontoer og passord slik at brukere får ikke til å opprette nye kontoer hvis du vil bruke Rights Management og din lokale policyer for passord gjelder for nye Azure brukerkontoer. Du kan også synkronisere passord slik at brukerne ikke trenger å huske forskjellige passord for å bruke IRM.

-   Du kan hindre at brukere ønsker å bruke Azure Rights Management med RMS for enkeltpersoner abonnement. Det er liten nytte i å gjøre dette fordi brukere vil enten dele filer uten beskyttelse (som kan sette selskapet i fare), eller bruker en annen fil beskyttelse mekanisme som ikke gir IT-avdeling muligheten til å få tilgang til data i de fleste tilfeller. Imidlertid Hvis du vil hindre at brukere registrerer seg å bruke RMS for enkeltpersoner, gjør du ett av følgende etter at du har tatt eierskap av organisasjonens mappe i Azure:

    -   Hindre at brukere registrerer seg for selvbetjent abonnementer som inneholder RMS for enkeltpersoner.  For øyeblikket, kan du definere dette av tjenesten; innstillingen gjelder for alle Azure abonnementer som bruker self service-prosessen. Hvis du vil gjøre dette, kan du angi det **AllowAdHocSubscriptions** parameter som False med den [Sett MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet fra Windows PowerShell-modulen for Active Directory-Azure. For eksempel: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Hindre brukere i å opprette en ny konto i Azure, noe som betyr at bare brukere som allerede har en konto i Azure kan registrere seg for selvbetjent abonnementer, som inneholder RMS for enkeltpersoner.  Hvis du vil gjøre dette, kan du angi det **AllowEmailVerifiedUsers** parameter som False med den [Sett MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet fra Windows PowerShell-modulen for Active Directory-Azure. For eksempel: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Synkronisere Active Directory Domain Services-infrastruktur med Azure Active Directory. Denne handlingen hindrer at nye kontoer som blir opprettet når brukerne registrere seg for selvbetjent abonnementer som RMS for enkeltpersoner, og du kan slette eller deaktivere kontoer som ble opprettet tidligere i mappen Azure.

Styre brukerkontoer i mappen Azure, eller hindre brukere i å registrere deg for RMS for enkeltpersoner, må du ha et abonnement på Azure og eier mappen. Hvis du ikke allerede har et abonnement på Azure, kan du skaffe et kostnadsfritt. Hvis en katalog ble opprettet automatisk for deg under prosessen med selvbetjening, bli eier av domenet som ble brukt til å opprette den. Hvis du allerede eier en mappe i Azure, men brukerne er angitt et nytt domene som du bruker i organisasjonen, kan du flette domenet i den eksisterende mappen. Hvis du vil ha mer informasjon, se instruksjonene i [Hva er selvbetjent registreringen av Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)

## <a name="BKMK_Detect"></a>Hvordan finne ut om brukerne har registrert deg for RMS for enkeltpersoner
Som administrator, hvordan vet du Hvis brukerne har registrert deg for RMS for enkeltpersoner? Du kan bruke en hvilken som helst eller en kombinasjon av følgende metoder:

-   Spør brukere om hvordan de beskytter høyst konfidensiell filer, spesielt når du samarbeider med andre utenfor organisasjonen.

-   Når du har et abonnement på Azure for organisasjonen, bruker du [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) cmdleten for å se om **RIGHTSMANAGEMENT_ADHOC** returneres som en av abonnementer. Hvis det er, er RMS for enkeltpersoner-abonnement som ble gitt til organisasjonen, med et utvalg av aktive enheter som er tilgjengelige for brukere av selvbetjent registreringsprosessen.

-   Bruk en system management løsning, for eksempel System Center Configuration Manager, lager programvare som er installert og programvaren i bruk. Rettighetsadministrasjon deling av programmer som kjører ved hjelp av den **ipviewer.exe** program, og du kan [laste ned og installere programmet](http://go.microsoft.com/fwlink/?LinkId=303970) gratis å identifisere andre egenskaper om dette programmet du bruker deretter til innholdslisten for programvare.

-   Være oppmerksom på eventuelle filtyper som er opprettet av programmet for Rights Management-deling. Filtypene .pfile og .ppdf er de mest åpenbare eksemplene, men det finnes andre filer som endrer filtypen sine når de opprinnelig er beskyttet av IRM. Hvis du vil ha mer informasjon, se den [støttede filtyper og filtypeangivelser i Filnavn](http://technet.microsoft.com/library/dn339003.aspx) -delen i den [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/dn339003.aspx).

## Se også
[Komme i gang med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

