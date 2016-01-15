---
description: na
keywords: na
title: Requirements for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
---
# Krav for Azure Rights Management
Hvis du vil distribuere Microsoft Azure Rights Management (Azure RMS) i organisasjonen, må du kontrollere at du har følgende forutsetninger. Du kan deretter bruke den [Veikart for Azure Rights Management-distribusjon](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til å distribuere Rights Management for organisasjonen.

|Krav|Hvis du vil ha mer informasjon|
|--------|----------------------------------|
|Et abonnement på sky for RMS|Organisasjonen må ha et abonnement på sky som støtter RMS.<br /><br />Mer informasjon om lisensiering, se den [Cloud-abonnementer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) delen i dette emnet.|
|Azure AD-katalogen|Organisasjonen din må ha en Azure AD-katalog som støtter brukergodkjenning for RMS. Hvis du vil bruke brukerkontoene dine lokale katalogen (AD DS), må du i tillegg også konfigurere directory-integrering.<br /><br />Multifaktorautentisering (MFA) støttes med Azure RMS når du har nødvendig klientprogramvare og riktig konfigurert MFA støttende infrastruktur.<br /><br />Hvis du vil ha mer informasjon, se den [Azure AD-katalogen](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_AzureADTenant) delen i dette emnet.|
|Klientenheter|Brukere må ha en klientenheter (datamaskin eller mobil enhet) som kjører et operativsystem som støtter RMS.<br /><br />Hvis du vil ha mer informasjon, se den [Klientenheter som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices) delen i dette emnet.|
|Programmer|Brukerne må kjøre programmer som støtter RMS.<br /><br />Hvis du vil ha mer informasjon, se den [Programmer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) delen i dette emnet.|
|Infrastrukturen som støtter tilkobling til Internett og avhengige cloud-tjenester|Hvis du har en brannmur eller lignende mellomliggende enheter som må konfigureres til å tillate at bestemte tilkoblinger, kan du se [Office 356 URL-adresser og IP-adresse områder](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Liste over URL-adresser og IP-adresser i den **Office 356 portal og identitet** delen gjelder for Office 365-portalen, Azure Active Directory-ressurser og Azure Rights Management. Bruk instruksjonene i denne artikkelen til å holde oppdatert med endringer til denne informasjonen ved å abonnere på en RSS-feed.<br /><br />I tillegg til informasjonen i Office-artikkel gjelder Azure RMS:<br /><br />-   Avbryt ikke TLS klienttjenesten til tilkoblingen (for eksempel for å gjøre pakkenivå inspeksjon). Dette bryter sertifikatet feste at RMS-klienter bruker med Microsoft-administrerte CAs til å sikre deres kommunikasjon med Azure RMS.<br />-   Ikke bruk en proxy-konfigurasjon som godkjenner på vegne av en bruker.|

Hvis du vil bruke Azure RMS med lokale servere, støttes følgende produkter:

-   Exchange Server

-   SharePoint Server

-   Windows Server-filservere som støtter filen klassifisering infrastruktur

Informasjon om tilleggskrav Azure RMS for dette scenariet, kan du se den [Lokale servere som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedServers) delen i dette emnet.

> [!IMPORTANT]
> Følgende distribusjonsscenariet støttes ikke:
> 
> -   Kjører AD RMS og Azure RMS side-ved-side i samme organisasjon, unntatt under overføring, som beskrevet i [Migrering fra AD RMS til Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).
> 
> Det er en støttet overføring bane [fra AD RMS til Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx), og fra [Azure RMS til AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Hvis du distribuerer Azure RMS, og deretter bestemmer deg for at du ikke lenger ønsker å bruke denne tjenesten i skyen, kan du se [Dekommisjonering og deaktivere Azure Rights Management](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

Bruk delene nedenfor for å lære mer om kravene til Azure RMS.

## <a name="BKMK_SupportedSubscriptions"></a>Cloud-abonnementer som støtter Azure RMS
Hvis du vil bruke Azure RMS, må organisasjonen ha minst ett av følgende abonnementer med et tilstrekkelig antall lisenser for brukere og tjenester som vil beskytte filer og e-postmeldinger. Hvis du har en tjeneste som du vil bruke beskyttelse for brukere (eiere av filene eller e-postmeldinger), krever disse brukerne en av disse lisensene. Brukere som bare vil bruke (for eksempel lese og redigere) dette beskyttede data trenger ikke en lisens.

-   Office 365

-   Azure Rights Management Premium (tidligere Azure RMS frittstående)

-   Enterprise mobilitet Suite

-   RMS for enkeltpersoner

Bruk følgende deler for mer informasjon og påloggingsalternativer.

For lisensiering sammenligning av Azure RMS-funksjoner for betalte abonnementer, kan du se [tilbud for sammenligning av Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

### Office 365-abonnementet
[30-dagers prøveversjon: Enterprise-E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

Dette abonnementet er utformet for organisasjoner som ønsker å bruke Office online-tjenestene deres Information Rights Management-funksjonen, som bruker RMS Azure. Ikke alle Office 365-abonnementer inkluderer imidlertid Azure RMS.

|Alternativet-lisensiering|Det nødvendigste på Office 365|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 utdanning A1|Office 365 Enterprise E3<br /><br />Office 365 utdanning A3<br /><br />Office 365 regjeringen G3|Office 365 Enterprise E4<br /><br />Office 365 utdanning A4<br /><br />Office 365 regjeringen G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint-Plan 2|Utveksle elektroniske Plan 1<br />Exchange Online Plan 2|
|-----------------------------|----------------------------------|-------------------------------|-------------------------------------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------------|
|Informasjon om rettighetsbeskyttelse (IRM)|Nei|Nei|Nei|Ja|Ja|Nei|Nei|Nei|

### Azure Rights Management Premium abonnement
[Gratis 30-dagers prøveperiode](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

Dette abonnementet ble tidligere kalt Azure RMS frittstående, og den er utformet for organisasjoner som ønsker å bruke Azure RMS, men har ikke abonnement som inkluderer Azure RMS. For eksempel hvis du har et abonnement for Office 365 Business Essentials eller Office 365 Enterprise E1, disse abonnementene inkluderer ikke Azure RMS (se tabellen i foregående avsnitt). Hvis du vil bruke Azure RMS, kan du kjøpe et abonnement for Azure Rights Management Premium (eller kjøpe et annet abonnement, for eksempel Office 365 Enterprise E4, som inkluderer Azure RMS).

Hvis du vil ha mer informasjon, se [Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management).

Dette abonnementet tilbyr også en prøveperiode for deg å prøve ut Azure RMS for 25 brukere, gratis. Hvis abonnementet utgår før du kjøper en erstatning-abonnement, kan du se delen "Hva skjer når prøveperioden abonnement utløper?"

|Alternativet-lisensiering|Det nødvendigste på Office 365|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 utdanning A1|Office 365 Enterprise E3<br /><br />Office 365 utdanning A3<br /><br />Office 365 regjeringen G3|Office 365 Enterprise E4<br /><br />Office 365 utdanning A4<br /><br />Office 365 regjeringen G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint-Plan 2|Utveksle elektroniske Plan 1<br />Exchange Online Plan 2|
|-----------------------------|----------------------------------|-------------------------------|-------------------------------------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------------|
|Informasjon om rettighetsbeskyttelse (IRM)|Ja|Yes <sup>1</sup>|Ja|Ja|Ja|Ja|Ja|Ja|
<sup>1</sup> for Business Premium, er det noen begrensninger på klienten: Du kan beskytte innhold og bruke beskyttet innhold med RMS ved hjelp av Outlook Web App og RMS deling app. Du kan bruke beskyttet innhold ved hjelp av andre Office-programmer, som inkluderer Office Online og klientapplikasjoner for Office 365 Business Premium.

#### <a name="BKMK_TrialExpiryBehavior"></a>Hva skjer når prøveperioden abonnement utløper?
Hvis prøveabonnementet utløper, vil du miste tilgang til innhold som er beskyttet ved hjelp av prøveabonnementet for Azure RMS. Hvis du deretter kjøper et abonnement som støtter Azure RMS, er imidlertid access automatisk gjenopprettet.

Et unntak for å miste tilgang ved utløp er Hvis organisasjonen brukt Azure RMS med RMS for enkeltpersoner abonnementet før du fikk av prøveabonnementet. Deretter tilgang til tidligere beskyttet innhold forblir, selv etter at prøveversjonen abonnementet utløper.

### Enterprise mobilitet Suite-abonnementet
[Gratis 30-dagers prøveperiode](http://go.microsoft.com/fwlink/?LinkId=615385)

Dette abonnementet er utformet for organisasjoner som ønsker å bruke en kombinasjon av Azure Active Directory Premium, Windows Intune og Azure Rights Management. Hvis du vil ha mer informasjon, se den [Microsoft Enterprise mobilitet oversikt](http://go.microsoft.com/fwlink/?LinkId=615386).

|Alternativet-lisensiering|Det nødvendigste på Office 365|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 utdanning A1|Office 365 Enterprise E3<br /><br />Office 365 utdanning A3<br /><br />Office 365 regjeringen G3|Office 365 Enterprise E4<br /><br />Office 365 utdanning A4<br /><br />Office 365 regjeringen G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint-Plan 2|Utveksle elektroniske Plan 1<br />Exchange Online Plan 2|
|-----------------------------|----------------------------------|-------------------------------|-------------------------------------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------------|
|Informasjon om rettighetsbeskyttelse (IRM)|Ja|Yes <sup>1</sup>|Ja|Ja|Ja|Ja|Ja|Ja|
<sup>1</sup> for Business Premium, er det noen begrensninger på klienten: Du kan beskytte innhold og bruke beskyttet innhold med RMS ved hjelp av Outlook Web App og RMS deling app. Du kan bruke beskyttet innhold ved hjelp av andre Office-programmer, som inkluderer Office Online og klientapplikasjoner for Office 365 Business Premium.

### RMS for enkeltpersoner-abonnement
Dette abonnementet er utformet for personer i en organisasjon som ikke har implementert Azure RMS- eller AD RMS. Den lar disse personene lese innhold som er beskyttet av en organisasjon som bruker RMS Azure, og de kan også beskytte sitt eget innhold.

Hvis du vil ha mer informasjon, se [RMS for enkeltpersoner og Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

## <a name="BKMK_AzureADTenant"></a>Azure AD-katalogen
Du må ha en Azure AD-mappen som skal brukes RMS Azure. Du kan bruke kontoen din organisasjon for denne mappen til å logge på Azure Management Portal, der, for eksempel kan du konfigurere og administrere maler for Rights Management.

Hvis du ikke allerede har et abonnement på Azure for organisasjonen, kan du få en ved å registrere deg for en gratis prøveperiode.: Gå til den [Azure får startet](https://account.windowsazure.com/organization) side og følg instruksjonene.

Hvis du vil ha mer informasjon, kan du se følgende ressurser i Active Directory-Azure-dokumentasjonen:

-   [Hva er en Azure AD-katalog?](http://msdn.microsoft.com/en-us/library/185da266-58a9-43e6-9c66-2c8f702545c6)

-   [Hvordan Azure abonnementer som er knyttet til Azure AD](http://msdn.microsoft.com/en-us/library/edf05c2e-944a-4da5-a330-dc9dc479f127)

Hvis du vil integrere Azure AD-mappen med din lokale AD skoger, kan du se [Directory integration](http://msdn.microsoft.com/en-us/library/bf82bdff-2467-403b-8c1a-0e9eebcf31e8).

> [!NOTE]
> Hvis du har mobile enheter eller Mac datamaskiner godkjennes på lokaler ved hjelp av AD FS eller en tilsvarende godkjenningstjeneste:
> 
> -   Du må bruke AD FS på minimum serverversjonen av **Windows Server 2012 R2**, eller en alternativ godkjenningstjeneste som støtter protokollen OAuth 2.0.

### <a name="BKMK_MFA"></a>Multifaktorautentisering (MFA) og Azure RMS
Hvis du vil bruke flere faktor krever (MFA)-godkjenning med Azure RMS minst ett av følgende:

-   Office-2013 (minimum versjon):

    -   Hvis du har Office 2013, må du også installere den [9 juni 2015 oppdatering for Office-2013 (KB3054853)](https://support.microsoft.com/kb/3054853). For mer informasjon om dette oppdatere og hvordan moderne godkjenning gir Active Directory godkjenning biblioteket ADAL-baserte Logg 2013 for Office, kan du se [Office 2013 moderne godkjenning public preview annonsert](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)  i Office-bloggen.

-   Rights Management deling av programmer for Windows:

    -   Du må ha installert Minimumsversjonen av 1.0.1908.0, som kan bekreftes ved hjelp av Kontrollpanel, programmer og funksjoner. Hvis du vil ha mer informasjon om deling programmet, se  [Rettighetsadministrasjon deling av programmer for Windows](../Topic/Rights_Management_Sharing_Application_for_Windows.md).

-   Rights Management deling app for mobile enheter og Mac-datamaskiner:

    -   Kontroller at du har den siste versjonen som er installert. MFA støtte gikk inn i September 2015 utgivelsen av RMS deling app.

Konfigurer MFA løsningen:

-   For Microsoft-administrerte leiere (du har Azure Active Directory eller Office 365):

    -   Konfigurere Azure MFA for å gjennomføre MFA for brukere. For instruksjoner, se [Komme i gang med Azure multifaktorautentisering i skyen](https://azure.microsoft.com/documentation/articles/multi-factor-authentication-get-started-cloud/) fra Azure-dokumentasjonen.

        Hvis du vil ha mer informasjon om Azure MFA, kan du se [Hva er Azure multifaktorautentisering?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)

-   For medlemmer av organisasjonsnettverk leiere (du opererer federation servere lokale):

    -   Konfigurere din sammenslutningsservere for Azure Active Directory eller Office 365. For eksempel hvis du bruker AD FS, se [konfigurere flere godkjenningsmetoder for AD FS](https://technet.microsoft.com/library/dn758113.aspx) på TechNet.

        Hvis du vil ha mer informasjon om denne situasjonen, se  [det fungerer med Office 365 – identitet programmet nå strømlinjeformet](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) i Office-bloggen.

## <a name="BKMK_SupportedDevices"></a>Klientenheter som støtter Azure RMS
Bruk avsnittene nedenfor til å identifisere hvilke enheter som støtter Azure RMS (Rights Management), og hvilke RMS-funksjoner støtter de:

-   [Datamaskiner](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedComputers)

-   [Mobile enheter](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedMobileDevices)

-   [Enheten klientegenskaper](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities)

### <a name="BKMK_RMSSupportedComputers"></a>Datamaskiner
Følgende datamaskin operativsystemer støtter rettighetsbehandling Azure:

-   **Windows 7** (x 86, x 64)

-   **Windows 8** (x 86, x 64)

-   **Windows 8.1** (x 86, x 64)

-   **Windows 10** (x 86, x 64)

-   **Mac OS X**: Minste versjon av Mac OS X 10,8 (Mountain Lion)

### <a name="BKMK_RMSSupportedMobileDevices"></a>Mobile enheter
Følgende mobiltelefon operativsystemer støtter rettighetsbehandling Azure:

-   **Windows Phone-**: Windows Phone 8.1

-   **Android telefoner og tavler**: Minimumsversjonen av Android 4.0.3

-   **iPhone og iPad**: Minimumsversjonen av iOS 7.0

-   **Windows RT tavler**: Windows 8 RT, Windows 8.1 RT

### <a name="BKMK_ClientCapabilities"></a>Enheten klientegenskaper
Alle støttede klientenheter støtter for øyeblikket ikke alle RMS-funksjoner. Bruk tabellen nedenfor til å identifisere hvilke programmer støtter RMS-funksjoner og unntak.

Hvis ikke angitt, gjelder funksjonene som støttes både Azure RMS og AD RMS. AD RMS-støtte på iOS, Android, OS X og Windows Phone 8.1 krever i tillegg [Active Directory Rights Management Services Mobile enhetsutvidelse](http://technet.microsoft.com/library/a69ead9d-7dd3-4b38-9830-4728e9757341).

Informasjon om tabellkolonnene:

-   **Beskyttet PDF**: Filer som har filtypen .ppdf og som opprettes automatisk når du bruker RMS deling av programmet til å dele Office-filer og PDF-filer via e-post. Deling RMS-programmet inkluderer en leser for beskyttet PDF-filer. Tidligere, hvis du har opprettet PDF-filer som du har beskyttet ved hjelp av Azure RMS- eller AD RMS, kan du fortsette å lese disse filene på Windows, iOS og Android-enheter ved hjelp av Foxit Reader og Nitro Pro.

-   **E-post:** E-postklienter som er nevnt kan beskytte e-postmeldingen, som automatisk vil beskytte eventuelle vedlagte filer. I dette scenariet kan klientens forhåndsvisningsfunksjonen vise beskyttet innhold (meldinger og vedlegg) til godkjente mottakere. Hvis en e-postmelding seg selv ikke er beskyttet, men vedlegget er beskyttet, vises imidlertid ikke klientens forhåndsvisningsfunksjonen beskyttet vedlegg til godkjente mottakere.

-   **Andre filtyper**: Tekst-og bildefiler omfatter filer med filtypen, for eksempel txt, XML, JPG, og jpeg. Disse filene, endre deres filtypen når de opprinnelig er beskyttet av RMS, og blir skrivebeskyttet. Filer som ikke kan beskyttes opprinnelig har filtypen .pfile etter at de er Generelt beskyttet av RMS. Hvis du vil ha mer informasjon, se den [beskyttelsesnivåer – opprinnelig og generell](https://technet.microsoft.com/library/dn339003.aspx) og [støttede filtyper og filtypeangivelser i Filnavn](https://technet.microsoft.com/library/dn339003.aspx) inndelinger fra den [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx).

|**Enhet for operativsystemet**|Word, Excel, PowerPoint|Beskyttet PDF-fil|E-post|Andre filtyper|
|----------------------------------|---------------------------|---------------------|----------|------------------|
|**Windows**|Office 2010<br /><br />Office-2013<br /><br />Office Mobile apps (bare Azure RMS)<sup>1</sup><br /><br />Office Online<sup>2</sup>|Gaaiho Doc<br /><br />PDF-skrivebordsklienten GigaTrust for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF-leser<br /><br />RMS-deling app|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA)<br /><br />Windows Mail<sup>3</sup>|RMS deling av programmer for Windows: Tekst, bilder, pfile<br /><br />Siemens-JT2Go: JT-filer (bare Windows-10)|
|**iOS**|Office for iPad og iPhone<sup>4</sup><br /><br />Office Online<sup>2</sup><br /><br />TITUS dokumenter|Foxit Reader<br /><br />RMS deling app<sup>1</sup><br /><br />TITUS dokumenter|NitroDesk<br /><br />Outlook for iPad og iPhone<sup>3</sup><br /><br />OWA for iOS<br /><br />Sikre øyene IQProtector<sup>1</sup><br /><br />TITUS e-post|RMS deling app<sup>1</sup>: Tekst, bilder, pfile<br /><br />TITUS dokumenter: Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online<sup>2</sup>|GigaTrust App for Android<br /><br />Foxit Reader<br /><br />RMS deling app<sup>1</sup>|9Folders<br /><br />GigaTrust App for Android<br /><br />NitroDesk<br /><br />OWA for Android<sup>5</sup><br /><br />Samsung e-post (S3 og senere)<br /><br />Sikre øyene IQProtector<sup>1</sup><br /><br />TITUS klassifisering for mobil|RMS deling app<sup>1</sup>: Tekst, bilder, pfile|
|**OS X**|Office 2011 (bare AD RMS)<br /><br />2016 Office for Mac<br /><br />Office Online<sup>2</sup>|Foxit Reader<br /><br />RMS deling app<sup>1</sup>|Outlook 2011 (bare AD RMS)<br /><br />Outlook-2016 for Mac<br /><br />Outlook for Mac|RMS deling app<sup>1</sup>: Tekst, bilder, pfile|
|**Windows RT**|Office 2013 RT<br /><br />Office Online<sup>2</sup>|Støttes ikke|Outlook 2013 RT<br /><br />E-app for Windows<br /><br />Windows Mail<sup>3</sup>|Siemens-JT2Go: JT-filer|
|**Windows Phone 8.1**|Office Mobile (bare AD RMS)|RMS deling app<sup>1</sup>|Outlook Mobile|RMS deling app<sup>1</sup>: Tekst, bilder, pfile|
|**BlackBerry 10**|Støttes ikke|Støttes ikke|E-post til BlackBerry<sup>3</sup>|Støttes ikke|
<sup>1</sup> støtter visning av beskyttet innhold.

<sup>2</sup> støtter visning av beskyttet innhold i SharePoint Online, OneDrive for bedrifter og Outlook Web Access.

<sup>3</sup> bruker Exchange ActiveSync IRM, som må være aktivert av Exchange-administratoren. Brukere kan vise, svar og svar alle for beskyttede e-postmeldinger, men brukere ikke kan beskytte nye e-postmeldinger selv.

<sup>4</sup> støtter visning og redigering av beskyttede dokumenter. Hvis du vil ha mer informasjon, se følgende innlegget på bloggen for Office: [Azure Rights Management-støtte kommer til Office for iPad og iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

<sup>5</sup> for mer informasjon, se følgende innlegget i bloggen for Office: [OWA for Android er nå tilgjengelig på utvalgte enheter](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

> [!TIP]
> Hvis du vil ha mer informasjon om kommende RMS-støtte i Office for ulike plattformer, kan du se følgende innlegget fra Office-blogg: [Office overalt, overalt kryptering](http://blogs.office.com/2015/02/18/office-everywhere-encryption-everywhere/)

## <a name="BKMK_SupportedApplications"></a>Programmer som støtter Azure RMS
Følgende programmer støtter Azure RMS, noe som betyr at RMS er tett integrert i disse programmene ved hjelp av RMS-APIs til å støtte bruksbegrensninger. Disse programmene er også kjent som RMS-enlightened:

-   **Microsoft Office-programmer** (Word, Excel, PowerPoint og Outlook) fra følgende suites kan beskytte innhold ved hjelp av Azure RMS:

    -   Office 365 ProPlus

    -   Office 365 Enterprise E3

    -   Office 365 Enterprise E4

    -   Office Professional Plus 2016

    -   Office Professional Plus 2013

    -   Office Professional Plus 2010

    Andre versjoner av Office (med unntak av Office 2007) kan oppta beskyttet innhold.

    > [!NOTE]
    > Azure RMS med Office Professional Plus 2010 eller Office Professional 2010:
    > 
    > -   Krever rettighetsadministrasjon deling av programmer for Windows
    > -   Støttes ikke på Windows 10

-   **Rettighetsadministrasjon deling av programmer for Windows**

    Hvis du vil ha mer informasjon om programmet Rights Management deling for Windows, kan du se følgende ressurser:

    -   [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/dn339003.aspx)

    -   [Rights Management deling program Brukerhåndbok](http://technet.microsoft.com/library/dn339006.aspx)

-   **Rettighetsadministrasjon deling program for mobile plattformer**

    Hvis du vil ha mer informasjon om programmet Rights Management deling for mobile plattformer, kan du se følgende ressurser:

    -   Last ned den aktuelle app ved hjelp av koblingene på [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970)

    -   Hvis du administrerer mobile enheter ved hjelp av Microsoft Intune, kan du distribuere og konfigurere programmet på [iOS og Android enheter som en policy administrert app](https://technet.microsoft.com/library/dn878026.aspx).

    -   [Vanlige spørsmål om Microsoft-rettighetsadministrasjon deling program for Mobile plattformer](http://technet.microsoft.com/dn451248)

-   **Andre programmer som støtter RMS-APIs**:

    -   LOB programmer som er skrevet internt ved hjelp av RMS-SDK

    -   Programmer fra programvareleverandører som er skrevet ved hjelp av RMS-SDK

    Hvis du vil ha mer informasjon om SDK, se den [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx).

> [!IMPORTANT]
> Følgende programmer støttes ikke av Azure RMS:
> 
> -   Microsoft Office for Mac 2011
> -   Microsoft-OneDrive for bedrifter for SharePoint Server 2013
> -   XPS-visningsprogrammet
> 
> I tillegg har RMS deling program følgende begrensninger:
> 
> -   For Windows-datamaskiner: Krever en minimum versjon av Windows 7 Service Pack 1

Hvis du vil ha mer informasjon om hvordan disse programmene støtter Azure RMS, se [Hvordan programmer støtter Azure rettighetsbehandling](../Topic/How_Applications_Support_Azure_Rights_Management.md).

Hvis du vil ha informasjon om hvordan du konfigurerer dem, se [Konfigurere programmer for Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

## <a name="BKMK_SupportedServers"></a>Lokale servere som støtter Azure RMS
Følgende lokale server-produkter støttes med Azure RMS når du bruker Azure RMS-kobling, som fungerer som et grensesnitt med kommunikasjon (en relay) mellom den lokale servere og Azure RMS. Denne konfigurasjonen krever i tillegg at du konfigurerer katalogsynkronisering mellom Active Directory-skoger og Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Fil-servere som kjører Windows Server og bruke filen klassifisering infrastruktur (FCI)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Fordi filservere som kjører Windows Server 2008 R2 ikke har en innebygd fil management oppgavehandling å bruke RMS-beskyttelse, kan du ikke bruke RMS-koblingen for dette scenariet. Du kan imidlertid bruke filen klassifisering infrastruktur og Azure RMS på disse operativsystemene Hvis du konfigurerer en oppgave for egendefinert fil for å kjøre en kjørbar fil eller skript som kan beskytte filer ved hjelp av Azure RMS. For eksempel et Windows PowerShell-skript som bruker den [RMS beskyttelse cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Du kan også bruke disse cmdlets med servere som kjører senere versjoner av Windows Server, med fordelen at disse cmdlets kan beskytte alle filtyper. RMS-koblingen beskytter Office-filer. For hvordan-instruksjoner, se [RMS-beskyttelse med Windows Server-filen klassifisering infrastruktur &#40;FCI&#41;](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md).

RMS-koblingen støttes på Windows Server 2012 R2, Windows Server 2012 og Windows Server 2008 R2.

Hvis du vil ha mer informasjon om hvordan du konfigurerer RMS-kontakt for disse lokale servere, se [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

## Se også
[Komme i gang med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

