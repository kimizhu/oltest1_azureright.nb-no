---
description: na
keywords: na
title: Logging and Analyzing Azure Rights Management Usage
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
---
# Logging og analysere Azure Rights Management-forbruk
Bruk informasjonen i dette emnet for å hjelpe deg med å forstå hvordan du kan bruke brukslogging med Azure Rights Management (Azure RMS). Azure Rights Management-tjenesten kan logge hver forespørsel om at den gjør for organisasjonen, som omfatter forespørsler fra brukere, handlingene som utføres av Rights Management-administratorer i organisasjonen og handlingene som utføres av Microsoft operatorer til å støtte Azure Rights Management-distribusjon.

Du kan deretter bruke disse loggene Azure Rights Management til å støtte følgende forretningsscenarier:

-   Analysere for de trenger.

    Azure Rights Management skriver loggene i W3C-utvidet loggformat til en Azure lagring konto som du oppgir. Du kan deretter angi disse loggene i et lager av ditt valg (for eksempel en database, et system for OLAP (online analytical processing), eller et kart redusere system) til å analysere informasjonen og lage rapporter. Som et eksempel, kan du identifisere hvem som har tilgang til dataene RMS-beskyttet. Du kan finne ut hva RMS-beskyttet data personer har tilgang til, og hvilke enheter og fra hvor. Du kan finne ut om personer kan lese beskyttet innhold. Du kan også identifisere hvilke personer har lest et viktig dokument som ble beskyttet.

-   Skjerm for misbruk.

    Azure Rights Management loggingsinformasjon er tilgjengelige i nær-sanntid, slik at du kan kontinuerlig overvåke bedriftens bruk av Rights Management. 99,9% av loggene er tilgjengelige innen 15 minutter til en handling som er initiert av RMS.

    Du kan for eksempel varsles hvis det er en plutselig økning av personer som leser RMS-beskyttet data utenfor standard arbeidstimer, som kan indikere at en ondsinnet bruker samler informasjon om å selge til konkurrenter. Eller hvis den samme brukeren tilsynelatende får tilgang til data fra to forskjellige IP-adresser i et kort tidsrom, som kan indikere at en brukerkonto er kompromittert.

-   Utføre juridiske analyse.

    Hvis du har en lekkasje av informasjon, er du sannsynligvis vil bli spurt om hvem som nylig åpnet enkeltdokumenter, og hvilken informasjon en mistanke om personen tilgang til nylig. Du kan svare på denne typen spørsmål når du bruker Azure Rights Management og logging fordi personer som bruker beskyttet innhold må alltid ha en IRM-lisens for å åpne dokumenter og bilder som er beskyttet av Azure Rights Management, selv om disse filene flyttes via e-post eller kopiert til USB-enheter eller andre lagringsenheter. Dette betyr at du kan bruke Azure Rights Management-loggene som en altomfattende informasjonskilde for juridiske analyse når du beskytter dataene ved hjelp av Azure Rights Management.

> [!NOTE]
> Hvis du er interessert bare i logging av administrative oppgaver for Azure Rights Management, og gjør ikke ønsker å spore hvordan brukerne bruker Rights Management, kan du bruke den [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) Windows PowerShell-cmdleten for Azure Rights Management.
> 
> Du kan også bruke Azure portalen for bruk på høyt nivå som inkluderer **RMS-Bruk**, **mest aktive RMS-brukere**, **RMS Enhetsbruk**, og **RMS-aktivert programbruk**. Hvis du vil ha tilgang til disse rapportene fra Azure portal, klikker du **Active Directory**, velg og åpne en mappe, og klikk deretter **rapporter**,

Bruk følgende deler for mer informasjon om Trafikklogging Azure Rights Management.

-   [Slik aktiverer du Trafikklogging Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_EnableRMSLogging)

-   [Hvordan få tilgang til og bruke bruken av Azure Rights Management-logger](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs)

