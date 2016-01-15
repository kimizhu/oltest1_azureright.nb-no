---
description: na
keywords: na
title: Migrating from AD RMS to Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
---
# Migrering fra AD RMS til Azure Rights Management
Bruk følgende sett med instruksjoner for å migrere Active Directory Rights Management Services (AD RMS)-distribusjon til Azure Rights Management (Azure RMS). Etter en overføring, brukere vil fortsatt ha tilgang til dokumenter og e-postmeldinger i organisasjonen beskyttet ved hjelp av AD RMS og nylig beskyttet innhold vil bruke Azure RMS.

Ikke sikker på om denne AD RMS-overføring er riktige for din organisasjon?

-   For en introduksjon til Azure RMS, business-problemer som det kan løse, hvordan det ser ut til administratorer og brukere og hvordan det fungerer, kan du se [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md)

-   En sammenligning mellom Azure RMS med AD RMS, se [Sammenligne Azure Rights Management og AD RMS](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md).

## Forutsetninger for å overføre AD RMS til Azure RMS
Før du starter overføringen til Azure RMS, må du kontrollere at følgende forutsetninger er på plass, og at du forstår alle begrensninger.

|Krav|Hvis du vil ha mer informasjon|
|--------|----------------------------------|
|En støttet RMS-distribusjon|Alle versjoner av AD RMS fra Windows Server 2008 og Windows Server 2012 R2 støtter migrering til Azure RMS:<br /><br />-   Windows Server 2008 (x 86 eller x 64)<br />-   Windows Server 2008 R2 (x 64)<br />-   Windows Server 2012 (x 64)<br />-   Windows Server 2012 R2 (x 64) **Note:** Hvis du kjører Windows RMS på Windows Server 2003, blir denne versjonen av operativsystemet ikke støttes under 2015. Du kan overføre denne versjonen av RMS til Azure RMS, men denne prosessen støttes bare hvis operativsystemet støttes fortsatt. For å unngå dette, kan du importere klarerte publisering domenet (TPD) til en versjon av AD RMS som støttes, og deretter importere TPD uten alternativet for RMS 1.0-kompatibilitet. Hvis du vil ha mer informasjon om TPDs, kan du se [Trusted Publishing Domain](http://technet.microsoft.com/library/dd996639%28v=ws.10%29.aspx)<br />Alle gyldige AD RMS-topologi støttes:<br /><br />-   Enkel skog, enkel RMS-klyngen<br />-   Én skog, flere bare lisensiering RMS-klynger<br />-   Flere skoger, flere RMS-klynger **Note:** Som standard overfører flere RMS-klynger til en enkelt Azure RMS leier. Hvis du ønsker en annen RMS-eiere, må du behandle dem som forskjellige overføringer. En nøkkel fra én RMS-klyngen kan ikke importeres til mer enn én Azure RMS leier.|
|Alle kravene til å kjøre Azure RMS, inkludert en Azure RMS leier (ikke aktivert)|Se [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).<br /><br />Selv om du må ha en Azure RMS leier før du kan overføre fra AD RMS, anbefaler vi at du ikke aktiverer Rights Management-tjenesten før overføringen. Dette trinnet omfatter overføringsprosessen med etter at du har eksportert nøkler og maler fra AD RMS og importert dem til Azure RMS. Imidlertid Hvis Azure RMS allerede er aktivert, kan du fremdeles overføre fra AD RMS.|
|Forberedelse av Azure RMS:<br /><br />-   Directory-synkronisering mellom den lokale katalogen og Azure Active Directory<br />-   E-post grupper i Active Directory-Azure|Se [Forbereder Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).|
|Hvis du har brukt funksjonen (IRM-Information Rights Management) for Exchange Server (for eksempel Transportregler og Outlook Web Access) eller SharePoint Server med AD RMS:<br /><br />-   Planlegge for en kort periode når IRM ikke vil være tilgjengelig på disse serverne|Du kan fortsette å bruke IRM på disse serverne med Azure RMS etter migreringen. En av overføringstrinnene er imidlertid å midlertidig deaktivere IRM-tjenesten, installere og konfigurere en kobling, konfigurere servere og aktivere IRM på nytt.<br /><br />Dette er det eneste avbruddet til tjeneste under overføringsprosessen.|
Begrensninger:

-   Selv om overføringsprosessen støtter overføring av din server licensing sertifikat (SLC) nøkkel til hardware sikkerhetsmodul (HSM) for Azure RMS, støtter Exchange Online for øyeblikket ikke denne konfigurasjonen. Hvis du vil ha full IRM-funksjonalitet med Exchange Online når du overfører til Azure RMS, Azure RMS leier nøkkelen må være [administreres av Microsoft](http://technet.microsoft.com/library/dn440580.aspx). Du kan eventuelt kjøre IRM med redusert funksjonalitet i Exchange Online når Azure RMS-leier behandles av deg (BYOK). Hvis du vil ha mer informasjon om hvordan du bruker Exchange Online med Azure RMS, se [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration) i disse instruksjonene.

-   Hvis du har programvaren og -klienter som ikke støttes med Azure RMS, vil de ikke kunne beskytte eller forbruker innhold som er beskyttet av Azure RMS. Husk å sjekke støttede programmer og klienter-delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet.

-   Hvis du importerer den lokale nøkkelen til Azure RMS som arkivert (du ikke definerer TPD skal være aktiv under importprosessen) og du overføre brukere satsvis for en tretrinns overføring, innhold som nylig er beskyttet av overførte brukere vil ikke være tilgjengelig for brukere som beholdes på AD RMS. I dette scenariet, når det er mulig, holde overføringstid kort og overføre brukere i logiske grupper, slik at hvis de samarbeider med en annen, flyttes de sammen.

    Denne begrensningen gjelder ikke når du setter TPD til aktiv under importprosessen, fordi alle brukerne vil beskytte innholdet ved hjelp av den samme nøkkelen. Vi anbefaler denne konfigurasjonen fordi du kan overføre alle brukere uavhengig av hverandre og i ditt eget tempo.

-   Hvis du kan samarbeide med eksterne partnere (for eksempel ved hjelp av klarert bruker domener eller føderasjonen), må de også overføre til Azure RMS enten samtidig som migreringen, eller så snart som mulig etterpå. For å fortsette å få tilgang til innhold at organisasjonen tidligere beskyttet ved hjelp av AD RMS, de må klienten konfigurasjonsendringer som ligner på de som du gjør, og er inkludert i dette dokumentet.

    På grunn av mulige konfigurasjoner variasjoner som partnerne kan ha, er nøyaktige instruksjoner for denne rekonfigurering utenfor området for dette dokumentet. Hvis du trenger hjelp, kan du kontakte Microsofts kundestøttetjeneste (CSS).

## Trinn for å overføre AD RMS til Azure RMS

|Trinn for overføring|Hvis du vil ha mer informasjon|
|------------------------|----------------------------------|
|**1. Last ned Azure RMS-administrasjonsverktøy for administrasjon**|For instruksjoner, se [Step 1: Download the Azure Rights Management Administration Tool](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step1Migration).|
|**2. Eksporter konfigurasjonsdata fra AD RMS og importere den til Azure RMS**|Du eksporterer konfigurasjonen (nøkler, maler, URL-adresser) fra AD RMS til en XML-fil, og deretter laste opp filen til Azure RMS ved hjelp av Import-AadrmTpd Windows PowerShell-cmdleten. Forholdsregler kan trenge, avhengig av din på viktige AD RMS-konfigurasjon:<br /><br />-   Programvare-beskyttede nøkkelen til programvare-beskyttede nøkler overføring: Sentralt administrerte, passordbaserte nøkler i AD RMS til Microsoft-administrerte Azure RMS leier nøkkel. Dette er den enkleste banen for migrering og kreves ingen ekstra trinn.<br />-   HSM-beskyttede nøkkelen til HSM-beskyttede nøkler overføring: Nøkler som lagres som en HSM for AD RMS til kunde-administrerte Azure RMS leier nøkkel (den "hente din egen nøkkel" eller BYOK scenario). Dette krever flere trinn for å overføre nøkkelen fra din lokale Thales HSM til Azure RMS HSM.<br />-   Programvare-beskyttede nøkkelen til HSM-beskyttede nøkler overføring: Sentralt administrerte passordbaserte nøkler i AD RMS til kunde-administrerte Azure RMS leier nøkkel (den "hente din egen nøkkel" eller BYOK scenario). Dette forutsetter at de fleste konfigurasjonen fordi må du først pakke ut nøkkelen programvare og importere den til et lokale HSM, og gjør deretter flere trinn for å overføre nøkkelen fra din lokale Thales HSM til Azure RMS HSM.<br /><br />For instruksjoner, se [Step 2. Export configuration data from AD RMS and import it to Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step2Migration).|
|**3. Aktivere RMS-leier**|Hvis det er mulig, kan du utføre dette trinnet etter importen og ikke før.<br /><br />For mer informasjon og instruksjoner, kan du se [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).|
|**4. Konfigurere importerte maler**|Når du importerer policymaler for rettigheter, er deres status arkivert. Hvis du vil at brukere skal kunne se og bruke dem, må du endre status for skjemamal som publiseres i Azure Management-portalen.<br /><br />For instruksjoner, se [Step 4. Configure imported templates](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step4Migration).|
|**5. Konfigurere klienter til å bruke RMS Azure**|Eksisterende Windows-datamaskiner må konfigureres for å bruke Azure RMS-tjeneste i stedet for AD RMS. Dette trinnet gjelder for datamaskiner i din organisasjon, og datamaskiner i partnerorganisasjoner Hvis du har samarbeidet med dem mens du kjørte AD RMS.<br /><br />Hvis du har distribuert i tillegg til [filtyper på mobil enhet](http://technet.microsoft.com/library/dn673574.aspx) for å støtte mobile enheter som telefoner iOS og iPads, Android telefoner og tavler, Windows phone og Mac-datamaskiner, må du fjerne SRV-poster i DNS som omadressert disse klientene til å bruke AD RMS.<br /><br />For instruksjoner, se [Step 5. Reconfigure clients to use Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step5Migration).|
|**6. Konfigurere IRM integrasjonen med Exchange Online**|Dette trinnet er nødvendig hvis du vil bruke Exchange Online med Azure RMS.<br /><br />For instruksjoner, se [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration).|
|**7. Distribuere RMS-kobling**|Dette trinnet er nødvendig hvis du vil bruke en av følgende lokale tjenester med Azure RMS:<br /><br />-   Exchange Server (for eksempel Transportregler og Outlook Web Access)<br />-   SharePoint Server<br />-   Windows-Server som kjører filen klassifisering infrastruktur<br /><br />For instruksjoner, se [Step 7. Deploy the RMS connector](#BKMK_Step7Migration).|
|**8. Dekommisjonering av AD RMS**|Når du har bekreftet som alle klientene som bruker RMS Azure og ikke lenger tilgang til AD RMS-servere, kan du avslutte AD RMS-distribusjon.<br /><br />For instruksjoner, se [Step 8. Decommission AD RMS](#BKMK_Step8Migration).|
|**9. Nye nøkler Azure RMS leier nøkkelen**|Dette trinnet er nødvendig hvis du kjørte ikke i kryptografiske modus 2 før overføringen, og valgfri, men anbefales for alle overføringer å beskytte sikkerheten til Azure RMS leier-tasten.<br /><br />For instruksjoner, se [Step 9. Re-key your Azure RMS tenant key](#BKMK_Step9Migration).|

### <a name="BKMK_Step1Migration"></a>Trinn 1: Laste ned verktøyet Azure Rights Management-Administrasjon
Gå til Microsoft Download Center og laste ned den [Azure Rights Management-administrasjonsverktøy](http://go.microsoft.com/fwlink/?LinkId=257721), som inneholder Azure RMS Administrasjon-modulen for Windows PowerShell.

### <a name="BKMK_Step2Migration"></a>Trinn 2. Eksporter konfigurasjonsdata fra AD RMS og importere den til Azure RMS
Dette trinnet er en prosess i to deler:

1.  Eksporter konfigurasjonen av data fra AD RMS ved å eksportere de klarerte publisering domenene (TPDs) til en XML-fil. Denne prosessen er den samme for alle overføringer.

2.  Importere konfigurasjonsdataene til Azure RMS. Det finnes forskjellige prosesser for dette trinnet, avhengig av den gjeldende konfigurasjonen for AD RMS-distribusjon og foretrukne topologien for Azure RMS leier-tasten.

#### Eksporter konfigurasjonen av data fra AD RMS
Gjør følgende på alle AD RMS-klynger, for alle klarerte publisering domener som har beskyttet innhold for organisasjonen. Du trenger ikke å kjøre denne på bare lisensiering klynger.

> [!NOTE]
> Følg denne fremgangsmåten hvis du bruker Rights Management for Windows Server 2003, i stedet for disse instruksjonene, [eksportere SLC, TUD, TPD og RMS privatnøkkelen](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) fra den [overføring fra Windows RMS til AD RMS i en annen infrastruktur](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) emnet.

###### Hvis du vil eksportere konfigurasjonsdataene klarert (domeneinformasjon for publisering)

1.  Logg på AD RMS-klyngen som en bruker med AD RMS administrasjonsrettigheter.

2.  Fra AD RMS-administrasjonskonsollen (**Active Directory Rights Management Services**), Utvid klyngenavnet AD RMS, **stoler policyer**, og klikk deretter **klarerte domener som publiserer**.

3.  Velg det klarerte domenet for publisering i resultater-ruten, og fra handlinger-ruten, klikk **Eksporter klarert domene publisering**.

4.  I den **Eksporter klarert av publisering domene** dialogboks:

    -   Klikk **Lagre som** og lagre bane og et filnavn for ditt valg. Sørg for å angi **.xml** som filtype (dette ikke er lagt til automatisk).

    -   Angi og Bekreft et sterkt passord. Husk dette passordet, fordi du trenger den senere, når du importerer konfigurasjonsdataene til Azure RMS.

    -   Ikke Merk av for å lagre filen klarert domene i RMS-versjon 1.0.

Når du har eksportert alle klarerte publisering domener, er du klar til å starte prosedyren for å importere disse dataene til Azure RMS.

#### Importere konfigurasjonsdataene til Azure RMS
Nøyaktige fremgangsmåten for dette trinnet avhenger av den gjeldende konfigurasjonen for AD RMS-distribusjon og foretrukne topologien for Azure RMS leier-tasten.

Gjeldende AD RMS distribusjonen skal bruke én av følgende konfigurasjoner for server LISENSGIVEREN sertifikat (SLC) nøkkelen:

-   Passordbeskyttelse i AD RMS-databasen. Dette er standardkonfigurasjonen.

-   HSM beskyttelse ved hjelp av en Thales hardware security module (HSM).

-   HSM beskyttelse ved å bruke en hardware sikkerhetsmodul (HSM) fra en annen leverandør enn Thales.

-   Passordet er beskyttet ved hjelp av en ekstern kryptografileverandøren.

> [!NOTE]
> Hvis du vil ha mer informasjon om bruk av maskinvare sikkerhet moduler med AD RMS, se [ved hjelp av AD RMS med maskinvare sikkerhet moduler](http://technet.microsoft.com/library/jj651024.aspx).

To Azure RMS leier viktige topologi alternativene er: Styrer Microsoft leier-tasten (**Microsoft-administrerte**) eller du administrere leier-tasten (**Kunde-administrerte**). Når du administrerer din egen Azure RMS leier nøkkel, det blir noen ganger referert til som "hente din egen nøkkel" (BYOK) og krever en hardware security module (HSM) fra Thales. Hvis du vil ha mer informasjon, se den [Choose your tenant key topology: Managed by Microsoft (the default) or managed by you (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ChooseTenantKey) delen i den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emnet.

> [!IMPORTANT]
> Exchange Online er ikke kompatibel med Azure RMS-BYOK.  Hvis du vil bruke BYOK etter migreringen og planlegger å bruke Exchange Online, må du kontrollere at du forstår hvordan denne konfigurasjonen reduserer IRM-funksjonalitet for Exchange Online. Les informasjonen i den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) delen i den  [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne for å hjelpe deg å velge den beste Azure RMS for klientadministrasjon viktige topologi for migreringen.

Bruk tabellen nedenfor til å identifisere hvilken fremgangsmåte som skal brukes for migreringen. Kombinasjoner som ikke er oppført, støttes ikke.

|Gjeldende AD RMS-distribusjon|Valgt Azure RMS leier viktige topologi|Instruksjoner for overføring|
|---------------------------------|------------------------------------------|--------------------------------|
|Passordbeskyttelse i AD RMS-databasen|Microsoft-administrerte|Se den **programvare-beskyttede nøkkelen til programvare-beskyttede nøkler migrering** prosedyren etter denne tabellen.<br /><br />Dette er den enkleste banen for migrering og krever bare at du overfører din konfigurasjonsdataene til Azure RMS.|
|HSM beskyttelse ved hjelp av en Thales nShield hardware security module (HSM)|Kunde-administrerte (BYOK)|Se den **HSM-beskyttede nøkkelen til HSM-beskyttede nøkler migrering** prosedyren etter denne tabellen.<br /><br />Dette krever verktøysettet BYOK og to sett med trinn for å overføre nøkkelen fra din lokale HSM til Azure RMS-HSMs og deretter overføre konfigurasjonsdataene til Azure RMS.|
|Passordbeskyttelse i AD RMS-databasen|Kunde-administrerte (BYOK)|Se den **programvare-beskyttede nøkkelen til HSM-beskyttede nøkler migrering** prosedyren etter denne tabellen.<br /><br />Dette krever verktøysettet BYOK og tre trinnsettene først pakke ut programvarenøkkel og importere den til en lokale HSM, deretter overføre nøkkelen fra din lokale HSM til Azure RMS-HSMs, og Overfør til slutt i konfigurasjonsdataene til Azure RMS.|
|HSM beskyttelse ved å bruke en hardware sikkerhetsmodul (HSM) fra en annen leverandør enn Thales|Kunde-administrerte (BYOK)|Kontakt leverandøren du HSM for instruksjoner om hvordan du overfører din nøkkel fra denne HSM til en Thales nShield Hardware Security Module (HSM). Deretter følger du instruksjonene for den **HSM-beskyttede nøkkelen til HSM-beskyttede nøkler migrering** prosedyren etter denne tabellen.|
|Passordet er beskyttet ved hjelp av en ekstern kryptografileverandøren|Kunde-administrerte (BYOK)|Kontakt leverandøren hvis du kryptografileverandøren instruksjoner overføre nøkkelen til en Thales nShield hardware security module (HSM). Deretter følger du instruksjonene for den **HSM-beskyttede nøkkelen til HSM-beskyttede nøkler migrering** prosedyren etter denne tabellen.|
Før du starter denne fremgangsmåten, kontroller at du har tilgang til XML-filer som du opprettet tidligere når du har eksportert de klarerte domenene for publisering. Dette kan for eksempel lagres på en USB-enhet som du flytter fra AD RMS-serveren til Internett-tilkoblede arbeidsstasjonen.

> [!NOTE]
> Imidlertid kan du lagre disse filene, Bruk fremgangsmåter til å beskytte dem, fordi disse dataene inkluderer den private nøkkelen.

##### Programvare-beskyttede nøkkelen til programvare-beskyttede nøkler migrering
Bruk denne fremgangsmåten til å importere AD RMS-konfigurasjonen til Azure RMS, vil resultere i Azure RMS leier nøkkelen som administreres av Microsoft.

###### Importere konfigurasjonsdataene til Azure RMS

1.  På en Internett-tilkoblede arbeidsstasjon, laste ned og installere Windows PowerShell-modul for Azure RMS (minimum versjon 2.1.0.0), som inneholder den [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdleten.

    > [!TIP]
    > Hvis du tidligere har lastet ned og installert modulen, kontrollerer du versjonsnummeret ved å kjøre: `(Get-Module aadrm -ListAvailable).Version`

    For å lese installasjonsinstrukser, kan du se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

2.  Start Windows PowerShell med den **Kjør som administrator** alternativet og bruker den [koble til AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) cmdlet til å koble til tjenesten Azure RMS:

    ```
    Connect-AadrmService
    ```
    Når du blir spurt, skriver du inn din [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for klientadministrasjon administratorlegitimasjon (vanligvis bruker du en konto som er en global administrator for Azure Active Directory eller Office 365).

3.  Bruk av [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet til å laste opp først eksportert klarerte publisering domene (XML) fil. Hvis du har mer enn én XML-filen fordi du hadde flere publisering klarerte domener, velger du filen som inneholder det eksporterte klarerte publisering domenet du vil bruke i Azure RMS for å beskytte innhold etter migreringen. Bruker du følgende kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    For eksempel: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Når du blir spurt, skriver du inn passordet du angav tidligere, og Bekreft at du vil utføre denne handlingen.

4.  Når kommandoen er fullført, kan du Gjenta trinn 3 for hver gjenstående XML-filen du opprettet ved å eksportere de klarerte domenene for publisering. Men for disse filene, kan du angi **-Active** til **false** Når du kjører Import-kommandoen. For eksempel: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Bruk av [Koble fra AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) cmdlet til å koble fra Azure RMS-tjenesten:

    ```
    Disconnect-AadrmService
    ```

Du er nå klar til å gå til [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### HSM-beskyttede nøkkelen til HSM-beskyttede nøkler migrering
Det er en todelt prosedyre til å importere HSM-tasten og konfigurasjon for AD RMS til Azure RMS, vil resultere i Azure RMS leier nøkkelen som administreres av deg (BYOK).

Du må først pakke HSM-tasten slik at den er klar til å overføre til Azure RMS, og deretter importere den med konfigurasjonsdataene.

###### Del 1: Pakke HSM-tasten slik at den er klar til å overføre til Azure RMS

1.  Følg trinnene i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen av den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md), ved hjelp av fremgangsmåten **Generer og overfør ditt leier nøkkel – via Internett** med følgende unntak:

    -   Ikke bruk fremgangsmåten for **generere leier-nøkkel**, fordi du allerede har tilsvarende fra AD RMS-distribusjon. Du må identifisere nøkkelen som brukes av AD RMS-serveren fra Thales-installasjonen og bruker denne nøkkelen under overføringen. Thales krypterte viktige filer, kalles vanligvis **key_(keyAppName)_(keyIdentifier)** lokalt på serveren.

    -   Ikke bruk fremgangsmåten for **overføre leier nøkkelen til Azure RMS**, som bruker kommandoen Legg til AadrmKey.  I stedet vil du overføre forberedt HSM nøkkelen når du laster opp eksporterte klarerte publisering domenet ditt, ved hjelp av kommandoen Importer-AadrmTpd.

2.  Koble til Azure RMS-tjenesten i Windows PowerShell-økt på en Internett-tilkoblede arbeidsstasjon.

Nå som du har forberedt HSM-nøkkel for Azure RMS, er du klar til å importere nøkkelfilen for HSM og AD RMS-konfigurasjonsdata.

###### Del 2: Importere HSM-tasten og konfigurasjon av dataene til Azure RMS

1.  Fortsatt på en arbeidsstasjon med Internett-tilkobling og Windows PowerShell-økten, laste opp første eksporterte klarerte publisering domene (.xml) filen. Hvis du har mer enn én XML-filen fordi du hadde flere publisering klarerte domener, velger du filen som inneholder de eksporterte klarerte publisering domenet som tilsvarer HSM-tasten du vil bruke i Azure RMS for å beskytte innhold etter migreringen. Bruker du følgende kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    For eksempel: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Når du blir spurt, skriver du inn passordet du angav tidligere, og Bekreft at du vil utføre denne handlingen.

2.  Når kommandoen er fullført, kan du Gjenta trinn 1 for hver gjenstående XML-filen du opprettet ved å eksportere de klarerte domenene for publisering. Men for disse filene, kan du angi **-Active** til **false** Når du kjører Import-kommandoen.  For eksempel: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Bruk av [Koble fra AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet til å koble fra Azure RMS-tjenesten:

    ```
    Disconnect-AadrmService
    ```

Du er nå klar til å gå til [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### Programvare-beskyttede nøkkelen til HSM-beskyttede nøkler migrering
Det er en tredelt prosedyre til å importere AD RMS-konfigurasjonen til Azure RMS, vil resultere i Azure RMS leier nøkkelen som administreres av deg (BYOK).

Du må først pakke ut din server LISENSGIVEREN sertifikat (SLC) nøkkel fra konfigurasjonsdataene og overføre nøkkelen til en lokale Thales HSM, og deretter pakke og overføre HSM-nøkkelen til Azure RMS, og deretter importere konfigurasjonsdataene.

###### Del 1: Trekke ut din SLC fra konfigurasjonsdataene og importere nøkkelen til din lokale HSM

1.  Bruk følgende trinn i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen av den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne:

    -   **Generer og overfør ditt leier nøkkel – via Internett**: **Klargjør Internett-tilkoblede arbeidsstasjonen**

    -   **Generer og overfør ditt leier nøkkel – via Internett**: **Forberede pulten frakoblet**

    Ikke Følg fremgangsmåten for å generere nøkkelen leier, fordi du allerede har tilsvarende i den eksporterte konfigurasjonsfilen dataene (XML). I stedet vil du kjøre en kommando for å pakke ut denne nøkkelen fra filen og importerer den til din lokale HSM.

2.  På frakoblet arbeidsstasjonen, kjører du følgende kommando:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    For eksempel for Nord-Amerika: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Tilleggsinformasjon:

    -   Parameteren ImportRmsCentrallyManagedKey angir at operasjonen er å importere SLC-nøkkelen.

    -   Hvis du ikke angir passordet for kommandoen, blir du bedt om å angi den.

    -   KeyIdentifier-parameteren er for en egendefinert nøkkelnavnet som oppretter filen navnet. Du må bare bruke små ASCII-tegn.

    -   Parameteren ExchangeKeyPackage angir en områdespesifikk nøkkelutveksling key (KEK)-pakken som har et navn som begynner med BYOK-KEK - pkg-.

    -   Parameteren NewSecurityWorldPackage angir en bestemt region verden sikkerhetspakken som har et navn som begynner med BYOK-SecurityWorld - pkg-.

    Denne kommandoen gir følgende:

    -   En nøkkelfil for HSM: %NFAST_KMDATA%\local\key_mscapi_ &lt; KeyID &gt;

    -   RMS konfigurasjon av datafilen med SLC fjernet: %NFAST_KMDATA%\local\no_key_tpd_ &lt; KeyID &gt; XML

3.  Hvis du har mer enn én RMS-konfigurasjon-datafiler, må du Gjenta trinn 2 for resten av disse filene.

Nå som SLC er pakket ut slik at det er en nøkkel HSM-basert, er du klar til å pakke og overføre den til Azure RMS.

###### Del 2: Pakke og overføre HSM-nøkkelen til Azure RMS

1.  Bruk fremgangsmåten nedenfor fra den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) delen av det [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md):

    -   **Generer og overfør ditt leier nøkkel – via Internett**: **Forberede leier nøkkelen for overføring**

    -   **Generer og overfør ditt leier nøkkel – via Internett**: **Overføre leier nøkkelen til Azure RMS**

Nå som du har overført HSM-nøkkelen til Azure RMS, er du klar til å importere AD RMS-konfigurasjonsdata, som inneholder en peker til den nylig overført leier nøkkelen.

###### Del 3: Importere konfigurasjonsdataene til Azure RMS

1.  Fremdeles på Internett-tilkoblede arbeidsstasjonen og Windows PowerShell-økten, kopiere over RMS-konfigurasjonsfiler med SLC fjernet (fra den frakoblede arbeidsstasjonen, %NFAST_KMDATA%\local\no_key_tpd_ &lt; KeyID &gt; XML)

2.  Last opp den første filen. Hvis du har mer enn én XML-filen fordi du hadde flere publisering klarerte domener, velger du filen som inneholder de eksporterte klarerte publisering domenet som tilsvarer HSM-tasten du vil bruke i Azure RMS for å beskytte innhold etter migreringen. Bruker du følgende kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    For eksempel: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Når du blir spurt, skriver du inn passordet du angav tidligere, og Bekreft at du vil utføre denne handlingen.

3.  Når kommandoen er fullført, kan du Gjenta trinn 2 for hver gjenstående XML-filen du opprettet ved å eksportere de klarerte domenene for publisering. Men for disse filene, kan du angi **-Active** til **false** Når du kjører Import-kommandoen. For eksempel: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Bruk av [Koble fra AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet til å koble fra Azure RMS-tjenesten:

    ```
    Disconnect-AadrmService
    ```

Du er nå klar til å gå til [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

### <a name="BKMK_Step3Migration"></a>Trinn 3. Aktivere RMS-leier
Instruksjoner for dette trinnet er fullstendig dekket i den [Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md) emnet.

> [!TIP]
> Hvis du har et abonnement på Office 365, kan du aktivere Azure RMS fra Office 365 administrasjonssenteret eller Azure Management-portalen. Vi anbefaler at du bruker Azure Management-portalen fordi du vil bruke denne management-portalen for å fullføre neste trinn.

**Hva skjer hvis Azure RMS-leier allerede er aktivert?** Hvis Azure RMS-tjenesten er allerede aktivert for organisasjonen, kanskje brukere har allerede brukt Azure RMS for å beskytte innhold med et automatisk generert leier nøkkelen (og standardmalene) i stedet for eksisterende nøkler (og maler) fra AD RMS. Dette er sannsynligvis ikke skje på datamaskiner som er godt administrert på intranettet, fordi de vil automatisk bli konfigurert for AD RMS-infrastrukturen. Men det kan skje på datamaskiner i arbeidsgruppen eller datamaskiner som sjelden kobler til intranettet. Dessverre, det er også vanskelig å identifisere disse datamaskinene som er grunnen til at vi anbefaler at du ikke aktiverer tjenesten før du importerer konfigurasjonsdataene fra AD RMS.

Hvis Azure RMS-leier allerede er aktivert, og du kan identifisere disse datamaskinene, må du kontrollere at du kjører CleanUpRMS_RUN_Elevated.cmd-skriptet på disse datamaskinene, som beskrevet i trinn 5. Kjører dette skriptet, tvinger dem til å initialisere brukermiljø, slik at de laster ned den oppdaterte leier nøkkelen og importerte maler.

### <a name="BKMK_Step4Migration"></a>Trinn 4. Konfigurere importerte maler
Fordi du importerte maler har en standard staten **arkivert**, må du endre denne tilstanden for å være **publisert** Hvis du vil at brukerne skal kunne bruke disse malene med Azure RMS.

Hvis malene i AD RMS brukes i tillegg til **ANYONE** gruppen, kan denne gruppen fjernes automatisk når du importerer maler til Azure RMS, må du manuelt legge til den samme gruppen eller brukere og de samme rettighetene til de importerte malene. Den samme gruppen for Azure RMS heter **AllStaff-&lt;tenant_GUID&gt;@&lt;tenant_name&gt;.onmicrosoft.com&gt;**. Denne gruppen kan for eksempel se ut som følgende for Contoso Ltd.: **AllStaff-9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a@contoso.onmicrosoft.com**.

Ser du organisasjonen er automatisk opprettet gruppen Hvis du kopierer en av malene som standard rettigheter policy i Azure portal, og deretter finne den **brukernavn** på den **rettigheter** siden. Du kan imidlertid bruke ikke Azure portalen til å legge til denne gruppen og må i stedet bruke ett av følgende alternativer for Azure RMS PowerShell:

-   Bruk av [eksport-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet til å eksportere malen til en. CSV-fil som du kan redigere for å legge til "AllStaff"-grupper og rettigheter til eksisterende grupper og rettigheter, og deretter bruke den [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet til å importere denne endringen tilbake til Azure RMS.

-   Bruk av [Ny-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell-cmdlet til å definere grupper av "AllStaff" og rettigheter som et objekt for definisjon av rettigheter, og kjøre denne kommandoen på nytt for å definere eksisterende grupper og rettigheter for malen. Legge til disse objektene for definisjon av rettigheter til malene ved hjelp av [Legg til AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) cmdleten.

> [!NOTE]
> Denne "AllStaff" tilsvarende gruppen er ikke nøyaktig det samme som gruppen ANYONE i AD RMS:  "AllStaff"-gruppen inneholder alle brukere i din Azure leier mens gruppen andre inneholder alle godkjente brukere som kan være utenfor organisasjonen.
> 
> På grunn av denne forskjellen mellom de to gruppene må du kanskje også legge til eksterne brukere i tillegg til "AllStaff"-gruppe. Ekstern e-postadresser for grupper støttes ikke.

Maler som du importerer fra AD RMS ser ut og fungerer på samme måte som egendefinerte maler som du kan opprette i Azure Management-portalen. Hvis du vil endre importerte maler kan publiseres slik at brukere kan se dem og velge dem fra programmer eller gjør andre endringer i malene, kan du se [Konfigurere egendefinerte maler for Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

> [!TIP]
> For en enhetlig opplevelse for brukere under overføringsprosessen, gjør du ikke gjøre endringer i de importerte malene enn disse to endringer; og ikke publisere to standardmalene som følger med Azure RMS, eller opprette nye maler på dette tidspunktet. I stedet må vente til overføringsprosessen er fullført og du har ikke tilgjengelig for AD RMS-serverne.

### <a name="BKMK_Step5Migration"></a>Trinn 5. Konfigurere klienter til å bruke RMS Azure
For Windows-klienter:

1.  [Last ned overføringsskriptene](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Disse skriptene Tilbakestiller konfigurasjonen på datamaskiner med Windows, slik at de bruker Azure RMS-tjeneste i stedet for AD RMS.

2.  Følg instruksjonene i skriptet omadressering (Redirect_OnPrem.cmd) til å endre skriptet slik at den peker til den nye Azure RMS leier.

3.  På Windows-datamaskiner ved å kjøre disse skriptene med utvidede rettigheter i brukerens kontekst.

For klienter for mobile enheter og Mac-datamaskiner:

-   Fjerne DNS SRV-oppføringene du opprettet da du distribuert av [AD RMS mobilenhet filtypen](http://technet.microsoft.com/library/dn673574.aspx).

#### Endringer som er gjort ved hjelp av overføringsskriptene
Denne delen dokumenter endringene gjør migrering-skript. Du kan bruke denne informasjonen for bare ment som referanse eller feilsøking, eller hvis du foretrekker å gjøre disse endrer deg selv.

CleanUpRMS_RUN_Elevated.cmd:

-   Slett innholdet i mappene %userprofile%\AppData\Local\Microsoft\DRM og %userprofile%\AppData\Local\Microsoft\MSIPC, inkludert alle undermapper og filer med lange filnavn.

-   Slett innholdet i følgende registernøkler:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Slett følgende registerverdier:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Opprett følgende registerverdier for hver URL-adresse som er angitt som en parameter under hver av følgende plasseringer:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Hver post har en REG_SZ-verdi på **https://OldRMSserverURL/_wmcs/licensing** med dataene i følgende format: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt; YourTenantURL &gt;* har følgende format: **{GUID} av .rms. [Region].aadrm.com**.
    > 
    > For eksempel:  5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Du kan finne denne verdien ved å identifisere den **RightsManagementServiceId** verdi når du kjører den [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdleten for Azure RMS.

### <a name="BKMK_Step6Migration"></a>Trinn 6. Konfigurere IRM-integrering for Exchange Online
Hvis du tidligere har importert TDP fra AD RMS til Exchange Online, må du fjerne denne TDP for å unngå konflikt mellom maler og policyer når du har overført til Azure RMS. Hvis du vil gjøre dette, bruker du [Fjern-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) cmdlet fra Exchange Online.

Hvis du velger en Azure RMS for klientadministrasjon viktige topologien i **Microsoft administrert**:

-   Se den [Exchange Online: IRM-konfigurasjonen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline) delen i den [Konfigurere programmer for Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) emnet. Denne delen inneholder vanlige kommandoer til å kjøre som kobler til Exchange Online-tjenesten, importerer nøkkelen leier fra Azure RMS og aktiverer IRM-funksjonalitet for Exchange Online. Når du har fullført disse trinnene, vil du ha full RMS-funksjonalitet med Exchange Online.

Hvis du velger en Azure RMS for klientadministrasjon viktige topologien i **Kundeadministrerte (BYOK)**:

-   Du vil ha redusert RMS-funksjonalitet med Exchange Online, som beskrevet i den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) delen i den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emnet.

### <a name="BKMK_Step7Migration"></a>Trinn 7. Distribuere RMS-kobling
Hvis du har brukt funksjonen (IRM-Information Rights Management) for Exchange Server eller SharePoint Server med AD RMS, må du først deaktivere IRM på disse serverne og fjerne AD RMS-konfigurasjonen. Deretter distribuere koblingen RMS (Rights Management), som fungerer som et grensesnitt med kommunikasjon (en relay) mellom den lokale servere og Azure RMS.

Til slutt for dette trinnet må Hvis du har importert flere TPDs til Azure RMS som ble brukt til å beskytte e-postmeldinger, du manuelt redigere registeret på Exchange Server-datamaskiner til å omadressere alle TPDs URL-adresser til RMS-koblingen.

> [!NOTE]
> Før du begynner, må du kontrollere de støttede versjonene av de lokale serverne som støtter RMS-koblingen i "lokale servere som støtter Azure RMS" den [Programmer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) delen av den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet.

##### Deaktivere IRM på Exchange-servere og fjerne AD RMS-konfigurasjon

1.  Finn følgende mappe på hver Exchange server, og Slett alle oppføringer i denne mappen: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Blant Exchange-servere, kan du bruke utveksling [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) cmdleten du først deaktivere IRM-funksjoner for meldinger som sendes til interne mottakere:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Deretter kan du bruke cmdleten samme for å deaktivere IRM-funksjonene for meldinger som sendes til eksterne mottakere:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Deretter kan du bruke cmdleten samme for å deaktivere IRM i Microsoft Office Outlook Web App og Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Til slutt kan du bruke cmdleten samme for å fjerne alle hurtigbufrede sertifikater:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  På hver Exchange Server nå tilbakestille IIS, for eksempel ved å kjøre en ledetekst som administrator og å skrive **iisreset**.

##### Deaktivere IRM på SharePoint-serverne og fjerne AD RMS-konfigurasjon

1.  Kontroller at ingen dokumenter er sjekket ut fra RMS-beskyttet biblioteker. Hvis det er, vil de være utilgjengelige på slutten av denne fremgangsmåten.

2.  På SharePoint Sentraladministrasjon-området, i den **Hurtigstart** -delen, klikker du **Sikkerhet**.

3.  På den **Sikkerhet** side i den **opplysning Policy** -delen, klikker du **konfigurere IRM (information rights management)**.

4.  På den **Information Rights Management** side i den **Information Rights Management** delen velger **ikke bruke IRM på denne serveren**, deretter **OK**.

5.  På hver av SharePoint Server-datamaskiner, kan du slette innholdet i mappen-\ProgramData\Microsoft\MSIPC\Server\*&lt; SID for kontoen som kjører SharePoint Server &gt;*.

##### Installere og konfigurere RMS-kobling

-   Bruk instruksjonene i den [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md) emnet.

##### For bare Exchange og flere TPDs: Redigere registret

-   På hver Exchange Server manuelt legge til følgende registernøkler for hver ekstra TPD som du har importert, vil omadressere TPD URL-adresser til RMS-koblingen. Disse registeroppføringene er spesifikke for migrering og ikke er lagt til av verktøy for konfigurasjon av server for Microsoft RMS-kobling.

    Når du gjør disse endringene i registret, kan du bruke følgende instruksjoner:

    -   Erstatte *ConnectorFQDN* med navnet du definerte i DNS for koblingen. For eksempel **rmsconnector.contoso.com**.

    -   Bruk HTTP eller HTTPS-prefikset for URL-kobling, avhengig av om du har konfigurert koblingen hvis du vil bruke HTTP- eller HTTPS til å kommunisere med de lokale serverne.

    **For Exchange-2013:**

    |Registerbane|Type|Verdi|Data|
    |----------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|RMS intranett lisensiering URL-https://&lt;AD &gt;/_wmcs/lisensiering|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|RMS ekstranett Licensing-URL-https://&lt;AD &gt;/_wmcs/lisensiering|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/Licensing<br />-   https://&lt;connectorFQDN&gt;/_wmcs/Licensing|
    **For Exchange Server 2010:**

    |Registerbane|Type|Verdi|Data|
    |----------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|RMS intranett lisensiering URL-https://&lt;AD &gt;/_wmcs/lisensiering|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|RMS ekstranett Licensing-URL-https://&lt;AD &gt;/_wmcs/lisensiering|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|

Når du har fullført denne fremgangsmåten, må du lese den **Neste trinn** i-delen i [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md) emnet.

### <a name="BKMK_Step8Migration"></a>Trinn 8. Dekommisjonering av AD RMS
Valgfritt: Fjerne Service Connection Point (SCP) fra Active Directory til å hindre at datamaskiner bli kjent med din lokale Rights Management-infrastruktur. Dette er valgfritt på grunn av omadressering, som du har konfigurert i registret (for eksempel ved å kjøre skriptet overføring). Hvis du vil fjerne tilkoblingspunktet for tjeneste, kan du bruke verktøyet AD SCP journal fra den [Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479).

Overvåke AD RMS-servere for aktiviteten, for eksempel ved å kontrollere den [forespørsler i rapporten systemets tilstand](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx),  [ServiceRequest tabell](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) eller [kontroll av brukertilgang til beskyttet innhold](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Når du har bekreftet at RMS-klienter ikke lenger kommuniserer med disse serverne, og at klienter er fullført ved hjelp av Azure RMS, kan du fjerne rollen for AD RMS-serveren fra denne serveren. Hvis du bruker dedikerte servere, vil du kanskje foretrekke mer trinn av første slår av serverne for en viss tid for å være sikker på at det er ingen rapporterte problemer som kanskje krever omstart av disse serverne for å sikre kontinuitet i tjenesten selv om du undersøke hvorfor klienter ikke bruker Azure RMS.

Etter dekommisjonering AD RMS-servere, vil du kanskje ta muligheten til å se gjennom malene i Azure Management-portalen og konsolidere dem slik at brukerne har færre å velge mellom, konfigurere dem på nytt eller med å legge til nye maler. Dette vil også være lurt å publisere standardmalene. Hvis du vil ha mer informasjon, se [Konfigurere egendefinerte maler for Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

### <a name="BKMK_Step9Migration"></a>Trinn 9. Nye nøkler Azure RMS leier nøkkelen
Dette trinnet er nødvendig når overføringen er fullført hvis AD RMS-distribusjonen ble bruker RMS kryptografiske modus 1, fordi ny inntasting oppretter en ny nøkkel for klientadministrasjon som bruker RMS kryptografiske modus 2. Ved hjelp av Azure RMS med kryptografiske modus 1 støttes bare under overføringsprosessen.

Dette trinnet er valgfritt, men anbefales når overføringen er fullført, selv om du kjørte i RMS kryptografiske modus 2, fordi det bidrar til å sikre Azure RMS leier nøkkelen fra potensielle sikkerhetsovertredelser til AD RMS-nøkkelen. Når du på nytt tasten Azure RMS leier nøkkelen (også kjent som "rullende nøkkelen"), en ny nøkkel opprettes, og den opprinnelige nøkkelen er arkivert. Imidlertid flytte fra én tast til en annen ikke skje umiddelbart, men over et par uker, ikke Vent til du har mistanke om brudd på den opprinnelige tasten men tasten RMS leier nøkkelen på nytt så snart overføringen er fullført.

Taste Azure RMS leier nøkkelen på nytt:

-   Hvis produktnøkkelen RMS leier administreres av Microsoft: Hvis du vil ringe Microsofts kundestøttetjeneste (CSS) og bevise at du er leier RMS-administratoren.

-   Hvis produktnøkkelen RMS leier administreres av deg (BYOK): Gjenta denne fremgangsmåten for BYOK for å generere og opprette en ny nøkkel via Internett eller personlig.

Hvis du vil ha mer informasjon om administrasjon av RMS leier nøkkelen, se [Operasjoner leietakeradministrasjon nøkkelen Azure Rights Management](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md).

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

