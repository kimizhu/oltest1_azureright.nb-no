---
description: na
keywords: na
title: Operations for Your Azure Rights Management Tenant Key
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
---
# Operasjoner leietakeradministrasjon n&#248;kkelen Azure Rights Management
Avhengig av leier viktige topologien (administreres av Microsoft eller kunde-administrert) har du ulike nivåer av kontroll og ansvar for Microsoft Azure Rights Management (Azure RMS) leier-tasten etter at den er implementert.

Dette kalles ofte for å bringe din egen nøkkel (BYOK) som når du administrerer din egen leier nøkkel. Hvis du vil ha mer informasjon om dette scenariet, og hvordan du kan velge mellom de to leier viktige topologi, se [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

Tabellen nedenfor viser hvilke operasjoner som du kan gjøre, avhengig av topologi som du har valgt for Azure RMS leier-tasten.

|Lifecycle operasjon|Microsoft-administrerte (standard)|Kunde-administrerte (BYOK)|
|-----------------------|--------------------------------------|------------------------------|
|Oppheve leier-nøkkel|Ingen (automatisk)|Ingen (automatisk)|
|Nye nøkler leier-nøkkel|Ja|Ja|
|Sikkerhetskopiere og gjenopprette leier-nøkkel|Nei|Ja|
|Leier-nøkkelen for dataeksport|Ja|Nei|
|Svare på et brudd|Ja|Ja|
Når du har identifisert hvilke topologien du har implementert, kan du bruke en av følgende deler for mer informasjon om disse operasjonene for Azure RMS leier-tasten.

## <a name="BKMK_MSManagedOperations"></a>Styrt av Microsoft: Leier viktige levetid drift
Hvis Microsoft behandler leier nøkkelen for Azure Rights Management (standard), kan du bruke følgende deler for mer informasjon om kundestøttesyklus operasjonene som er relevante for denne topologien:

-   [Oppheve leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRevoke)

-   [Nye nøkler leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey)

-   [Sikkerhetskopiere og gjenopprette leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBackup)

-   [Leier-nøkkelen for dataeksport](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSExport)

-   [Svare på et brudd](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBreach)

### <a name="BKMK_MSRevoke"></a>Oppheve leier-nøkkel
Når du stoppe abonnementet på Azure RMS, Azure RMS stopper ved hjelp av nøkkelen leier og ingen handling er nødvendig fra deg.

### <a name="BKMK_MSRekey"></a>Nye nøkler leier-nøkkel
Ny inntasting av er også kjent som ruller inn nøkkelen. Ikke nye nøkler leier-nøkkel med mindre det er helt nødvendig. Eldre klienter, for eksempel Office 2010 er ikke laget for å håndtere endringer elegant. I dette scenariet må du fjerne RMS-tilstand på datamaskiner ved hjelp av gruppepolicy eller en tilsvarende mekanisme. Det er imidlertid enkelte legitime hendelser som kan tvinge deg til å taste leier-nøkkelen på nytt. For eksempel:

-   Firmaet ditt er delt inn i to eller flere firmaer. Når nye nøkler du leier-tasten, får ikke tilgang til nytt innhold som publiserer ansatte i det nye firmaet. De får tilgang til det gamle innholdet hvis de har en kopi av den gamle leier-nøkkelen.

-   Du tror hovedkopien av leier nøkkelen (kopi i din besittelse) ble skadet.

Du kan tasten leier-nøkkelen på nytt ved å kalle Microsofts kundestøttetjeneste (CSS) og bevise at du er administrator for leieradministrasjon.

Når nye nøkler du leier-nøkkelen, er nye innholdet beskyttet ved hjelp av den nye nøkkelen for leietakeradministrasjon. Dette skjer på en tretrinns måte, slik at for en bestemt tidsperiode, noe nytt innhold vil fortsette å være beskyttet med nøkkelen gamle leier. Tidligere forblir beskyttet innhold beskyttet til den gamle for leietakeradministrasjon. Hvis du vil støtte dette scenarioet, beholder Azure RMS gamle leier nøkkelen slik at den kan utstede lisenser for gammelt innhold.

### <a name="BKMK_MSBackup"></a>Sikkerhetskopiere og gjenopprette leier-nøkkel
Microsoft er ansvarlig for å sikkerhetskopiere leier-nøkkelen, og det kreves ingen handling fra deg.

### <a name="BKMK_MSExport"></a>Leier-nøkkelen for dataeksport
Du kan eksportere Azure RMS-konfigurasjonen og leier nøkkelen ved å følge instruksjonene i tre trinn:

##### Trinn 1: Starte eksport

-   Hvis du vil gjøre dette, kan du kontakte Microsofts kundestøttetjeneste Service (CSS). Du må bevise at du er administrator for Azure RMS-leier.

##### Trinn 2: Vente på bekreftelse

-   Microsoft bekrefter at din forespørsel om å frigi RMS leier nøkkelen er ekte. Denne prosessen kan ta opptil 3 uker.

##### Trinn 3: Motta viktige instruksjoner fra CSS

-   Microsofts kundestøttetjeneste (CSS) sender deg Azure RMS-konfigurasjonen og leier nøkkelen som krypterte i en passordbeskyttet fil som har filtypen .tpd. Hvis du vil gjøre dette, sender CSS først deg (som personen som startet eksport) et verktøy på e-post. Du må kjøre verktøyet fra en ledetekst som følger:

    ```
    AadrmTpd.exe -createkey
    ```
    Dette genererer et RSA-nøkkelpar og lagrer de offentlige og private halvdeler som filer i gjeldende mappe. For eksempel: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** og **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Svare på e-postmeldingen fra CSS, legge ved fil som har et navn som starter med **PublicKey**. CSS neste sender deg en TPD-fil som en XML-fil som er kryptert med RSA-nøkkel. Kopier denne filen til samme mappe som du opprinnelig kjørte verktøyet AadrmTpd og kjøre verktøyet på nytt, ved hjelp av filen som starter med **PrivateKey** og fra CSS-filen. For eksempel:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    Utdataene fra denne kommandoen skal være to filer: En inneholder passord i ren tekst for den passordbeskyttede TPD, og den andre er passordbeskyttet TPD seg selv. For å kunne kryssreferere formål, må begge ha samme GUID som fellesnøkler og private nøkler filene fra da du kjørte AadrmTpd.exe createkey - kommandoen:

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    Ta sikkerhetskopi av filene, og lagre dem trygt for å sikre at du kan fortsette å dekryptere innhold som er beskyttet med denne nøkkelen for leietakeradministrasjon. I tillegg, hvis du overfører til AD RMS, du kan importere TPD filen (filen som starter med **ExportedTDP**) til AD RMS-serveren.

##### Trinn 4: Kontinuerlig: Beskytte leier-nøkkel

-   Når du mottar leier-nøkkelen, holde det godt vernet, fordi Hvis noen får tilgang til den, de kan dekryptere alle dokumenter som er beskyttet ved hjelp av nøkkelen.

    Hvis årsaken til å eksportere nøkkelen leier er fordi du ikke lenger vil bruke Azure RMS som beste praksis, deaktiverer du nå RMS-leier. Forsinke ikke å gjøre dette etter at du får leier nøkkelen fordi denne forholdsregelen bidrar til å minimere konsekvensene Hvis leier nøkkelen brukes av noen som ikke skal ha den. For instruksjoner, se [Dekommisjonering og deaktivere Azure Rights Management](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

### <a name="BKMK_MSBreach"></a>Svare på et brudd
Ingen sikkerhetssystem, uansett hvor sterkt er fullstendig uten en brudd svar prosess. Leier nøkkelen kan bli videresendt eller stjålet. Selv om det er godt beskyttet godt, kan sikkerhetsproblemene finnes i gjeldende generasjon HSM-teknologi eller gjeldende nøkler og algoritmer.

Microsoft har et dedikert team til å svare på sikkerhetshendelser i sine produkter og tjenester. Så snart det er troverdige rapporter av en hendelse, engasjerer dette teamet til å undersøke omfanget, årsaken og begrensninger. Hvis denne hendelsen gjelder for dine aktiva, vil deretter Microsoft varsle din Azure RMS-Leieradministratorer via e-post ved å bruke adressen du oppgir når du abonnerer på.

Hvis du har et brudd, avhenger beste handlingen som du eller Microsoft kan utføre av omfanget av mislighold; Microsoft vil samarbeide med deg gjennom denne prosessen. Tabellen nedenfor viser noen vanlige situasjoner og sannsynlige svaret, selv om det nøyaktige svaret avhenger av all informasjon som vises under undersøkelsen.

|Hendelse beskrivelse|Sannsynlig svar|
|------------------------|-------------------|
|Leier-nøkkelen er lekket.|-Tasten leier-nøkkelen på nytt. Se den [Nye nøkler leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey) delen i dette emnet.|
|En uautorisert person eller skadelig programvare har rettigheter til å bruke leier-nøkkelen, men selve nøkkelen lekker ikke.|Ny inntasting leier nøkkelen ikke hjelper her, og krever analyse av opprinnelig årsak. Hvis en prosess- eller feil var ansvarlig for uautorisert person til å få tilgang, kan denne situasjonen må løses.|
|Sikkerhetsproblemet som ble oppdaget i RSA-algoritmen, eller nøkkellengde eller brute force angrep blir beregningsmessig gjennomførbar.|Microsoft må oppdatere Azure RMS for å støtte nye algoritmer og lengre nøkler som er fleksibel og be alle kunder til å fornye sine leier nøkler.|

## <a name="BKMK_BYOKManagedOperations"></a>Administrert av kunden: Leier viktige levetid drift
Hvis du administrerer leier nøkkelen for Azure Rights Management (ta din egen nøkkel eller BYOK, scenario), Bruk følgende deler for mer informasjon om kundestøttesyklus operasjonene som er relevante for denne topologien:

-   [Oppheve leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRevoke)

-   [Nye nøkler leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey)

-   [Sikkerhetskopiere og gjenopprette leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBackup)

-   [Leier-nøkkelen for dataeksport](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKExport)

-   [Svare på et brudd](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBreach)

### <a name="BKMK_BYOKRevoke"></a>Oppheve leier-nøkkel
Når du stoppe abonnementet på Azure RMS, Azure RMS stopper ved hjelp av nøkkelen leier og ingen handling er nødvendig fra deg.

### <a name="BKMK_BYOKRekey"></a>Nye nøkler leier-nøkkel
Ny inntasting av er også kjent som ruller inn nøkkelen. Ikke nye nøkler leier-nøkkel med mindre det er helt nødvendig. Eldre klienter, for eksempel Office 2010 er ikke laget for å håndtere endringer elegant. I dette scenariet må du fjerne RMS-tilstand på datamaskiner ved hjelp av gruppepolicy eller en tilsvarende mekanisme. Det er imidlertid enkelte legitime hendelser som kan tvinge deg til å taste leier-nøkkelen på nytt. For eksempel:

-   Firmaet ditt er delt inn i to eller flere firmaer. Når nye nøkler du leier-tasten, får ikke tilgang til nytt innhold som publiserer ansatte i det nye firmaet. De får tilgang til det gamle innholdet hvis de har en kopi av den gamle leier-nøkkelen.

-   Du tror hovedkopien av leier nøkkelen (kopi i din besittelse) ble skadet.

Når nye nøkler du leier-nøkkelen, er nye innholdet beskyttet ved hjelp av den nye nøkkelen for leietakeradministrasjon. Dette skjer på en tretrinns måte, slik at for en bestemt tidsperiode, noe nytt innhold vil fortsette å være beskyttet med nøkkelen gamle leier. Tidligere forblir beskyttet innhold beskyttet til den gamle for leietakeradministrasjon. Hvis du vil støtte dette scenarioet, beholder Azure RMS gamle leier nøkkelen slik at den kan utstede lisenser for gammelt innhold.

Generere til nøkkelen leier-nøkkelen på nytt, og opprette en ny nøkkel via Internett eller personlig, ved å følge fremgangsmåten i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen fra den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emnet.

### <a name="BKMK_BYOKBackup"></a>Sikkerhetskopiere og gjenopprette leier-nøkkel
Du er ansvarlig for sikkerhetskopiering av leier-tasten. Hvis du genererte leier-nøkkelen i en Thales HSM, hvis du vil sikkerhetskopiere nøkkelen bare sikkerhetskopiere Tokenized nøkkel-fil, filen verden og administratoren kort.

Hvis du har overført nøkkelen ved å følge fremgangsmåtene i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen fra den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emnet, Azure RMS vedvarer Tokenized nøkkel filen, beskytter mot feil i noen Azure RMS-noder. Imidlertid ikke anser dette som en fullstendig sikkerhetskopi. For eksempel hvis du trenger en ren tekst-kopi av nøkkelen til å bruke utenfor en Thales HSM vil Azure RMS ikke kunne hente den for deg, fordi den bare har en ikke-reverserbar kopi.

### <a name="BKMK_BYOKExport"></a>Leier-nøkkelen for dataeksport
Hvis du bruker BYOK, kan du eksportere nøkkelen leier fra Azure RMS. Kopien i Azure RMS er ikke-gjenopprettelige. Hvis du vil slette denne nøkkelen slik at den ikke lenger kan brukes, kan du kontakte Microsofts kundestøttetjeneste Service (CSS).

### <a name="BKMK_BYOKBreach"></a>Svare på et brudd
Ingen sikkerhetssystem, uansett hvor sterkt er fullstendig uten en brudd svar prosess. Leier nøkkelen kan bli videresendt eller stjålet. Selv om det er godt beskyttet godt, kan sikkerhetsproblemene finnes i gjeldende generasjon HSM-teknologi eller gjeldende nøkler og algoritmer.

Microsoft har et dedikert team til å svare på sikkerhetshendelser i sine produkter og tjenester. Så snart det er troverdige rapporter av en hendelse, engasjerer dette teamet til å undersøke omfanget, årsaken og begrensninger. Hvis denne hendelsen gjelder for dine aktiva, vil deretter Microsoft varsle din Azure RMS-Leieradministratorer via e-post ved å bruke adressen du oppgir når du abonnerer på.

Hvis du har et brudd, avhenger beste handlingen som du eller Microsoft kan utføre av omfanget av mislighold; Microsoft vil samarbeide med deg gjennom denne prosessen. Tabellen nedenfor viser noen vanlige situasjoner og sannsynlige svaret, selv om det nøyaktige svaret avhenger av all informasjon som vises under undersøkelsen.

|Hendelse beskrivelse|Sannsynlig svar|
|------------------------|-------------------|
|Leier-nøkkelen er lekket.|-Tasten leier-nøkkelen på nytt. Se den [Nye nøkler leier-nøkkel](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey) delen i dette emnet.|
|En uautorisert person eller skadelig programvare har rettigheter til å bruke leier-nøkkelen, men selve nøkkelen lekker ikke.|Ny inntasting leier nøkkelen ikke hjelper her, og krever analyse av opprinnelig årsak. Hvis en prosess- eller feil var ansvarlig for uautorisert person til å få tilgang, kan denne situasjonen må løses.|
|Sikkerhetsproblem som ble oppdaget i denne generasjonen HSM-teknologi.|Microsoft må oppdatere HSMs. Hvis det er grunn til å tro at dette sikkerhetsproblemet eksponeres nøkler, vil Microsoft be alle kunder til å fornye sine leier nøkler.|
|Sikkerhetsproblemet som ble oppdaget i RSA-algoritmen, eller nøkkellengde eller brute force angrep blir beregningsmessig gjennomførbar.|Microsoft må oppdatere Azure RMS for å støtte nye algoritmer og lengre nøkler som er fleksibel og be alle kunder til å fornye sine leier nøkler.|

## Se også
[Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

