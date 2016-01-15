---
description: na
keywords: na
title: Deploying the Azure Rights Management Connector
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
---
# Distribusjon av Azure Rights Management-kobling
Bruk denne informasjonen til å lære mer om Microsoft Rights Management (RMS)-kobling, og hvordan du kan bruke den til å gi informasjon om beskyttelse med eksisterende lokale installasjoner som bruker Microsoft Exchange Server, Microsoft SharePoint Server eller servere som kjører Windows Server og bruke filen klassifisering infrastruktur (FCI)-funksjonen i File Server Resource Manager.

> [!TIP]
> For et høyt nivå eksempelscenario med skjermbilder, kan du se den [Automatisk beskyttelse av filer på filservere som kjører Windows Server og filen klassifisering infrastruktur](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Example_FCI) delen i den [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emnet.

## <a name="OverviewConnector"></a>Oversikt over Microsoft Rights Management-kobling
Microsoft Rights Management (RMS)-kobling kan du raskt aktivere eksisterende lokale servere å bruke Information Rights Management (IRM) funksjonaliteten til sky-baserte Microsoft Rights Management-tjenesten (Azure RMS). Med denne funksjonen, IT og brukere enkelt kan beskytte dokumenter og bilder både i organisasjonen og ytre, uten å måtte installere ekstra infrastruktur eller opprette klareringsforhold med andre organisasjoner. Selv om noen av dine brukere kobler til elektroniske tjenester, i et scenario med hybrid, kan du bruke denne koblingen. Enkelte brukeres postbokser bruker Exchange Server, for eksempel noen brukernes postbokser Bruk Exchange Online. Når du installerer RMS-koblingen, alle brukere kan beskytte og bruke e-postmeldinger og vedlegg ved hjelp av Azure RMS, og informasjon om beskyttelse fungerer sømløst mellom to distribusjon-konfigurasjoner.

RMS-koblingen er en liten plass å installere lokale, på servere som kjører Windows Server 2012 R2, Windows Server 2012 eller Windows Server 2008 R2. I tillegg kjører koblingen på fysiske datamaskiner, kan du også kjøre den på virtuelle maskiner, inkludert Azure IaaS VMs. Når du installerer og konfigurerer koblingen, fungerer den som en kommunikasjon grensesnitt (en relay) mellom de lokale serverne og cloud-tjeneste.

Hvis du administrerer din egen nøkkel for leieradministrasjon for Azure RMS (Plasser du eier nøkkelen eller BYOK scenario), RMS-koblingen og de lokale serverne som bruker den ikke tilgang hardware sikkerhetsmodul (HSM) som inneholder nøkkelen leier. Dette er fordi alle kryptografiske operasjoner som bruker nøkkelen leier utføres i Azure RMS, og ikke lokale.

![](../Image/RMS_connector.png)

RMS-koblingen støtter følgende lokale servere: Exchange Server, SharePoint Server og servere som kjører Windows Server og bruke filen klassifisering infrastruktur til å klassifisere og bruke policyer på Office-dokumenter i en mappe. Hvis du vil beskytte alle filtyper ved å bruke filen klassifisering, må du ikke bruke RMS-koblingen, men i stedet bruke den [RMS beskyttelse cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> For støttede versjoner av disse lokale servere, se "lokale servere som støtter Azure RMS" i den [Programmer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) delen av den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet.

Bruk de følgende delene som hjelper deg med å planlegge, installere og konfigurere RMS-koblingen. Deretter må du gjøre noen etter installasjonskonfigurasjon slik at serverne dine kan bruke koblingen.

-   [Prerequisites for the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_Prereqs)

-   **Trinn 1:**  [Installing the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_InstallingConnector)

-   **Trinn 2:**  [Entering credentials](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#EnteringCredentials)

-   **Trinn 3:**  [Authorizing servers to use the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#AuthorizingServers)

-   **Trinn 4:**  [Configuring load balancing and high availability](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#ConfiguringConnector)

-   Valgfritt: [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS)

-   Valgfritt: [Configuring the RMS connector for a web proxy server](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringWebProxy)

-   Valgfritt: [Installing the RMS connector administration tool on administrative computers](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_InstallingStandaloneTool)

-   **Trinn 5:**  [Configuring servers to use the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#ConfiguringServers)

    -   [Configuring an Exchange server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ExchangeServer)

    -   [Configuring a SharePoint server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringSharePoint)

    -   [Configuring a file server for File Classification Infrastructure to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_FileServer)

-   [Next steps](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_NextSteps)

## <a name="BKMK_Prereqs"></a>Forutsetninger for RMS-kobling
Før du installerer RMS-kobling, må du kontrollere at følgende krav er på plass.

|Krav|Hvis du vil ha mer informasjon|
|--------|----------------------------------|
|Tjenesten RMS (Rights Management) er aktivert|[Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md)|
|Directory-synkronisering mellom Active Directory-skoger og Azure Active Directory|Etter RMS er aktivert, vil Azure Active Directory må være konfigurert for å arbeide med brukere og grupper i Active Directory-databasen. **Important:** Du må utføre dette trinnet for directory-synkronisering for RMS-kobling skal fungere, selv for en test-nettverket. Men du kan bruke Office 365 og Azure Active Directory ved hjelp av brukerkontoer du oppretter manuelt i Azure Active Directory, krever denne koblingen at kontoene i Azure Active Directory, er synkronisert med Active Directory Domain Services; Manuell passordsynkronisering er ikke nok.<br />Hvis du vil ha mer informasjon, kan du se følgende ressurser:<br /><br />-   [Instruksjoner for konfigurering av Azure AD-leier](http://technet.microsoft.com/library/hh967611.aspx)<br />-   [Instruksjoner for å aktivere katalogsynkronisering med AAD ved hjelp av DirSync](http://technet.microsoft.com/library/hh967642.aspx)|
|Valgfritt men anbefales:<br /><br />-   Aktiver federation mellom den lokale Active Directory og Azure Active Directory|Du kan aktivere federering av identitet mellom den lokale katalogen og Azure Active Directory. Denne konfigurasjonen gir en bedre brukeropplevelse ved å bruke enkel pålogging til RMS-tjenesten. Uten enkel pålogging, blir brukere bedt om legitimasjon før de kan bruke rettighetsbeskyttet innhold.<br /><br />For instruksjoner for å konfigurere federation ved hjelp av Active Directory Federation Services (AD FS) mellom Active Directory Domain Services og Azure Active Directory, kan du se [Sjekkliste: Bruk AD FS å implementere og administrere enkel pålogging](http://technet.microsoft.com/library/jj205462.aspx) i Windows Server-biblioteket.|
|Minst to medlemsdatamaskiner vil installere RMS-koblingen på:<br /><br /><ul><li>En 64-biters fysisk eller virtuell datamaskin som kjører ett av følgende operativsystemer:<br /><br /><ul><li>Windows Server 2012 R2</li><li>Windows Server 2012</li><li>Windows Server 2008 R2</li></ul></li><li>Minst 1 GB RAM</li><li>Minimum 64 GB ledig plass på harddisken</li><li>Minst én nettverksgrensesnitt</li><li>Tilgang til Internett via en brannmur (eller webproxy) som ikke krever godkjenning</li><li>Må være i en skog eller et domene som klarerer andre skoger i organisasjonen som inneholder installasjoner Exchange eller SharePoint-servere som du vil bruke sammen med RMS-kobling</li></ul>|Du må installere RMS-koblingen på minst to datamaskiner for feiltoleranse og høy tilgjengelighet. **Tip:** Hvis du bruker Outlook Web Access eller mobile enheter som bruker Exchange ActiveSync IRM, og det er svært viktig at du har tilgang til e-postmeldinger og vedlegg som er beskyttet av Azure RMS, anbefaler vi at du distribuerer en belastningsfordelt gruppe tilkoblingsservere for å sikre høy tilgjengelighet.<br />Du trenger ikke dedikerte servere å kjøre koblingen, men du må installere den på en annen datamaskin fra servere som bruker koblingen. **Important:** Installer ikke koblingen på en datamaskin som kjører Exchange Server, SharePoint-Server eller en filserver som er konfigurert for filen klassifisering infrastruktur Hvis du vil bruke funksjonaliteten fra disse tjenestene med Azure RMS. Dessuten Installer ikke denne koblingen på en domenekontroller.|

## <a name="BKMK_InstallingConnector"></a>Installere RMS-kobling
Etter at du har bekreftet forutsetningene i delen ovenfor, kan du bruke følgende instruksjoner for å installere RMS-koblingen:

1.  Identifisere datamaskiner (minimum to) som kjører RMS-koblingen. De må oppfylle minimum spesifikasjonen som er oppført i delen ovenfor.

    > [!NOTE]
    > Du vil installere en enkelt RMS-kontakt (som består av flere servere for høy tilgjengelighet) per leier (Office 365 leier eller Azure AD leier). I motsetning til Active Directory-RMS har du ikke å installere en RMS-koblingen i hver skog.

2.  Last ned kildefilene for RMS-kontakten fra den [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=314106).

    Hvis du vil installere RMS-kobling, laster du ned RMSConnectorSetup.exe.

    I tillegg:

    -   Hvis du senere vil konfigurere kontakten fra en 32-biters datamaskin, kan du også laste ned RMSConnectorAdminToolSetup_x86.exe.

    -   Hvis du vil bruke verktøyet for konfigurasjon av server for RMS-kobling, for å automatisere konfigurasjonen av registerinnstillingene du lokale servere, også laste ned GenConnectorConfig.ps1.

3.  På datamaskinen du vil installere RMS-koblingen, kan du kjøre **RMSConnectorSetup.exe** med administratorrettigheter.

4.  På velkomstsiden for Microsoft Rights Management Connector installasjon-siden, velger du **installere Microsoft Rights Management-kontakten på datamaskinen**, og klikk deretter **neste**.

5.  Les og godta lisensvilkårene for bruk av RMS-koblingen, og klikk deretter **neste**.

Angi en konto og passord for å konfigurere RMS-koblingen for å fortsette.

## <a name="EnteringCredentials"></a>Angi legitimasjon
Før du kan konfigurere RMS-kobling, må du angi legitimasjon for en konto som har tilstrekkelige rettigheter til å konfigurere RMS-koblingen.

Hvis du har implementert [kort Kontroller](https://technet.microsoft.com/library/jj658941.aspx), må du kontrollere at kontoen du skrev inn er i stand til å beskytte innholdet. Hvis du har begrenset mulighet til å beskytte innholdet i gruppen "IT-avdelingen", må kontoen som du angir her for eksempel være medlem av gruppen. Hvis ikke, vil du se feilmeldingen: **Forsøket på å finne plasseringen av administrasjonstjenesten og organisasjonen mislyktes. Kontroller at Microsoft Rights Management-tjenesten er aktivert for organisasjonen.**

Du kan bruke en konto som har én av følgende rettigheter:

-   **Office 365-Leieradministrator**: En konto som er en global administrator for Office 365-leier.

-   **Microsoft RMS leier Global Administrator**: En konto med administratorrettigheter på Microsoft RMS-leier.

-   **Microsoft RMS-kontakt Administrator**: En konto i Active Directory, Azure som har fått rettigheter til å installere og administrere RMS-kontakt for organisasjonen.

    > [!NOTE]
    > Hvis du vil bruke Microsoft RMS-koblingen administratorkonto, må du først gjøre følgende for å tilordne administratorrollen RMS connector:
    > 
    > 1.  På samme datamaskin, kan du laste ned og installere Windows PowerShell for Rights Management. Hvis du vil ha mer informasjon, se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).
    > 
    >     Start Windows PowerShell med den **Kjør som administrator** kommando, og koble til Azure RMS-tjenesten ved hjelp av den [koble til AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) kommando:
    > 
    >     ```
    >     Connect-AadrmService                   //provide Office365 Tenant Administrator or Microsoft RMS Tenant Global Administrator credential
    >     ```
    > 2.  Kjør den [Legg til AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/windowsazure/dn629417.aspx) kommandoen, bruker bare én av følgende parametere:
    > 
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    > 
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    > 
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     Skriv for eksempel: **Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role " ConnectorAdministrator "**
    > 
    >     Men disse kommandoene bruke ConnectorAdministrator-rollen, kan du også bruke GlobalAdministrator-rollen her også.

Under installasjonen RMS-kontakt, valideres og installert alle nødvendige programvaren, Internet Information Services (IIS) er installert hvis denne ikke allerede finnes og connector-programvaren er installert og konfigurert. I tillegg er RMS klargjort for konfigurasjon ved å opprette følgende:

-   En tom tabell over servere som er autorisert til å bruke koblingen til å kommunisere med Azure RMS. Du vil legge til servere til denne tabellen senere.

-   Et sett med sikkerhetstokener for koblingen, som godkjenner operasjoner med Azure RMS. Disse symbolene er lastet ned fra Azure RMS og installert på den lokale datamaskinen i registret. De er beskyttet ved hjelp av data protection application programming interface (DPAPI) og påloggingsinformasjonen for kontoen for lokalt System.

Gjør følgende på den siste siden i veiviseren, og klikk deretter **er ferdig med**:

-   Hvis dette er den første koblingen som du har installert, merker du ikke **Start kontakt administrator-konsollen til å godkjenne servere** på dette tidspunktet. Du vil velge dette alternativet etter at du har installert den andre (eller siste) RMS-koblingen. I stedet kjøre veiviseren på nytt på minst én datamaskin. Du må installere minst to kontakter.

-   Hvis du har installert den andre (eller siste)-koblingen, velger du **Start kontakt administrator-konsollen til å godkjenne servere**.

> [!TIP]
> Det er nå en bekreftelse test du kan utføre for å teste om webtjenester for RMS-kobling er i drift:
> 
> -   Koble til fra en web-leser, **http://&lt;connectoraddress&gt;/_wmcs/certification/servercertification.asmx**, å erstatte *&lt; connectoraddress &gt;* med serveradressen eller navnet som har RMS-kontakt som er installert. En vellykket tilkobling viser en **ServerCertificationWebService** siden.

Hvis du trenger å avinstallere RMS-koblingen, kjører du veiviseren på nytt, og velg avinstallasjonsalternativet.

## <a name="AuthorizingServers"></a>Godkjenning av servere for å bruke RMS-kobling
Når du har installert RMS-koblingen på minst to datamaskiner, er du klar til å godkjenne servere og tjenester som du ønsker å bruke RMS-koblingen. Hvis du for eksempel servere som kjører Exchange Server 2013 eller SharePoint Server-2013.

Hvis du vil definere disse serverne, kjører RMS-Koblingsverktøy for administrasjon og legge til oppføringer i listen over tillatte servere. Du kan kjøre dette verktøyet når du velger **Start administrasjonskonsollen for connector til å godkjenne servere** på slutten av Microsoft Rights Management-koblingen installasjonen veiviseren, eller du kan kjøre den separat fra veiviseren.

Når du godkjenner disse serverne, må du være klar over følgende hensyn:

-   Servere som du legger til, vil bli gitt spesielle privilegier. Alle kontoer som du angir for Exchange Server-rollen i kobling-konfigurasjonen vil bli gitt til [super brukerrolle](https://technet.microsoft.com/library/mt147272.aspx) i Azure RMS, som gir dem tilgang til alt innhold for denne RMS-leier. Superbruker-funksjonen aktiveres automatisk på dette tidspunktet Hvis det er nødvendig. Hvis du vil unngå sikkerhetsrisikoen for heving av tilgangsnivåer, pass på at du angir hvilke konti som brukes av Exchange-servere i organisasjonen. Alle servere som er konfigurert som SharePoint-servere eller servere som bruker FCI gis vanlig brukerrettigheter.

-   Du kan legge til flere servere som en enkelt oppføring ved å angi en Active Directory-sikkerhet eller distribusjonsgruppe, eller en tjenestekonto som brukes av mer enn én server. Når du bruker denne konfigurasjonen, gruppe med servere som skal dele de samme RMS-sertifikatene og alle anses eiere for innhold som noen av dem er beskyttet. Hvis du vil minimere administrative administrasjonskostnader, anbefaler vi at du bruker denne konfigurasjonen av en enkelt gruppe i stedet for individuelle servere for å godkjenne organisasjonens Exchange-servere eller en SharePoint-serverfarm.

På den **servere tillates for å bruke koblingen** klikker du **Legg til**.

### <a name="BKMK_AddServer"></a>Legge til en server i listen over tillatte servere
På den **at en server kan bruke koblingen** side, angir du navnet på objektet, eller Bla gjennom for å identifisere objektet du vil autorisere.

Det er viktig at du godkjenner det riktige objektet. Kontoen som kjører tjenesten for lokale (for eksempel Exchange eller SharePoint) for en server å bruke koblingen må være valgt for godkjenning. For eksempel hvis tjenesten kjører som en konfigurert tjenestekonto, legge til navnet på denne kontoen i listen. Hvis tjenesten kjører som lokalt System, kan du legge til navnet på objektet (for eksempel servernavn$). Som beste praksis, kan du opprette en gruppe som inneholder disse kontoene og angi gruppe i stedet for enkelte server-navn.

Mer informasjon om de forskjellige serverrollene:

-   For servere som kjører Exchange: Du må angi en sikkerhetsgruppe, og du kan bruke standardgruppe (**Exchange-servere**) som Exchange automatisk oppretter og vedlikeholder av alle Exchange-servere i skogen.

-   For servere som kjører SharePoint:

    -   Hvis et SharePoint 2010-server er konfigurert til å kjøre som lokalt System (det ikke er bruker en tjenestekonto), manuelt opprette en sikkerhetsgruppe har i Active Directory Domain Services, og legge til navnet datamaskinobjektet for serveren i denne konfigurasjonen til denne gruppen.

    -   Hvis en SharePoint-server er konfigurert for å bruke en tjenestekonto (anbefalt praksis for SharePoint 2010) og det eneste alternativet for SharePoint 2013, gjør du følgende:

        1.  Legge til service-kontoen som kjører tjenesten for Sentraladministrasjon av SharePoint for å aktivere SharePoint konfigureres fra sin administrator-konsollen.

        2.  Legg til kontoen som er konfigurert for SharePoint App Pool.

        > [!TIP]
        > Hvis disse to kontoer er forskjellige, kan du vurdere å opprette en enkelt gruppe som inneholder begge kontoene for å redusere de administrative administrasjonskostnader.

-   For servere som bruker filen klassifisering infrastrukturen, kjøre de tilknyttede tjenestene som den lokale systemkontoen, så må du godkjenne kontoen for filservere (for eksempel servernavn$) eller en gruppe som inneholder disse datamaskinkontoer.

Når du er ferdig med å legge til servere til i listen, klikker du **Lukk**.

Hvis du ikke allerede har gjort det, må du nå konfigurere belastningsfordeling for servere som har RMS-koblingen som er installert, og vurdere om du skal bruke HTTPS for tilkoblinger mellom disse serverne og servere som du akkurat har godkjent.

## <a name="ConfiguringConnector"></a>Konfigurere Last belastningsfordeling og høy tilgjengelighet
Etter at du har installert andre eller den siste forekomsten av RMS-koblingen, kan du definere kobling URL-navnet på en server og konfigurere systemet for belastningsfordeling.

Kobling URL-servernavnet kan være et hvilket som helst navn under et navneområde du kontrollerer. Du kan for eksempel opprette en oppføring i DNS-systemet for **rmsconnector.contoso.com** og konfigurere denne oppføringen hvis du vil bruke en IP-adresse i systemet for belastningsfordeling. Det er ingen spesielle krav for dette navnet, og den må ikke konfigureres på selve koblingen serverne. Hvis Exchange- og SharePoint-servere skal være kommunikasjon med koblingen over Internett, har ikke dette navnet til å løse på Internett.

> [!IMPORTANT]
> Vi anbefaler at du ikke kan endre dette navnet når du har konfigurert Exchange eller SharePoint-servere for å kunne bruke koblingen, fordi du må deretter fjerner disse serverne av alle IRM-konfigurasjoner og konfigurere dem på nytt.

Når navnet er opprettet i DNS og er konfigurert for en IP-adresse, kan du konfigurere belastningsfordeling for adressen, som leder trafikk til kontakt-servere. Du kan bruke en hvilken som helst IP-baserte belastningsfordeling for dette formålet, som inkluderer Network Load Balancing (NLB)-funksjonen i Windows Server. Hvis du vil ha mer informasjon, se [Load Balancing Deployment Guide](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx).

Bruk følgende innstillinger til å konfigurere NLB-klynger:

-   Porter: 80 (for HTTP) eller 443 (for HTTPS)

    Hvis du vil ha mer informasjon om HTTP eller HTTPS, kan du se den neste delen.

-   Affinitet: Ingen

-   Metode for programvaredistribusjon: Er lik

Dette navnet som du definerer for belastningsfordeling system (for servere som kjører RMS-tilkoblingstjeneste) er navnet på organisasjonen RMS koblingen du vil bruke senere, når du konfigurerer de lokale serverne bruk av RMS Azure.

## <a name="BKMK_ConfiguringHTTPS"></a>Konfigurere RMS-koblingen for å bruke HTTPS
> [!NOTE]
> Denne konfigurasjonstrinnet er valgfritt, men anbefales for ekstra sikkerhet.

Selv om bruken av TLS eller SSL er valgfrie for RMS-kobling, anbefaler vi den for eventuelle HTTP-baserte sikkerhetssensitiv-tjenesten. Denne konfigurasjonen godkjenner serverne kjører koblingen til Exchange- og SharePoint-serverne som bruker koblingen. I tillegg alle data som sendes fra disse serverne til koblingen er kryptert.

Hvis du vil aktivere RMS-koblingen til å bruke TLS, på hver server som kjører RMS-kobling, må du installere et sertifikat for godkjenning av serveren som inneholder navnet du vil bruke for koblingen. For eksempel hvis RMS-kontakt navn som du har definert i DNS er **rmsconnector.contoso.com**, distribuere et sertifikat for godkjenning av serveren som inneholder **rmsconnector.contoso.com** i emnet for serversertifikatet som vanlig navn. Angi **rmsconnector.contoso.com** i det alternative navnet for sertifikatet som DNS-verdien. Sertifikatet har ikke å inkludere navnet på serveren. I IIS, binde dette sertifikatet til standard Web-område.

Hvis du bruker HTTPS-alternativet, må du kontrollere at alle servere som kjører koblingen har en gyldig servergodkjenning sertifikat som stammer fra en rotsertifiseringsinstans som stoler på at Exchange og SharePoint-servere. I tillegg hvis sertifiseringsinstansen (CA) som utstedte sertifikater for tilkoblingsservere publiserer sertifikatopphevelseslisten (CRL), må Exchange og SharePoint-servere kunne laste ned denne CRLEN.

> [!TIP]
> Du kan bruke følgende informasjon og ressurser til å be om og installere et sertifikat for godkjenning av serveren, og å binde dette sertifikatet til standard Web-område i IIS:
> 
> -   Hvis du bruker Active Directory-sertifikattjenester (AD CS) og sertifiseringsinstans (CA) til å distribuere disse serversertifikater for godkjenning, kan du kopiere og deretter bruke sertifikatmalen Web-serveren. Denne sertifikatmalen bruker **angitt i forespørselen** for emnenavnet for sertifikatet, noe som betyr at du kan gi FQDN for navnet på RMS-kobling for emnenavn for sertifikat eller alternativt navn for emne når du ber om sertifikatet.
> -   Hvis du bruker en frittstående Sertifiseringsinstans eller kjøpe dette sertifikatet fra et annet firma, kan du se [konfigurering av Internet serversertifikater (IIS 7)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) i den [Web Server (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) dokumentasjonsbibliotek på TechNet.
> -   Hvis du vil konfigurere IIS til å bruke sertifikatet, kan du se [legge til en Binding til et område (IIS 7)](http://technet.microsoft.com/library/cc731692.aspx) i den i den [Web Server (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) dokumentasjonsbibliotek på TechNet.

## <a name="BKMK_ConfiguringWebProxy"></a>Konfigurere RMS-kontakt for en proxy-server
Hvis serverne connector er installert i et nettverk som ikke har direkte Internett-tilkobling og krever manuell konfigurasjon av en proxy-server for utgående Internett-tilgang, må du konfigurere registret på disse serverne til RMS-koblingen.

#### Slik konfigurerer du RMS-koblingen for å bruke en proxy-server

1.  På hver server som kjører RMS-koblingen, åpner du Registerredigering, for eksempel Regedit.

2.  Gå til **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  Legge til strengverdien for **ProxyAddress** og angi deretter dataene for denne verdien til å være **: http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**

    For eksempel: **http://proxyserver.contoso.com:8080**

4.  Lukk Registerredigering, og Start serveren på nytt eller utfører en IISReset kommando for å starte IIS på nytt.

## <a name="BKMK_InstallingStandaloneTool"></a>Installerer RMS administrasjon koblingsverktøyet på administrative datamaskiner
Du kan kjøre RMS koblingsverktøyet-administrasjon fra en datamaskin som ikke har RMS-connector er installert, hvis datamaskinen oppfyller følgende krav:

-   En fysisk eller virtuell datamaskin som kjører Windows Server 2012 eller Windows Server 2012 R2 (alle versjoner), Windows Server 2008 R2 eller Windows Server 2008 R2 Service Pack 1 (alle versjoner), Windows 8.1, Windows 8 eller Windows 7.

-   Minst 1 GB RAM.

-   Minimum 64 GB ledig plass på harddisken.

-   Minst én nettverksgrensesnittet.

-   Tilgang til Internett via en brannmur (eller webproxy).

Hvis du vil installere RMS administrasjon koblingsverktøyet, kjører du følgende filer:

-   For en 32-biters datamaskin: RMSConnectorAdminToolSetup_x86.exe

-   For en 64-biters datamaskin: RMSConnectorSetup.exe

Hvis du ikke har allerede lastet ned disse filene, kan du gjøre dette fra den [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=314106).

## <a name="ConfiguringServers"></a>Konfigurere servere for å bruke RMS-kobling
Når du har installert og konfigurert RMS-koblingen, er du klar til å konfigurere lokale serverne som skal bruke Rights Management og koble til Azure RMS ved hjelp av koblingen. Dette betyr at du konfigurerer følgende servere:

-   For Exchange-2013: Client access-servere og e-postservere

-   For Exchange 2010: Client access-servere og hub transport-servere

-   For SharePoint: Front SharePoint-webservers, inkludert de som er vert for Sentraladministrasjon av SharePoint-server

-   For filen klassifisering infrastruktur: Windows Server-datamaskiner som har installert fil Resource Manager

Denne konfigurasjonen krever registerinnstillinger. Hvis du vil gjøre dette, har du to alternativer:

|Konfigurasjonsalternativet|Fordeler|Ulemper|
|------------------------------|------------|-----------|
|Automatisk ved å bruke verktøyet for konfigurasjon av server for Microsoft RMS-kobling|Ingen direkte redigering av registret. Dette er automatisert ved hjelp av et skript.<br /><br />Du trenger ikke å kjøre et Windows PowerShell-cmdleten for å få URL-adressen for Microsoft RMS.<br /><br />Forutsetningene kontrolleres automatisk for deg (men ikke automatisk remediated) Hvis du kjører det lokalt.|Når du kjører verktøyet, må du opprette en tilkobling til en server som allerede kjører RMS-koblingen.|
|Manuelt ved å redigere registret|Det kreves ingen tilkobling til en server som kjører RMS-koblingen.|Flere administrative indirekte kostnader som er utsatt for feil.<br /><br />Du må skaffe din Microsoft RMS-URL, som krever at du kjører et Windows PowerShell-kommando.<br /><br />Du må alltid ta alle forutsetninger kontrollene selv.|
> [!IMPORTANT]
> I begge tilfeller må du manuelt installere eventuelle forutsetninger og konfigurere Exchange, SharePoint og filen klassifisering infrastruktur for å bruke IRM.

For de fleste organisasjoner blir automatisk konfigurasjon ved hjelp av verktøyet for konfigurasjon av server for Microsoft RMS-koblingen bedre alternativ, fordi det gir større effektivitet og pålitelighet enn manuell konfigurasjon.

Når du har gjort endringer i systemkonfigurasjonen på disse serverne, må starte dem på nytt hvis de kjører Exchange eller SharePoint og tidligere konfigurert til å bruke AD RMS. Det er ikke nødvendig å starte disse serverne på nytt Hvis du konfigurerer dem for rettighetsadministrasjon for første gang. Du må alltid starte filserver som er konfigurert til å bruke filen klassifisering infrastruktur etter at du har endret disse konfigurasjonsinnstillingene.

#### Slik bruker du verktøyet for konfigurasjon av server for Microsoft RMS-kobling

1.  Hvis du ikke har allerede lastet ned skript for verktøyet for konfigurasjon av server for Microsoft RMS-kobling (GenConnectorConfig.ps1), laste det ned fra den [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=314106).

2.  Lagre GenConnectorConfig.ps1-filen på datamaskinen der du vil kjøre verktøyet. Hvis du vil kjøre verktøyet lokalt, må dette være serveren du vil konfigurere for å kommunisere med RMS-koblingen. Hvis ikke, kan du lagre det på en hvilken som helst datamaskin.

3.  Bestemme hvordan du vil kjøre verktøyet:

    -   **Lokalt**: Du kan kjøre verktøyet interaktivt, fra serveren konfigurert til å kommunisere med RMS-koblingen. Dette er nyttig for en engangs konfigurasjon, for eksempel en testmiljøet.

    -   **Programvaredistribusjon**: Du kan kjøre verktøyet for å produsere registerfilene som du deretter distribuerer til én eller flere aktuelle servere ved hjelp av en systems management-program som støtter programvaredistribusjon av, for eksempel System Center Configuration Manager.

    -   **Gruppepolicy,**: Du kan kjøre verktøyet for å lage et skript som du gir til en administrator som kan opprette gruppepolicyobjekter for servere som skal konfigureres. Dette skriptet oppretter ett gruppepolicyobjekt for hver server konfigureres, som systemansvarlig kan tildele til de aktuelle serverne.

    > [!NOTE]
    > Dette verktøyet konfigurerer servere som skal kommunisere med RMS-koblingen, og som er oppført i begynnelsen av denne delen. Ikke Kjør dette verktøyet på servere som kjører RMS-koblingen.

4.  Start Windows PowerShell med den **kjøre som administrator** alternativ, og bruk kommandoen Get-help for å lese instruksjonene slik Bruk verktøyet for konfigurasjon av valgte-metoden:

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Når verktøyet har kjørt, be deg angi URL-adressen til RMS-koblingen for din organisasjon. Angi protokollprefikset (HTTP:// eller HTTPS://) og navnet på koblingen som du definerte i DNS for belastningsfordeles adressen for koblingen. Https://connector.contoso.com for eksempel. Verktøyet bruker denne URL-adressen til å kontakte serverne som kjører RMS-koblingen deretter og få andre parametere som brukes til å opprette de nødvendige konfigurasjonene.

> [!IMPORTANT]
> Når du kjører dette verktøyet, må du kontrollere at du angir navnet på koblingen belastningsfordelt RMS for organisasjonen, og ikke navnet på en enkelt server som kjører RMS-tilkoblingstjeneste.

Bruk de følgende delene for spesifikk informasjon for hver tjeneste:

-   [Configuring an Exchange server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ExchangeServer)

-   [Configuring a SharePoint server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringSharePoint)

-   [Configuring a file server for File Classification Infrastructure to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_FileServer)

> [!NOTE]
> Når disse serverne er konfigurert til å bruke koblingen, kanskje ikke klientprogrammer som er installert lokalt på disse serverne fungerer med RMS. Når dette skjer, er det fordi programmene forsøker å bruke koblingen i stedet for å bruke RMS direkte, som ikke støttes.
> 
> I tillegg Office 2010 er installert lokalt på en Exchange-server, den klientprogram IRM-funksjonene vil kanskje fungere fra datamaskinen etter at serveren er konfigurert til å bruke koblingen, men dette støttes ikke.
> 
> I begge tilfellene må du installere klientapplikasjoner på separate datamaskiner som ikke er konfigurert for å bruke koblingen. Deretter riktig bruker RMS direkte.

### <a name="BKMK_ExchangeServer"></a>Konfigurere en Exchange-server for å kunne bruke koblingen
Følgende Exchange roller kommunisere med RMS-koblingen:

-   For Exchange-2013: Klientadgangsserver og postboksserver

-   For Exchange 2010: Klientadgangsserver og hub transport-server

For å bruke RMS-kobling, må disse serverne kjører Exchange kjøre ett av følgende programvareversjoner:

-   Exchange Server 2013 med Exchange-2013 kumulativ oppdatering 3

-   Exchange Server 2010 med Exchange 2010 Service Pack 3-samleoppdateringen 6

Du må også installere på disse serverne, en versjon av RMS-klienten som inkluderer støtte for RMS kryptografiske modus 2. Minimumsversjonen som støttes i Windows Server 2008 er inkludert i hurtigreparasjonen som du kan laste ned fra [RSA nøkkellengde økes til 2048 biter for AD RMS i Windows Server 2008 R2 og Windows Server 2008](http://support.microsoft.com/kb/2627272). Den minste versjonen for Windows Server 2008 R2 kan lastes ned fra [RSA nøkkellengde økes til 2048 biter for AD RMS i Windows 7 eller Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Windows Server 2012 og Windows Server 2012 R2 støtter kryptografiske modus 2.

> [!IMPORTANT]
> Hvis disse versjoner eller senere versjoner av Exchange og RMS-klienten ikke er installert, kan du ikke konfigurere Exchange hvis du vil bruke koblingen. Kontroller at disse versjonene er installert før du fortsetter.

##### Slik konfigurerer du Exchange-servere for å kunne bruke koblingen

1.  På Exchange server-rollene som kommuniserer med RMS-koblingen, gjør du ett av følgende:

    -   Kjør konfigurasjonsverktøyet for Microsoft RMS-kobling for serveren. Hvis du vil ha mer informasjon, se [How to use the server configuration tool for Microsoft RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_HowToRunTheTool) i dette emnet.

    -   Foreta manuelle register redigering ved hjelp av tabellene nedenfor til å legge til innstillingene i registret manuelt på serverne.

2.  Aktivere IRM-funksjonalitet i Exchange. Hvis du vil ha mer informasjon, se [informasjon Rights Management prosedyrer](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx) i Exchange-biblioteket.

Hvis du vil legge til eller registerinnstillinger på disse serverne, som konfigurerer servere for å bruke RMS-koblingen manuelt, bruker du tabellene nedenfor. Instruksjoner for når du bruker disse tabellene:

-   *MicrosoftRMSURL* er organisasjonens Microsoft RMS URL-adresse. Slik finner du denne verdien:

    1.  Kjøre den [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdleten for Azure RMS. Hvis du ikke allerede har installert Windows PowerShell-modul for Azure RMS, se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

    2.  Fra utdataene, kan du identifisere den **LicensingIntranetDistributionPointUrl** verdi.

        For eksempel: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  Fra-verdien, kan du fjerne **/_wmcs/lisensiering** fra denne strengen. Gjenstående strengen er URL-adressen for Microsoft RMS. I vårt eksempel være Microsoft RMS URL-adressen følgende verdi:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.RMS.NA.aadrm.com**

-   *ConnectorFQDN* er navnet belastningsfordeling som du har definert i DNS for koblingen. For eksempel **rmsconnector.contoso.com**.

-   Prefikset HTTPS for URL-adresse for kobling hvis du har konfigurert koblingen for å bruke HTTPS til å kommunisere med de lokale serverne. Hvis du vil ha mer informasjon, se den [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS) delen i dette emnet. URL-adresser til Microsoft RMS Bruk alltid HTTPS.

#### Tabell for Exchange 2013 registerinnstillinger

|Registerbane|Type|Verdi|Data|
|----------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation|Reg_SZ|Standard|https://*_wmcs/MicrosoftRMSURL-sertifisering*|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|https://MicrosoftRMSURL/_wmcs/Licensing|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|

#### Tabell for Exchange 2010-registerinnstillinger

|Registerbane|Type|Verdi|Data|
|----------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation|Reg_SZ|Standard|https://*MicrosoftRMSURL*/_wmcs /-sertifisering|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|https://*MicrosoftRMSURL*/_wmcs/lisensiering|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra Exchange-serveren i RMS-kobling:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|

### <a name="BKMK_ConfiguringSharePoint"></a>Konfigurere en SharePoint-server Hvis du vil bruke koblingen
Følgende SharePoint-roller, kommunisere med RMS-koblingen:

-   Front SharePoint-webservers, inkludert de som er vert for Sentraladministrasjon av SharePoint-server

For å bruke RMS-kobling, må disse serverne som kjører SharePoint Team Services kjører én av følgende programvareversjoner:

-   SharePoint Server 2013

-   SharePoint Server 2010

En server for SharePoint 2013 må også kjøre en versjon av MSIPC-klienten 2.1 som er from1.0.622.34 gjennom 1.0.10907.0.

> [!WARNING]
> Det finnes flere versjoner av MSIPC 2.1-klienten, så pass på å installere en versjon som er nevnt i denne artikkelen.
> 
> Du kan også kontrollere klientversjonen ved å kontrollere versjonsnummeret for MSIPC.dll, som ligger i **\Program Files\Active Directory Rights Management Services Client 2.1**. Egenskaper-dialogboksen viser versjonsnummeret for klienten MSIPC 2.1.

Disse serverne kjører SharePoint 2010 må ha installert en versjon av MSDRM-klient som inkluderer støtte for RMS kryptografiske modus 2. Minimumsversjonen som støttes i Windows Server 2008 er inkludert i hurtigreparasjonen som du kan laste ned fra [RSA nøkkellengde økes til 2048 biter for AD RMS i Windows Server 2008 R2 og Windows Server 2008](http://support.microsoft.com/kb/2627272), og den minste versjonen for Windows Server 2008 R2 kan lastes ned fra [RSA nøkkellengde økes til 2048 biter for AD RMS i Windows 7 eller Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Windows Server 2012 og Windows Server 2012 R2 støtter kryptografiske modus 2.

##### Konfigurere SharePoint-servere for å kunne bruke koblingen

1.  På SharePoint-serverne kommuniserer med RMS-koblingen, gjør du ett av følgende:

    -   Kjør konfigurasjonsverktøyet for Microsoft RMS-kobling for serveren. Hvis du vil ha mer informasjon, se [How to use the server configuration tool for Microsoft RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_HowToRunTheTool) i dette emnet.

    -   Hvis du bruker SharePoint 2013, kan du gjøre manuelle register redigering ved hjelp av tabellen i delen nedenfor til å legge til innstillingene i registret manuelt på serverne.

2.  Aktivere IRM i SharePoint. Hvis du vil ha mer informasjon, se [konfigurere Information Rights Management (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) i SharePoint-biblioteket.

    Når du følger disse instruksjonene, må du konfigurere SharePoint for å kunne bruke koblingen ved å angi **Bruk denne RMS-serveren**, og angi deretter belastningsfordeling kobling URL-adressen som du har konfigurert. Angi protokollprefikset (HTTP:// eller HTTPS://) og navnet på koblingen som du definerte i DNS for belastningsfordeles adressen for koblingen. For eksempel hvis navnet på koblingen er https://connector.contoso.com, konfigurasjonen vil se ut som i illustrasjonen nedenfor:

    ![](../Image/AzRMS_SharePointConnector.png)

    Når IRM er aktivert på en SharePoint-farm, kan du aktivere IRM på individuelle biblioteker ved hjelp av den **Information Rights Management** alternativet på den **bibliotekinnstillinger** side for hver av bibliotekene.

    > [!IMPORTANT]
    > For SharePoint å få tilgang til RMS ved hjelp av koblingen, må du godkjenne de tilsvarende kontiene i administrasjonsverktøyet for RMS-kobling. Hvis du ikke allerede har gjort dette, kan du se [Authorizing servers to use the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#AuthorizingServers) i dette emnet.

Bruk tabellen nedenfor hvis du vil legge til eller registerinnstillinger på en server som kjører SharePoint 2013 manuelt.

#### Tabell for registerinnstillinger for SharePoint 2013
Instruksjoner for når du bruker denne tabellen:

-   *MicrosoftRMSURL* er organisasjonens Microsoft RMS URL-adresse. Slik finner du denne verdien:

    1.  Kjøre den [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdleten for Azure RMS. Hvis du ikke allerede har installert Windows PowerShell-modul for Azure RMS, se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

    2.  Fra utdataene, kan du identifisere den **LicensingIntranetDistributionPointUrl** verdi.

        For eksempel: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  Fra-verdien, kan du fjerne **/_wmcs/lisensiering** fra denne strengen. Gjenstående strengen er URL-adressen for Microsoft RMS. I vårt eksempel være Microsoft RMS URL-adressen følgende verdi:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.RMS.NA.aadrm.com**

-   *ConnectorFQDN* er navnet belastningsfordeling som du har definert i DNS for koblingen. For eksempel **rmsconnector.contoso.com**.

-   Prefikset HTTPS for URL-adresse for kobling hvis du har konfigurert koblingen for å bruke HTTPS til å kommunisere med de lokale serverne. Hvis du vil ha mer informasjon, se den [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS) delen i dette emnet. URL-adresser til Microsoft RMS Bruk alltid HTTPS.

|Registerbane|Type|Verdi|Data|
|----------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection|Reg_SZ|https://*MicrosoftRMSURL*/_wmcs/lisensiering|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra SharePoint-serveren til RMS-kontakten:<br /><br />-   http://*ConnectorFQDN*/_wmcs/lisensiering<br />-   https://*ConnectorFQDN*/_wmcs/lisensiering|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification|Reg_SZ|Standard|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra SharePoint-serveren til RMS-kontakten:<br /><br />-   http://*ConnectorFQDN*/_wmcs /-sertifisering<br />-   https://*ConnectorFQDN*/_wmcs /-sertifisering|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|Ett av følgende, avhengig av om du bruker HTTP- eller HTTPS fra SharePoint-serveren til RMS-kontakten:<br /><br />-   http://*ConnectorFQDN*/_wmcs/lisensiering<br />-   https://*ConnectorFQDN*/_wmcs/lisensiering|

### <a name="BKMK_FileServer"></a>Konfigurere en filserver for filen klassifisering infrastruktur for å bruke koblingen
For å bruke RMS-kontakt og filen klassifisering infrastruktur for å beskytte Office-dokumenter, må filserveren kjøre ett av følgende operativsystemer:

-   Windows Server 2012 R2

-   Windows Server 2012

##### Konfigurere servere for å kunne bruke koblingen

1.  Servere som er konfigurert for filen klassifisering infrastruktur og som skal kommunisere med RMS-koblingen for filen, gjør du ett av følgende:

    -   Kjør konfigurasjonsverktøyet for Microsoft RMS-kobling for serveren. Hvis du vil ha mer informasjon, se [How to use the server configuration tool for Microsoft RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_HowToRunTheTool) i dette emnet.

    -   Foreta manuelle register redigering ved hjelp av tabellen i delen nedenfor til å legge til innstillingene i registret manuelt på serverne.

2.  Opprett regler for klassifisering og oppgavene for filen til å beskytte dokumenter med RMS-kryptering, og deretter angi en RMS-mal for å bruke RMS-policyer automatisk. Hvis du vil ha mer informasjon, se [File Server Resource Manager oversikt](http://technet.microsoft.com/library/hh831701.aspx) i biblioteket for Windows Server-dokumentasjonen.

Bruk tabellen nedenfor hvis du vil legge til eller registerinnstillinger på en filserver som bruker filen klassifisering-infrastruktur til å beskytte dokumenter manuelt.

#### Tabell for filserveren og registerinnstillinger for filen klassifisering infrastruktur
Instruksjoner for når du bruker denne tabellen:

-   *ConnectorFQDN* er navnet belastningsfordeling som du har definert i DNS for koblingen. For eksempel **rmsconnector.contoso.com**.

-   Prefikset HTTPS for URL-adresse for kobling hvis du har konfigurert koblingen for å bruke HTTPS til å kommunisere med de lokale serverne. Hvis du vil ha mer informasjon, se den [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS) delen i dette emnet. URL-adresser til Microsoft RMS Bruk alltid HTTPS.

|Registerbane|Type|Verdi|Data|
|----------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|http://*ConnectorFQDN*/_wmcs/lisensiering|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation|Reg_SZ|Standard|http://*ConnectorFQDN*/_wmcs /-sertifisering|

## <a name="BKMK_NextSteps"></a>Neste trinn
Nå som RMS-connector er installert og konfigurert, og serverne er konfigurert til å bruke den, kan IT-administratorer og brukere beskytte og bruke e-postmeldingen og dokumenter ved hjelp av Azure RMS. Hvis du vil gjøre det enkelt for brukere, kan du distribuere RMS deling av programmer som installerer et tillegg for Office, og legger til nye alternativer for Høyreklikk i Filutforsker. Hvis du vil ha mer informasjon, se den [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/%20dn339003%28v=ws.10%29.aspx).

I tillegg kan du vurdere følgende for å hjelpe deg med å overvåke RMS-koblingen og organisasjonens bruk av RMS:

-   Innebygde **Kontakt Microsoft Rights Management** ytelsestellere

-   [Logging og analysere Azure Rights Management-forbruk](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md)

Du kan bruke den [Veikart for Azure Rights Management-distribusjon](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til å kontrollere om det finnes andre konfigurasjonstrinn som du vil gjøre før du ruller [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for brukere og administratorer. Hvis det ikke er noen andre konfigurasjonstrinn du trenger å gjøre, se [Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) for operative veiledning til å støtte en vellykket distribusjon for organisasjonen.

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

