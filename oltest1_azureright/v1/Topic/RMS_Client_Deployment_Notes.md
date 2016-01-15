---
description: na
keywords: na
title: RMS Client Deployment Notes
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
---
# RMS-klient distribusjon notater
Tjenesten for Rights Management-klienten (RMS client) versjon 2 er også kjent som MSIPC-klient. Det er programvare for Windows-datamaskiner som kommuniserer med Microsoft Rights Management services på lokaler eller i skyen for å beskytte tilgang til og bruk av informasjon som den flyter gjennom programmer og enheter, innenfor grensene av organisasjonen eller utenfor de administrerte grenser. I tillegg til levering med den [Rights Management deling av programmer for Windows](https://technet.microsoft.com/library/dn919648.aspx), RMS-klienten er tilgjengelig [som en valgfri nedlasting](http://www.microsoft.com/download/details.aspx?id=38396) som kan, med bekreftelse og godkjenning av lisensavtalen, fritt distribueres med tredjeparts programvare slik at klienter kan beskytte og forbruker innhold som er beskyttet av Rights Management services.

Dette emnet inneholder følgende deler:

-   [Distribuerte RMS-klienten](#BKMK_RedistributeInstaller)

-   [Installere RMS-klienten](#BKMK_InstallClient)

-   [Spørsmål og svar om RMS-klienten](#BKMK_QA)

-   [RMS-klientinnstillinger](#BKMK_Settings)

-   [AD RMS: Hvis du begrenser RMS-klienten til å bruke klarerte AD RMS-servere](#BKMK_UsingTrustedServers)

-   [RMS-Service Discovery-konfigurasjon](#BKMK_ServiceDiscovery)

## <a name="BKMK_RedistributeInstaller"></a>Distribuerte RMS-klienten
RMS-klienten kan fritt distribuert og sammen med andre programmer og IT-løsninger. Hvis du er en utvikler eller løsningsforhandlere og ønsker å videreformidle RMS-klienten, har du to alternativer:

-   Anbefalt: Bygg inn RMS-klienten installasjonsprogrammet i din installasjon av programmer og kjøre den i stille modus (den **/quiet** bryteren, som beskrevet i neste del).

-   Kontroller RMS-klienten en forutsetning for programmet. Med dette alternativet må du kanskje gi brukere ytterligere instrukser for dem å skaffe, installere og oppdatere sine datamaskiner med klienten, før de kan bruke programmet.

## <a name="BKMK_InstallClient"></a>Installere RMS-klienten
RMS-klienten ligger i en kjørbar installeringsfil som kalles **setup_msipc_***&lt; arch &gt;***.exe**, der *&lt; arch &gt;* er enten **x86** (for klientmaskiner på 32-biters) eller **x64** (for klientmaskiner på 64-biters). 64-bit (x 64) installasjonspakken installeres både en 32-biters runtime kjørbare for kompatibilitet med 32-biters programmer som kjører på en 64-biters operativsystem installasjon, samt en 64-biters runtime kjørbar som støtter opprinnelig 64-biters programmer. Installasjonsprogrammet for 32-biters (x 86) kan ikke kjøres på en 64-biters Windows-installasjon.

> [!NOTE]
> Du trenger forhøyede rettigheter til å installere RMS-klienten, for eksempel et medlem av gruppen Administratorer på den lokale datamaskinen.

Du kan installere RMS-klienten ved hjelp av en av følgende installasjonsmetoder:

-   **Stille modus.** Ved hjelp av den **/quiet** bytte som en del av kommandolinjealternativene, kan du stille installere RMS-klienten på datamaskiner. Følgende eksempel viser en installasjon i stille modus for RMS-klienten på en klientdatamaskin for 64-biters:

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **Interaktiv modus.** Du kan eventuelt installere RMS-klienten ved hjelp av GUI-basert installasjonsprogram som tilbys av veiviseren for installasjon av RMS-klienten. Hvis du vil gjøre dette, dobbeltklikker du installasjonspakken RMS-klienten (**setup_msipc_***&lt; arch &gt;***.exe**) i mappen som den ble overført eller lastet ned på den lokale datamaskinen.

## <a name="BKMK_QA"></a>Spørsmål og svar om RMS-klienten
Følgende del inneholder vanlige spørsmål om RMS-klienten og svarene på dem.

### Hvilke operativsystemer støtter RMS-klienten?
RMS-klienten støttes med følgende operativsystemer:

|Windows Server-operativsystem|Windows-klient-operativsystem|
|---------------------------------|---------------------------------|
|Windows Server 2012 R2|8.1 for Windows|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 med minimum SP1|
|Windows Server 2008 (bare AD RMS)|Windows Vista med minimum av SP2 (bare AD RMS)|

### Hvilke prosessorer eller plattformer støtte RMS-klienten?
RMS-klienten støttes på x 86 og x 64 databehandling plattformer.

### Der er RMS-klienten installert?
RMS-klienten er installert som standard i %ProgramFiles%\Active Directory Rights Management Services Client 2. &lt; versjonsnummer &gt;.

### Hvilke filer er knyttet til RMS-klientprogramvaren?
Følgende filer installeres som en del av RMS-klientprogramvaren:

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

I tillegg til disse filene installerer RMS-klienten også støttefiler for multilingual user interface (MUI) i 44 språk. Kjør installasjonen av RMS-klienten for å kontrollere språkene som støttes, og når installasjonen er fullført, kan du se gjennom innholdet i mappene flerspråklig støtte under standardbanen.

### Er RMS-klienten som er inkludert som standard når jeg installere et operativsystem som støttes?
Nr. Denne versjonen av RMS-klienten som leveres som en valgfri nedlasting som kan installeres separat på datamaskiner som kjører støttede versjoner av Microsoft Windows-operativsystemet.

### RMS-klienten oppdateres automatisk av Microsoft Update?
Hvis du har installert denne RMS-klienten ved hjelp av alternativet for stille installasjon, arver gjeldende innstillinger for Microsoft Update i RMS-klienten. Hvis du installerte RMS-klienten ved hjelp av installasjonsprogrammet for GUI-basert, veiviseren for installasjon av RMS-klienten ber deg om å aktivere Microsoft Update.

## <a name="BKMK_Settings"></a>RMS-klientinnstillinger
Følgende del inneholder for innstillingsinformasjon om RMS-klienten. Denne informasjonen kan være nyttig hvis du har problemer med programmer eller tjenester som bruker RMS-klienten.

> [!NOTE]
> Noen innstillinger avhenger av om RMS-enlightened-programmet kjører som en modus klientprogram (for eksempel Microsoft Word og Outlook eller RMS deling program), eller server modus program (for eksempel SharePoint og Exchange).  I følgende tabeller, identifiseres disse innstillingene som **klientmodus** og **Server-modus**, henholdsvis.

### Hvor RMS-klienten butikkene lisenser på klientdatamaskiner
RMS-klienten lagrer lisenser på den lokale disken og bufrer også informasjon i Windows-registret.

|Beskrivelse|Klienten modus baner|Server modus baner|
|---------------|------------------------|----------------------|
|Lisens lagerlokasjon|%localappdata%\Microsoft\MSIPC|%ALLUSERSPROFILE%\Microsoft\MSIPC\Server\*&lt; SID &gt;*\|
|Mal Lagre plassering|%localappdata%\Microsoft\MSIPC\Templates|%ALLUSERSPROFILE%\Microsoft\MSIPC\Server\Templates\*&lt; SID &gt;*\|
|Sted i registret|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local innstillinger<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*&lt; SID &gt;*|
> [!NOTE]
> *&lt; SID &gt;* er sikker ID (SID) for kontoen som kjører serverprogrammet. Hvis applikasjonen kjører under den innebygde Network Service-kontoen, for eksempel erstatte *&lt; SID &gt;* med verdien av den velkjente SID for kontoen (S-1-5-20).

### Windows-registerinnstillingene for RMS-klienten
Du kan bruke Windows-registernøklene til å angi eller endre noen konfigurasjoner for RMS-klienten. Som administrator for RMS-enlightened programmer som kommuniserer med AD RMS-servere du kan for eksempel oppdatere enterprise service plasseringen (overstyring av AD RMS-serveren som er valgt for publisering) avhengig av klientdatamaskinens gjeldende plassering i Active Directory-topologi. Eller du vil aktivere sporing av RMS på klientdatamaskinen, for å feilsøke et problem med et program for RMS-enlightened. Bruk tabellen nedenfor til å identifisere registerinnstillingene som du kan endre for RMS-klienten.

|Oppgave|Innstillinger|
|-----------|-----------------|
|AD RMS: Oppdatere plasseringen for enterprise-service for en klientdatamaskin|Oppdater følgende registernøkler:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />    REG_SZ: standard<br />    **Verdi:**&lt; http eller https &gt; :// *RMS_Cluster_Name*/_wmcs/sertifisering<br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />    REG_SZ: standard<br />    **Verdi:** &lt; http eller https &gt; :// *RMS_Cluster_Name*/_wmcs/Licensing|
|Slik aktiverer og deaktiverer sporing|Oppdater følgende registernøkkel:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />    REG_DWORD: Spor<br />    **Verdi:** 1 for å aktivere sporing, 0 for å deaktivere sporing (standard)|
|Endre frekvensen i dager for å oppdatere maler|Følgende registerverdier angir hvor ofte oppdateres maler på brukerens datamaskin Hvis verdien for TemplateUpdateFrequencyInSeconds ikke er angitt.  Hvis ingen av disse verdiene er angitt, er standard Oppdateringsintervall for programmer som bruker RMS-klienten (versjon 1.0.1784.0) til å laste ned maler 1 dag. Versjoner før dette har en standardverdi på hver 7 dager.<br /><br />**Klientmodus:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Verdi:** Et heltall som angir antall dager (minimum 1) mellom nedlastinger.<br /><br />**Server-modus:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt; SID &gt;*<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Verdi:** Et heltall som angir antall dager (minimum 1) mellom nedlastinger.|
|Endre hyppigheten i sekunder for å oppdatere maler **Important:** Hvis dette er angitt, ignoreres verdien du vil oppdatere maler i dager. Angi en eller den andre, ikke begge.|Følgende registerverdier angir hvor ofte maler vil bli oppdatert på brukerens datamaskin. Hvis denne verdien eller verdien du vil endre frekvensen i dager (TemplateUpdateFrequency) ikke er angitt, er standard Oppdateringsintervall for programmer som bruker RMS-klienten (versjon 1.0.1784.0) til å laste ned maler 1 dag. Versjoner før dette har en standardverdi på hver 7 dager.<br /><br />**Klientmodus:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Verdi:** Et heltall som angir antall sekunder (minimum 1) mellom nedlastinger.<br /><br />**Server-modus:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt; SID &gt;*<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Verdi:** Et heltall som angir antall sekunder (minimum 1) mellom nedlastinger.|
|AD RMS: Laste ned maler umiddelbart ved neste forespørsel publisering|Under testingen og evalueringer vil du kanskje RMS-klienten til å laste ned maler så snart som mulig. Hvis du vil gjøre dette, fjerner følgende registernøkkel og RMS-klienten vil laste ned maler umiddelbart ved neste forespørsel publisering i stedet venter tiden som er angitt av registerinnstilling for TemplateUpdateFrequency:<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\ &lt; servernavn &gt; \Template **Note:** &lt; servernavn &gt; kan ha ekstern (en corprights.contoso.com) og URL-adresser til intern (corprights) og derfor to ulike oppføringer.|
|AD RMS: Aktivere støtte for medlemmer av organisasjonsnettverk godkjenning|Hvis datamaskinen RMS-klienten kobler seg til en AD RMS-klyngen ved hjelp av en forent klarering, må du konfigurere den federation hjemmeområde.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_SZ: FederationHomeRealm<br />    **Verdi:** Verdien til registernøkkelen er uniform resource identifier (URI) for federation service (for eksempel "https://fs-01.contoso.com").|
|AD RMS: Støtte for sammenslutningsservere partner som krever skjemabasert godkjenning for brukerinndata|Som standard RMS-klienten, opererer i stille modus og brukerinndata kreves ikke. Partner sammenslutningsservere, imidlertid kan være konfigurert til å kreve brukerinndata slik som ved hjelp av skjemabasert godkjenning. I dette tilfellet må du konfigurere RMS-klienten ignorerer stille modus, slik at skjemaet samlede godkjenning vises i et leservindu, og brukeren er forfremmet til godkjenning.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_DWORD: EnableBrowser **Note:** Hvis federation-serveren er konfigurert til å bruke skjemabasert godkjenning, kreves denne nøkkelen. Hvis federation-serveren er konfigurert for å bruke integrert Windows-godkjenning, er det ikke nødvendig å bruke denne nøkkelen.|
|AD RMS: Blokker ILS for forbruk av tjeneste|RMS-klienten gjør at tid innhold som er beskyttet av ILS-tjenesten som standard, men kan du konfigurere klienten for å blokkere denne tjenesten ved å angi følgende registernøkkel. Hvis denne registernøkkelen er satt til å blokkere ILS-tjenesten, forsøk på å åpne og bruke innhold som er beskyttet av ILS-tjenesten returnerer følgende feil:<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: **DisablePassportCertification**<br />    **Verdi:** 1 for å blokkere ILS forbruk, 0 for å tillate ILS-forbruk (standard)|

### Behandle malen distribusjon for RMS-klienten
Maler gjør det enkelt for brukere og administratorer raskt ta i bruk IRM-beskyttelse og RMS-klienten laster ned automatisk maler fra RMS-serverne eller service Hvis du legger til malene i følgende mappe, RMS-klienten ikke vil laste ned maler fra standardplasseringen og laste ned maler som du har satt inn i denne mappen i stedet. RMS-klienten kan fortsette å laste ned maler fra andre tilgjengelige RMS-servere.

**Klientmodus:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Server-modus:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\*&lt; SID &gt;*

Når du bruker denne mappen, er det ingen spesielle navnekonvensjonen kreves bortsett fra at malene skal utstedes av RMS-serveren eller tjenesten og de må ha filtypen XML. Contoso-Confidential.xml eller Contoso-ReadOnly.xml er for eksempel gyldige navn.

## <a name="BKMK_UsingTrustedServers"></a>AD RMS: Hvis du begrenser RMS-klienten til å bruke klarerte AD RMS-servere
RMS-klienten kan være begrenset til å bruke bare bestemte klarerte AD RMS-servere ved å gjøre følgende endringer i Windows-registret på lokale datamaskiner.

**Hvis du vil aktivere begrense RMS klarerte klienten bare å bruke AD RMS-servere**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD: AllowTrustedServersOnly

    **Verdi:** Hvis det er angitt en annen verdi enn null, klareres RMS-klienten bare de angitte serverne som er konfigurert i listen over TrustedServers og Azure Rights Management-tjenesten.

**Legge til medlemmer i listen over klarerte AD RMS-servere**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ: *&lt; URL_or_HostName &gt;*

    **Verdi:** Strengverdier som er lagt til i denne plassering av registret kan være enten navneformat for DNS-domene (for eksempel **adrms.contoso.com**) eller fullstendig URL-adresser til klarerte AD RMS-servere (for eksempel **https://adrms.contoso.com**). Hvis en angitt URL-adresse som begynner med **https://**,  RMS-klienten vil bruke SSL eller TLS til å kontakte den angitte AD RMS-serveren.

## <a name="BKMK_ServiceDiscovery"></a>RMS-Service Discovery-konfigurasjon
RMS service discovery kan kontrollere hvilke RMS-server eller tjeneste til å kommunisere med før du beskyttet innhold RMS-klienten. Discovery Service kan også skje når RMS-klienten bruker beskyttet innhold, men dette er mindre sannsynlig til å skje fordi policyen som er knyttet til innholdet inneholder foretrukket RMS-server eller tjeneste, og bare hvis det er mislykket klienten deretter kjører service Discovery-konfigurasjon.

Service discovery søker først etter en lokale versjon av Rights Management (AD RMS). Hvis det er vellykket, ser service discovery automatisk for sky-versjonen av Rights Management (Azure RMS).

Hvis du vil utføre service Discovery-konfigurasjon for en distribusjon på lokaler, kontrollerer RMS-klienten følgende:

1.  Windows-registret på den lokale datamaskinen: Hvis service discovery-innstillingene er konfigurert i registret, blir disse innstillingene, forsøkes først.  Disse innstillingene er ikke konfigurert i registret som standard.

2.  Active Directory-domenetjenester: En datamaskin som er tilknyttet et domene spørringer Active Directory for et service connection point (SCP). Hvis en SCP er registrert, returnerte URL-adressen til RMS-serveren til RMS-klienten til å bruke.

### AD RMS: Aktivere inkluderinger for serversiden Service Discovery-konfigurasjon ved hjelp av Active Directory
Hvis du har tilstrekkelige rettigheter (Enterprise Admins og lokal administrator for AD RMS-serveren), kan du automatisk registrere et service connection point (SCP) når du installerer AD RMS-rotserver for klynge. Hvis det allerede finnes en SCP i skogen, må du først slette eksisterende SCP før du kan registrere en ny.

Du kan registrere og slette en SCP etter AD RMS er installert ved hjelp av følgende fremgangsmåte. Før du starter, må du kontrollere at kontoen har de nødvendige rettighetene (Enterprise Admins og lokal administrator for AD RMS-serveren).

##### Å aktivere AD RMS service Discovery-konfigurasjon ved å registrere en SCP i Active Directory

1.  Åpne Active Directory Management Services-konsollen på AD RMS-serveren:

    -   Hvis du bruker Windows Server 2008 R2 eller Windows Server 2008, klikker du **Start**, klikker du **Administrative verktøy**, og klikk deretter **Active Directory Rights Management Services**.

    -   Hvis du bruker Windows Server 2012 R2 eller Windows Server 2012 i Server Manager, klikker du **Verktøy**, og klikk deretter **Active Directory Rights Management Services**.

2.  Høyreklikk AD RMS-klyngen i AD RMS-konsollen, og klikk deretter **Egenskaper**.

3.  Klikk på **SCP** i kategorien.

4.  Velg den **Endre SCP** merket.

5.  Velg den **Angi SCP til gjeldende sertifisering klyngen** alternativet, og klikk deretter **OK**.

### Aktivering av Søk etter webtjenesten på klientsiden ved hjelp av Windows-registret
Som et alternativ til å bruke en SCP eller der en SCP ikke finnes, kan du konfigurere registret på klienten slik at RMS-klienten kan finne en AD RMS-server.

##### Aktivere klientsiden AD RMS service Discovery-konfigurasjon ved hjelp av Windows-registret

1.  Åpne Registerredigering, Regedit.exe:

    -   På klientmaskinen, i vinduet Kjør skriver du inn **regedit**, og trykk deretter ENTER for å åpne Registerredigering.

2.  I Registerredigering, gå til **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!IMPORTANT]
    > Hvis du kjører en 32-biters program på en 64-biters datamaskin, blir banen som følger: 
    > **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  Hvis du vil opprette undernøkkelen ServiceLocation, høyreklikker du **MSIPC**, velger du **Ny**, klikker du **nøkkel**, og skriv deretter inn **ServiceLocation**.

4.  Hvis du vil opprette undernøkkelen EnterpriseCertification, høyreklikker du **ServiceLocation**, velger du **Ny**, klikker du **nøkkel**, og skriv deretter inn **EnterpriseCertification**.

5.  Hvis du vil angi URL-adressen for enterprise-sertifisering, dobbeltklikker du på **(standard)** verdi under den **EnterpriseCertification** undernøkkelen, og når den **Rediger streng** dialogboks vises, for **Verdidata**, type &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Certification, og klikk deretter **OK**.

6.  Hvis du vil opprette undernøkkelen EnterprisePublishing, høyreklikker du **ServiceLocation**, velger du **Ny**, klikker du **nøkkel**, og skriv deretter inn EnterprisePublishing.

7.  Hvis du vil angi enterprise publiserer URL-adresse, dobbeltklikker du **(standard)** , under den **EnterprisePublishing** undernøkkel, og når den **Rediger streng** vises, skriver du inn for **Verdidata** følgende &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Licensing, og klikk deretter **OK**.

8.  Lukk Registerredigering.

Hvis RMS-klienten ikke kan finne en SCP ved å spørre Active Directory, og det er ikke angitt i registret, mislykkes discovery servicehenvendelser for AD RMS.

### Omdirigere Licensing servertrafikk
I noen tilfeller må du kanskje omdirigere trafikk under service Discovery-konfigurasjon, for eksempel når to organisasjoner er slått sammen og den gamle lisensierende serveren i en organisasjon er utgått og klienter må bli omadressert til en ny lisensserver. Eller du migrere fra AD RMS til Azure RMS. Bruk følgende fremgangsmåte for å aktivere lisensiering omadressering.

##### Slik aktiverer du RMS lisensiering omadressering ved hjelp av Windows-registret

1.  Åpne Registerredigering, Regedit.exe:

    -   På klientmaskinen, i vinduet Kjør skriver du inn **regedit**, og trykk deretter ENTER for å åpne Registerredigering.

2.  I Registerredigering, går du til ett av følgende:

    -   For 64-biters versjonen av Office på x 64 plattform: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   For 32-biters versjonen av Office på x 64 plattform: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Opprett en undernøkkel med LicensingRedirection ved å høyreklikke **Servicelocation**, velger du **Ny**, klikker du **nøkkel**, og skriv deretter inn **LicensingRedirection**.

4.  Hvis du vil angi lisensiering omadressering, høyreklikker du **LicensingRedirection** undernøkkelen, velg **Ny**, og velg deretter **Strengverdi**.  For **navnet**, angi tidligere server licensing URL-adressen og **verdien** angir den nye serveren lisensiering URL-adressen.

    For eksempel vil omadressere til en i Fabrikam.com-lisensiering fra en server på Contoso.com, kan du angi følgende verdier:

    **Navn:** `https://contoso.com/_wmcs/licensing`

    **Verdi:** `https://fabrikam.com/_wmcs/licensing`

    > [!NOTE]
    > Hvis den gamle lisensierende serveren har både intranett og ekstranett URL-adresser angitt deretter et nytt navn og verditilordning må angis for begge disse URL-adressene under nøkkelen LicensingRedirection.

5.  Gjenta det forrige trinnet for alle servere som skal omadresseres.

6.  Lukk Registerredigering.