-   [Hvordan du kan administrere lagringsplassen Azure Rights Management-Logg](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_ManageStorage)

-   [Hvordan du delegerer tilgang til bruken av Azure Rights Management-logger](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate)

-   [Slik tolker du bruken av Azure Rights Management-logger](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret)

-   [Windows PowerShell-referanse](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_PowerShell)

## <a name="BKMK_EnableRMSLogging"></a>Slik aktiverer du Trafikklogging Azure Rights Management
Trafikklogging Azure Rights Management er valgfri, slik at hvis du vil bruke den, må du ta bestemte trinn. Når du bruker Rights Management Azure Trafikklogging, skjer det ingen endringer i hvordan Rights Management fungerer og loggføringsprosessen for seg selv er gratis. Du må angi en konto for Azure lagring for loggene, og du vil bli belastet for dette lageret.

Før du begynner, må du kontrollere at du oppfyller følgende forutsetninger for å bruke Azure Rights Management Trafikklogging:

|Krav|Hvis du vil ha mer informasjon|
|--------|----------------------------------|
|Et IT-administrert abonnement som inkluderer Azure Rights Management|Du må ha et abonnement på Microsoft Azure Rights Management som administreres av organisasjonen. Organisasjoner som bruker RMS for personer kan ikke bruke Trafikklogging Azure Rights Management.<br /><br />Hvis organisasjonen har brukere som bruker RMS for enkeltpersoner, gir Azure Rights Management Trafikklogging en svært overbevisende business grunn til å konvertere RMS for personer til et abonnement på Microsoft Azure Rights Management.<br /><br />Hvis du vil ha mer informasjon om hvilke abonnementer som inkluderer Azure RMS, se den [Cloud-abonnementer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet.<br /><br />Hvis du vil ha mer informasjon om RMS for enkeltpersoner, se [RMS for enkeltpersoner og Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)|
|Azure abonnement|Du må ha et abonnement på Azure og tilstrekkelig lagringsplass på Azure for Azure Rights Management-logger.|
|Windows PowerShell for Azure Rights Management|Hvis du ikke allerede har gjort det, kan du laste ned og installere Windows PowerShell-modul for Azure Rights Management. Du vil bruke Windows PowerShell-cmdleter til å konfigurere og administrere Azure Rights Management bruksloggene.<br /><br />Hvis du vil ha mer informasjon, se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).|
Bruk følgende fremgangsmåte for å aktivere Trafikklogging Azure Rights Management, som inneholder trinn for å opprette en konto for Azure lagring og deretter konfigurere Azure for bruk av lagringsplass kontoen for Rights Management-logger.

> [!NOTE]
> Denne fremgangsmåten forutsetter at du har en Azure konto. Trafikklogging Azure Rights Management støtter individuelle konti, men som beste praksis, kan du bruke arbeid eller skolen kontoer. I tillegg anbefaler vi at du oppretter en dedikert lagring konto for Rights Management-logger. Du må dele tilgangstastene lagring med Azure Rights Management og potensielt andre hvis de vil også bruke loggfilene.
> 
> Hvis du vil ha mer informasjon om lagring av Azure, se den [Azure dokumentasjonen for lagring av](http://azure.microsoft.com/documentation/services/storage/).

#### Hvordan du oppretter kontoen for lagring og aktivere Trafikklogging Azure Rights Management

1.  Logg deg på den [Azure portal](https://manage.windowsazure.com/).

2.  Velg **lagring**.

    > [!TIP]
    > Hvis du ikke ser dette alternativet, må du kontrollere at du har et abonnement på Azure, i tillegg til abonnementet for Rights Management.

3.  Klikk **Opprett A lagring konto** og den **URL-adressen**, angi et unikt navn for lagring konto og endre om nødvendig den **plassering/AFFINITET GRUPPEN** slik at den passer til ditt område.

4.  Klikk **OK**, og vent til du ser navnet ditt lagring vise statusen **Online**.

5.  Klikk **Behandle tilgangstaster**.

6.  Fra den **Behandle tilgangstaster** som viser din primære og sekundære nøkler, kopiere den primære nøkkelen til utklippstavlen, og lukk deretter dialogboksen.

7.  Start Windows PowerShell med den **kjøre som administrator for** alternativet. Kjøre den [koble til AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) kommando for å koble til Azure Rights Management-tjenesten:

    ```
    Connect-AadrmService
    ```

8.  Bruk av [Sett AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) kommando for å angi hvor du vil beholde Azure Rights Management bruksloggene, erstatter *&lt; Access_Key &gt;* med den primære nøkkelen som du kopierte i trinn 6 og *&lt; StorageAccount &gt;* med navnet på lagringsplass kontoen du opprettet i trinn 3:

    ```
    $accesskey = convertto-securestring -asplaintext -force –string <Access_Key> Set-AadrmUsageLogStorageAccount -AccessKey $accesskey -StorageAccount <StorageAccount>
    ```

9. Bruk av [Aktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx) kommando for å aktivere logging for bruk av Azure Rights Management:

    ```
    Enable-AadrmUsageLogFeature
    ```
    Du skal se meldingen: **Bruk Logg-funksjonen er aktivert for Rights management-tjenesten.**

Nå som brukslogging er aktivert, Azure Rights Management begynner å logge alle handlinger for organisasjonen, og lagrer denne informasjonen til lagring av kontoen. Av loggingsinformasjon er ikke tilgjengelig før dette tidspunktet.

## <a name="BKMK_AccesAndUseLogs"></a>Hvordan få tilgang til og bruke bruken av Azure Rights Management-logger
Azure Rights Management skriver logger til kontoen din Azure lagring som en rekke BLOBer. Hver blob inneholder én eller flere loggposter i utvidet W3C-loggformat. Blob-navnene er tall, i rekkefølgen de ble opprettet. Den [Slik tolker du bruken av Azure Rights Management-logger](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret) senere i dette dokumentet inneholder mer informasjon om logginnholdet og hvordan opprettes.

Det kan ta litt tid for logger skal vises i lagringsplass kontoen etter en Azure Rights Management-handling. De fleste loggene vises innen 15 minutter.

Lagringsplass kontoen du opprettet for rettighetsadministrasjon Azure bruksloggene er som en postboks og støtter lesing av direkte fra lagringsplass kontoen, men det er ikke optimalisert for å brukes på denne måten. I stedet for best ytelse og for å redusere kostnader, anbefaler vi at du laster ned loggene til lokalt, for eksempel en lokal mappe, en database eller et kart redusere lageret.

Du kan laste ned din bedre effektiviteten på to måter:

-   Bruke Windows PowerShell-cmdlet [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx).

    Dette er den enkleste måten å få tilgang til av bruksloggene. Denne cmdleten laster ned logger av datamaskinen, laster du ned hver blob som en fil på en plassering du angir.

-   Bruk av [Azure lagring SDK](http://www.windowsazure.com/en-us/develop/net/) å skrive dine egne egendefinerte programmet til å laste ned loggene.

    Et egendefinert program kan gi større fleksibilitet enn cmdleten Get-AadrmUsageLogs. Du kan for eksempel delegere nedlasting av loggene til noen eller en prosess som ikke må bruke Azure Rights Management administrativ legitimasjon. Eller du vil avspørre loggene i sanntid, fordi du vil overvåke for misbruk.

#### Å laste ned bruksloggene ved hjelp av PowerShell

-   Start Windows PowerShell med den **Kjør som administrator** alternativ, og kjøre **Get-AadrmUsageLog –Path &lt;location&gt;**. For eksempel når du har opprettet en mappe med navnet **logs** på E-stasjonen:

    -   Å laste ned alle tilgjengelige logger til mappen E:\logs: `Get-AadrmUsageLog -Path "e:\logs"`

    -   Å laste ned en rekke BLOBer: `Get-AadrmUsageLog –Path "e:\logs" –FromCounter 1024 –ToCounter 2047`

Når du kjører disse cmdlets, viser navnet på den siste bloben som ble lastet ned i Windows PowerShell. Du kan tilordne dette navnet til en variabel, som lar deg kjøre Get-AadrmUsageLog i en løkke eller en tidsplan, laster du ned bare trinnvis logger hver gang.

For eksempel:

**PS C:\ &gt; $LastBlobName = Get-AadrmUsageLog – banen "e:\logs"**

**1527**

**PS C:\ &gt; $LastBlobName**

**1527**

> [!TIP]
> Du kan samle alle nedlastede loggfilene til en CSV-format ved hjelp av [Microsofts Logg Parser](http://www.microsoft.com/download/details.aspx?id=24659), som er et verktøy for å konvertere mellom forskjellige velkjente loggformater. Du kan også bruke dette verktøyet til å konvertere data til SYSLOG-format, eller du kan importere den til en database. Når du har installert verktøyet, kjører du **LogParser.exe /?** for hjelp og informasjon for å bruke dette verktøyet. Du kan for eksempel kjøre følgende kommando for å importere all informasjon i et .log format: **logparser –i:w3c –o:csv “SELECT &#42; INTO AllLogs.csv FROM &#42;.log”**.

Du kan stoppe midlertidig og fortsette Trafikklogging. Når du vil stoppe logging, beholder Azure Rights Management kontoinformasjonen lagring slik at du enkelt kan gjenoppta logging på nytt.

#### I hvilemodus og reaktiverer Trafikklogging

-   Hvis du vil stoppe logging, kan du bruke cmdleten følgende: [Deaktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   Hvis du vil gjenoppta logging, kan du bruke cmdleten følgende: [Aktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   Hvis du vil kontrollere om logging er aktivert eller deaktivert, kan du bruke cmdleten følgende: [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

    En verdi på **SANN** betyr at brukslogging er aktivert for Azure Rights Management og en verdi på **False** betyr at brukslogging er deaktivert.

## <a name="BKMK_ManageStorage"></a>Hvordan du kan administrere lagringsplassen Azure Rights Management-Logg
Du blir belastet for lagringsplass som brukes til å holde loggene Azure Rights Management.

Azure Rights Management ikke ingen automatisk behandling av din bruk av loggfiler. Hvis du ikke gjør noe, forblir i lagring-kontoen. Hvis du vil spare plass og redusere lagringskostnadene, kan du likevel å slette dem etter at du har lastet dem ned. Eller du kan velge hvilke filer som skal slettes. Med ett unntak bruker Azure Rights Management ikke disse loggfilene, så det er ingen begrensninger om når du kan slette dem.

Er navnet på filen som du ikke må slette (eller endre) **metadata** som er i den **rms-metadata** beholder. Azure Rights Management bruker denne blob til å holde oversikt over det siste blob-nummeret som ble brukt. Hvis denne filen slettes, Azure Rights Management starter en ny beholder logger med en blob-tall som starter fra 1, og alle fremtidige nedlastinger som bruker cmdleten Get-AadrmUsageLog bruker denne nye beholderen for å laste ned filer. Alle loggene i den opprinnelige beholderen er derfor beholdt, men frittstående. Den eneste måten å laste ned disse foreldreløse loggene er å bruke Azure lagring SDK.

> [!TIP]
> I stedet for å behandle Azure Rights Management Logg lagringen selv, kan du delegere denne management-funksjonen til et annet selskap ved å dele lagringsplass kontoen navnet og få tilgang til nøkkelen. Hvis du vil ha mer informasjon, se den [Hvordan du delegerer tilgang til bruken av Azure Rights Management-logger](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate) senere i dette emnet.

I noen tilfeller vil du kanskje Lag din tilgangstaster for lagring. For eksempel:

-   Du kan endre firma som styrer bruksloggene Azure Rights Management.

-   Du mistenker at nøkkelen storage access settes i fare.

Hvis dette skjer for deg, er når du bruker sekundære hurtigtast (på antakelsen om at du tidligere har brukt den primære nøkkelen) å sikre kontinuitet i tjenesten. Når du genererer på nytt som du ikke tidligere har brukt, kan du deretter konfigurere Azure Rights Management for å bruke den nye nøkkelen. Bruk følgende fremgangsmåte til å generere nøkkelen sekundære bruddene på nytt og konfigurere Azure Rights Management for å bruke den:

#### Generere nøkkelen sekundære bruddene på

1.  Logg deg på den [Azure portal](https://manage.windowsazure.com/).

2.  Velg **lagring**.

3.  Klikk **Behandle tilgangstaster**.

4.  I den **Behandle tilgangstaster** -dialogboksen klikker du **Lag** ved siden av sekundær tilgangstast, og kopier den nye sekundære bruddene nøkkelen til utklippstavlen.

5.  Start Windows PowerShell med den **Kjør som administrator** alternativet og bruker den [Sett AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) cmdlet til å konfigurere Azure Rights Management for å bruke denne nye tilgangstasten erstatter *&lt; StorageAccount &gt;* med navnet på kontoen for lagring og *&lt; Access_Key &gt;* med gjenskapte sekundære hurtigtast du nettopp kopierte:

    ```
    Set-AadrmUsageLogStorageAccount -StorageAccount <StorageAccount>-AccessKey <Access_Key>
    ```
    > [!WARNING]
    > Selv om du kan bytte til en annen lagringsplass kontoen når du kjører denne kommandoen, denne handlingen orphans tidligere loggene og de vil ikke lenger være tilgjengelig for den cmdleten Set-AadrmUsageLogStorageAccount eller lignende kommandoer og funksjoner.

6.  Tilbake i den **Behandle tilgangstaster** dialogboks-boksen, regenerere den primære nøkkelen.

## <a name="BKMK_Delegate"></a>Hvordan du delegerer tilgang til bruken av Azure Rights Management-logger
Du kan delegere tilgang til RMS-logger ved å dele lagringsplass kontoen navnet og få tilgang til nøkkelen. Du vil kanskje representanttilgang til en annen bruker administrative, en utvikler i organisasjonen din eller en uavhengig programvareleverandør (ISV). Fordi de ikke har administratorrettigheter på RMS, kan de bruke cmdleten Get-AardrmUsageLog til å laste ned loggene RMS. I stedet må de bruke Windows Storage SDK til å laste ned loggene. De kan også skrive et program for å lese loggene direkte fra Azure lagring.

Det er trygt å dele lagringsplass kontoen navnet og få tilgang til nøkkelen på denne måten når lagringsplass kontoen er dedikert til RMS-logger. Selv om andre personer som har access-nøkkelen, kan de kan bruke dette til å få tilgang til en annen konto for lagring eller bruke RMS leier kontoen.

## <a name="BKMK_Interpret"></a>Slik tolker du bruken av Azure Rights Management-logger
Bruk informasjonen nedenfor for å hjelpe deg med å tolke bruksloggene Azure Rights Management.

### Lagring konto-oppsett
Første gang Azure Rights Management skriver logger på kontoen for lagring, oppretter følgende to programmer:

-   **Rms-metadata**: Denne beholderen er reservert for Azure Rights Management. Ikke endre eller slette denne beholderen.

-   **Rms - logger - &lt; guid &gt;**: Denne beholderen er der Azure Rights Management oppretter og lagrer loggene. Hvis du ikke lenger vil logging informasjonen de inneholder, kan du trygt slette alle filer i denne beholderen.

Over tid, Azure Rights Management kan opprette flere **Rms - logger - &lt; guid &gt;** beholdere. For eksempel hvis den **Rms-metadata** beholder blir ødelagt eller slettes ved et uhell, Azure Rights Management tilbakestiller innholdet og oppretter en ny **Rms - logger - &lt; guid &gt;** beholder for alle fremtidige logger. Gamle loggene i den gamle beholderen slettes ikke, men er løse.

### Logg-sekvens
Azure rettighetsadministrasjon skriver loggene som en rekke BLOBer. Hver blob inneholder én eller flere loggposter, i utvidet W3C-loggformat.

Navnet på hver blob er et tall. Innenfor hver loggbeholder kalles første blob 000000001. Hver blob heter fortløpende i rekkefølgen den ble opprettet. Hver blob inneholder én eller flere loggposter. Hver loggpost har et UTC-tidsstempel som angir når den tilsvarende forespørselen ble betjent av Azure Rights Management.

> [!IMPORTANT]
> Logging av Azure Rights Management-systemet er optimalisert for å gi deg logger raskt, i stedet for i strengt sekvensiell rekkefølge. Rekkefølgen på BLOBer, i tillegg til rekkefølgen på loggposter innenfor en blob, kanskje ikke i kronologisk rekkefølge. Det er den eneste grunnen til BLOBer kalles sekvensielt slik at du kan effektivt laste dem ned trinnvis.
> 
> To eksempler på mulige Logg sekvens resultater:
> 
> -   Loggposter i blob-000000004 kan overlappe kronologisk med loggposter i blob-000000003. I et ekstremt tilfelle kan alle loggposter i blob 000000004 genereres før alle loggposter i blob-000000003.
> -   Den andre loggposten i en blob kan ha blitt generert før den første loggposten, men ble skrevet til lagring i omvendt rekkefølge.

Før du analyserer Azure Rights Management bruksloggene, anbefaler vi at du laster ned og importere loggen til en database der du kan sortere logger basert på deres tidsstempel. Hvis du vil ha mer informasjon om å laste ned loggene, se den [Hvordan få tilgang til og bruke bruken av Azure Rights Management-logger](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs) delen i dette emnet.

Siden loggene ikke nødvendigvis kronologisk, men fleste av dem er skrevet i løpet av 15 minutter av forespørselen, når du identifiserer loggene som du vil bruke ved hjelp av deres tidsstempel, må du legge til 15 minutter til tiden du er interessert i. Deretter laster du ned disse loggene. Denne strategien skal sørge for at du får nesten alle logger.

En ting å huske er at tidsstempelet på hver loggpost er lokal tid av Azure Rights Management-tjenesten behandlet forespørselen. Ettersom Azure Rights Management kjører på flere servere på tvers av flere datasenter, kan noen ganger loggene virke å være i feil rekkefølge, selv når de sorteres etter deres tidsstempel. Imidlertid er de ulike liten og vanligvis innenfor et minutt. I de fleste tilfeller er dette ikke et problem som ville være et problem for analyse av loggen.

### Blob-format
Hver blob er utvidet W3C-loggformat. Den starter med følgende to linjer:

**#Software: RMS**

**#Version: 1.1**

Den første linjen angir at disse er Azure Rights Management-logger. Den andre linjen angir at resten av BLOBen følger versjon 1.1-spesifikasjonen. Vi anbefaler at alle programmer som kan analysere disse loggene kontrollerer disse to linjer før du fortsetter å analysere resten av BLOBen.

Den tredje linjen lister opp en liste over feltnavn som er atskilt med tabulatorer:

**#Fields: dato tid rad-ID-typen til forespørselen om bruker-id resultatet Korrelasjons-id innholds-id eier e-utstederen mal-id filnavn Utgivelsesdato c-info c-ip**

Hver av de etterfølgende linjene er en loggpost. Verdiene i feltene er i samme rekkefølge som den foregående linjen, og er atskilt med tabulatorer. Bruk tabellen nedenfor til å tolke feltene.

|Feltnavn|W3C-datatype|Beskrivelse|Verdien for eksempel|
|------------|----------------|---------------|------------------------|
|dato|Dato|UTC-datoen da forespørselen ble vist.<br /><br />Kilden er den lokale klokken på serveren som betjenes av forespørselen.|2013-06-25|
|tid|Tid|UTC-tid i 24-timers format når forespørselen ble vist.<br /><br />Kilden er den lokale klokken på serveren som betjenes av forespørselen.|21:59:28|
|rad-id|Tekst|Unik GUID for denne loggposten.<br /><br />Denne verdien er nyttig når du samle logger eller Kopier logger til et annet format.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|Forespørsel-type|Navn|Navnet på RMS-API som ble forespurt.|AcquireLicense|
|bruker-id|Streng|Brukeren som sendte forespørselen.<br /><br />Verdien er omsluttet av enkle anførselstegn. Noen forespørselstyper er anonym, da verdien er ".|'en joe@contoso.com'|
|resultatet|Streng|'Fullført' hvis forespørselen ble vist vellykket.<br /><br />Feiltype i enkle anførselstegn hvis forespørselen mislyktes.|'Fullført'|
|Korrelasjons-id|Tekst|GUIDEN som er felles mellom RMS-klienten logg og Logg på server for en bestemt forespørsel.<br /><br />Denne verdien kan være nyttig for å feilsøke problemer med klienten.|cab52088-8925-4371-be34-4b71a3112356|
|Innholds-id|Tekst|GUID, omsluttet av klammeparenteser som identifiserer det beskyttede innholdet (for eksempel et dokument).<br /><br />Dette feltet har en verdi Hvis typen til forespørselen om AcquireLicense og er tomt for alle andre forespørselstyper.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|eieren av e-post|Streng|E-postadressen til eieren av dokumentet.|alice@contoso.com|
|utsteder|Streng|E-postadressen til utstederen av dokumentet.|alice@contoso.com (eller) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Mal-id|Streng|IDen for malen som brukes til å beskytte dokumentet.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|Filnavn|Streng|Filnavnet på dokumentet som ble beskyttet.|TopSecretDocument.docx|
|Publisert av dato|Dato|Datoen da dokumentet ble beskyttet.|2015-10-15T21:37:00|
|c-info|Streng|Informasjon om klient-plattform som foretar forespørselen.<br /><br />Den bestemte strengen varierer, avhengig av programmet (for eksempel operativsystemet eller leseren).|' MSIPC; versjon = 1.0.623.47; Prognavn = WINWORD. EXE; AppVersion = 15.0.4753.1000; AppArch = x 86; OSName = Windows: OSVersion = 6.1.7601; OSArch = amd64'|
|c-ip|Adresse|IP-adressen til klienten som kommer med forespørselen.|64.51.202.144|

#### Unntak for feltet bruker-id
Selv om bruker-id-feltet angir vanligvis brukeren som sendte forespørselen, er det to unntak der verdien ikke er tilordnet til en ekte bruker:

-   Verdien **' microsoftrmsonline ved &lt; YourTenantID &gt;. rms. &lt; område &gt;. aadrm.com'**.

    Dette indikerer en Office 365-tjeneste, for eksempel Exchange Online eller Sharepoint Online, er å gjøre forespørselen. I strengen, *&lt; YourTenantID &gt;* er GUIDEN for din leier og *&lt; område &gt;* er området der leier er registrert. For eksempel **na** representerer Nord-Amerika, **eu** representerer Europa, og **ap** representerer Asia.

-   Hvis du bruker RMS-koblingen.

    Forespørsler fra denne koblingen er logget med hovednavn for tjeneste RMS genereres automatisk når du installerer RMS-koblingen.

#### Vanlig forespørselstyper
Det finnes mange forespørselstyper for Azure Rights Management, men tabellen nedenfor viser noen av de mest vanlige forespørselstyper.

|Type forespørsel|Beskrivelse|
|--------------------|---------------|
|AcquireLicense|en klient fra en Windows-basert maskin ber om en lisens til RMS-beskyttet innhold.|
|AcquirePreLicense|en-klient på vegne av brukeren ber om en lisens til RMS-beskyttet innhold.|
|AcquireTemplates|et kall ble gjort til får maler som er basert på malen IDer|
|AcquireTemplateInformation|et kall ble gjort til å hente IDer med malen fra tjenesten.|
|AddTemplate|oppringingen blir foretatt fra Azure portal for å legge til en mal.|
|BECreateEndUserLicenseV1|et kall gjøres fra en mobil enhet til å opprette en sluttbrukerlisens.|
|BEGetAllTemplatesV1|et kall gjøres fra en mobil enhet (back-end) til å hente alle malene.|
|Certify|klienten er sertifisering innholdet for beskyttelse.|
|Dekryptere|klienten forsøker å dekryptere det RMS-beskyttet innholdet.|
|DeleteTemplateById|et kall gjøres fra Azure portal til å slette en mal og mal-ID.|
|ExportTemplateById|oppringingen blir foretatt fra Azure portal til å eksportere en mal basert på en mal-ID|
|FECreateEndUserLicenseV1|ligner på AcquireLicense-forespørselen, men fra mobile enheter.|
|FECreatePublishingLicenseV1|det samme som Certify og GetClientLicensorCert kombineres, fra mobile klienter.|
|FEGetAllTemplates|et kall gjøres, fra en mobil enhet (front) til å hente malene.|
|GetAllTemplates|oppringingen blir foretatt fra Azure portal for å få alle malene.|
|GetClientLicensorCert|klienten ber om et sertifikat for publisering (som senere brukes til å beskytte innhold) fra en Windows-basert datamaskin.|
|GetConfiguration|kalles en Azure PowerShell-cmdleten for å få konfigurasjonen av Azure RMS-leier.|
|GetConnectorAuthorizations|et kall gjøres fra RMS-koblinger til å få sine konfigurasjoner fra skyen.|
|GetTenantFunctionalState|The Azure portal kontrollerer om Azure RMS er aktivert.|
|GetTemplateById|oppringingen blir foretatt fra Azure portal for å få en mal ved å angi en mal-ID|
|ExportTemplateById|et kall gjøres fra Azure portal til å eksportere en mal ved å angi en mal-ID|
|FindServiceLocationsForUser|et kall gjøres til å søke etter URL-adresser, som brukes til å kalle Certify eller AcquireLicense.|
|ImportTemplate|et kall gjøres fra Azure portal til å importere en mal.|
|ServerCertify|oppringingen blir foretatt et RMS-aktivert klient (for eksempel SharePoint) for å sertifisere serveren.|
|SetUsageLogFeatureState|et kall gjøres til å aktivere Trafikklogging.|
|SetUsageLogStorageAccount|et kall gjøres til å angi plasseringen av Azure RMS-loggene.|
|SignDigest|et kall gjøres når en nøkkel brukes for å signere formål. Dette kalles vanligvis én gang per AcquireLicence (eller FECreateEndUserLicenseV1), Certify, og GetClientLicensorCert (eller FECreatePublishingLicenseV1).|
|UpdateTemplate|et kall gjøres fra Azure portal til å oppdatere en eksisterende mal.|

## <a name="BKMK_PowerShell"></a>Windows PowerShell-referanse
Bruk følgende Windows PowerShell-cmdleter til å hjelpe deg med å konfigurere og bruke Azure Rights Management Trafikklogging:

-   [Deaktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Aktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Sett AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Hvis du vil ha mer informasjon om hvordan du bruker Windows PowerShell for Azure Rights Management, se [Administrasjon av Azure Rights Management ved hjelp av Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Se også
[Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md)

