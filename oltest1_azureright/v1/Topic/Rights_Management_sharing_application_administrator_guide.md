---
description: na
keywords: na
title: Rights Management sharing application administrator guide
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
---
# Rights Management deling program administratorh&#229;ndboken
Bruk informasjonen nedenfor hvis du er ansvarlig for Microsoft Rights Management deling av programmer på et bedriftsnettverk, eller hvis du vil ha mer teknisk informasjon enn det som er i den [Rights Management deling program Brukerhåndbok](../Topic/Rights_Management_sharing_application_user_guide.md) eller [Vanlige spørsmål om Microsoft Rights Management deling av programmer for Windows](http://go.microsoft.com/fwlink/?LinkId=303971):

-   [Automatisk distribusjon for Microsoft Rights Management program for deling](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ScriptedInstall)

    -   [Kontrollerer installasjonen vellykket](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)

    -   [Avinstallere kommandoer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_uninstallscripted)

    -   [Undertrykke automatiske oppdateringer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SuppressAutomaticUpdates)

    -   [Azure RMS: Konfigurere sporing av dokument](#BKMK_DocumentTracking)

    -   [AD RMS: Støtte for flere e-domener i organisasjonen](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains)

-   [Teknisk oversikt for Microsoft Rights Management program for deling](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_AdminOverview)

    -   [Beskyttelsesnivåer – opprinnelig og generisk](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection)

    -   [Støttede filtyper og filtypeangivelser i filnavn](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes)

    -   [Hvis du endrer standardnivået for beskyttelse av filer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection)

> [!TIP]
> Hvis du er ny til RMS-deling-app, eller se for mer informasjon, se [hvordan RMS beskytter alle filtyper – ved hjelp av RMS deling app](https://curah.microsoft.com/191031/how-rms-protects-all-file-types-by-using-the-rms-sharing-app).

RMS deling programmet egner seg best til å arbeide med Azure RMS, fordi denne konfigurasjonen distribusjon støtter sending beskyttet vedlegg til brukere i en annen organisasjon, og alternativer, for eksempel e-postmeldinger og dokumentsporing med tilbakekalling.  Men med begrensninger fungerer det også med den lokale versjonen, AD RMS. En omfattende sammenligning av funksjoner som støttes av Azure RMS og AD RMS, kan du se [sammenligne Azure Rights Management og AD RMS](https://technet.microsoft.com/library/jj739831.aspx). Hvis du har AD RMS, og du vil overføre til Azure RMS, kan du se [migrering fra AD RMS til Azure Rights Management](https://technet.microsoft.com/library/dn858447.aspx).

## <a name="BKMK_ScriptedInstall"></a>Automatisk distribusjon for Microsoft Rights Management program for deling
Windows-versjonen av RMS deling programmet støtter en skriptet installasjon, noe som gjør det egnet for distribusjon i bedrifter.

Bare forutsetningene for installasjon er at datamaskinene kjører en minimumsversjon av Windows 7 Service Pack 1, og at Microsoft Framework, minimum versjon 4.0 er installert. Hvis du må installere Microsoft .NET Framework 4.0, kan du [laste det ned for installasjon fra Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=17718).

#### Laste ned RMS deling program for automatisk distribusjon

1.  Gå til den [Microsoft Rights Management deling av programmer for Windows](http://www.microsoft.com/download/details.aspx?id=40857) fra Microsoft Download Center, og klikk **Last ned**.

2.  Velg og Last ned filene du trenger. Det finnes to installasjonspakker for klient: én for Windows 64-bit (Microsoft Rights Management deling program x64.zip) og en annen for 32-biters (Microsoft Rights Management deling program x86.zip).

3.  Pakk ut filer fra komprimerte installasjonspakker, for eksempel ved å dobbeltklikke dem.. Kopier de utpakkede filene til en nettverksplassering som klientdatamaskiner kan få tilgang til.

Installasjonspakker for RMS deling programmet støtter ulike distribusjonsscenarier, og inkluderer følgende:

|Beskrivelse|Distribusjonsscenariet|
|---------------|--------------------------|
|Microsoft Online Sign-In Assistant|Kreves for følgende:<br /><br />-   Office 2010 og Azure RMS<br />-   Office-2013 og Azure RMS Hvis du ikke har installert den [9 juni 2015 oppdatering for Office-2013](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Hurtigreparasjon for Office (KB 2596501)|Kreves for følgende:<br /><br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS|
|For å aktivere AD RMS-klient 1.0 til å fungere med Azure RMS (KB 2843630)|Kreves for følgende:<br /><br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS|
|AD RMS-klienten og RMS deling av program|Kreves for følgende:<br /><br />-   2016 for Office eller Office-2013 og Azure RMS eller Active Directory-RMS<br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS<br />-   Deling av programmer og Office-tillegg bare RMS|
|Office-tillegg for båndet|Kreves for følgende:<br /><br />-   2016 for Office eller Office-2013 og Azure RMS eller Active Directory-RMS<br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS<br />-   Deling av programmer og Office-tillegg bare RMS|
|Forberedelsesverktøy for Azure Active Directory Rights Management|Kreves for følgende:<br /><br />-   Office 2010 og Azure RMS|
Bruk følgende fremgangsmåter til å identifisere kommandoer som kreves for å distribuere RMS deling program for disse distribusjonsscenariene:

-   **2016 for Office eller Office-2013 og Azure RMS eller Active Directory-RMS**

    Brukerne kjører Office-2016 eller Office 2013, organisasjonen bruker Azure RMS eller Active Directory-RMS, og brukere kan samarbeide med andre organisasjoner som bruker RMS Azure eller Active Directory-RMS.

-   **Office 2010 og Azure RMS**

    Brukerne kjører Office 2010, organisasjonen bruker Azure RMS, og brukere kan samarbeide med andre organisasjoner som bruker RMS Azure eller Active Directory-RMS.

-   **Office 2010 og Active Directory-RMS**

    Brukerne kjører Office 2010, organisasjonen bruker AD RMS, og brukere kan samarbeide med andre organisasjoner som bruker RMS Azure.

-   **Deling av programmer og Office-tillegg bare RMS**

    Brukerne kjører Office-2016, 2013 Office eller Office 2010, organisasjonen bruker AD RMS og brukerne trenger ikke å samarbeide med andre organisasjoner som bruker RMS Azure. Denne installasjonen kan du installere bare deling program- og Office-tillegg.

> [!NOTE]
> I disse scenariene, hvis organisasjonen kjører AD RMS, kan brukerne motta beskyttet innhold fra andre organisasjoner som bruker Azure RMS, men brukerne kan ikke sende beskyttet innhold til brukere i en organisasjon som bruker RMS Azure. Hvis organisasjonen kjører Azure RMS, kan brukerne sende og motta beskyttet innhold fra andre organisasjoner.

For å fullføre installasjonen for hver prosedyre, datamaskinen må startes på nytt. Du kan starte en automatisk omstart ved hjelp av en kommando, for eksempel avslutning /i.

#### Distribuere RMS deling program for 2016 for Office eller Office-2013 og Azure RMS eller Active Directory-RMS

-   På hver datamaskin du vil installere RMS deling av programmer og relaterte komponenter, kan du kjøre følgende kommando med utvidede rettigheter:

    ```
    setup.exe /s
    ```

For å bekrefte suksess, kan du se den [Kontrollerer installasjonen vellykket](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) delen i dette emnet.

#### Distribuere RMS deling av programmer for Office 2010 og Azure RMS

1.  Du må være global administrator for leietakeradministrasjon av Office 365 eller Azure Active Directory slik at du kan få din organisasjons sertifisering URL-adresse ved å kjøre verktøyet Azure Active Directory Rights Management preparation. Du må kjøre dette verktøyet bare én gang på en enkelt datamaskin. Du vil bruke for sertifisering URL-adresse når du installerer RMS deling program på hver datamaskin:

    1.  Logge på en datamaskin ved hjelp av en lokal administratorkonto.

    2.  På datamaskinen, [laste ned og installere Microsoft Online Sign i hjelperen](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Kjør følgende kommando for å se vises på skjermen for sertifisering URL-adresse, som du deretter kan kopiere og lagre for neste trinn:

        -   For 8.1 for Windows og Windows 8, 64-biters:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   For 8.1 for Windows og Windows 8, 32-biters:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   For Windows 7, 64-biters:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Denne kommandoen kan bli bedt om å angi påloggingsinformasjonen for Azure. Hvis datamaskinen ikke er koblet til et domene, vil du bli spurt. Hvis datamaskinen er koblet til et domene, kan det hende at verktøyet kan du bruke bufret legitimasjon.

2.  På hver datamaskin du vil installere RMS deling av programmet, kan du kjøre følgende kommando med utvidede rettigheter:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  På hver datamaskin du vil installere RMS deling av programmet, må brukere kjøre følgende kommando (trenger ikke utvidede rettigheter). Det finnes ulike måter å oppnå dette, inkludert ber brukerne til å kjøre kommandoen (for eksempel en kobling i en e-postmelding eller en kobling på skrivebordet Hjelp-portalen) eller du kan legge den til sine påloggingsskript:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

For å bekrefte suksess, kan du se den [Kontrollerer installasjonen vellykket](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) delen i dette emnet.

#### Distribuere RMS deling av programmer for Office 2010 og Active Directory-RMS

1.  På hver datamaskin du vil installere RMS deling av programmet, kan du kjøre følgende kommando med utvidede rettigheter:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  På hver datamaskin du vil installere RMS deling av programmet, må brukere kjøre følgende kommando (trenger ikke utvidede rettigheter). Det finnes ulike måter å oppnå dette, inkludert ber brukerne til å kjøre kommandoen (for eksempel en kobling i en e-postmelding eller en kobling på skrivebordet Hjelp-portalen) eller du kan legge den til sine påloggingsskript:

    -   For Windows 10 8.1 for Windows og Windows 8, 64-biters:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   For Windows 10 8.1 for Windows og Windows 8, 32-biters:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   For Windows 7, 64-biters:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

For å bekrefte suksess, kan du se den [Kontrollerer installasjonen vellykket](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) delen i dette emnet.

#### Installere RMS deling av programmer og Office-tillegg bare

1.  Installere AD RMS-klienten og RMS deling av programmer ved å bruke følgende kommando:

    -   For 64-biters Windows:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   For 32-biters Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    For eksempel: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Installere Office-tillegget ved hjelp av følgende kommandoer:

    -   For 64-biters versjon av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   For 32-biters versjon av Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    For eksempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

For å bekrefte suksess, kan du se den [Kontrollerer installasjonen vellykket](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) delen i dette emnet.

### <a name="BKMK_verifyscripted"></a>Kontrollerer installasjonen vellykket
Du kan bruke loggfilene for installasjonen for å kontrollere at installasjonen blir vellykket.

##### Å bekrefte installasjonen suksess for RMS deling program for 2016 for Office eller Office-2013 og Azure RMS eller Active Directory-RMS

-   For å bekrefte suksess for Setup.exe-kommandoen på hver datamaskin, kan du søke etter loggfilen for installasjonen **RMInstaller.log** i den *%temp%\RMS_installer_ &lt; guid &gt;* -mappen, og finn deretter sluttkoden.

    En vellykket installasjon har en sluttkode på 0 og et annet tall indikerer en mislykket installasjon.

    Filnavnet for eksempel: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

##### Å bekrefte installasjonen suksess for deling av programmer for Office 2010 og Azure RMS RMS

1.  For å bekrefte suksess for Setup.exe-kommandoen på hver datamaskin, kan du søke etter loggfilen for installasjonen **RMInstaller.log** i den *%temp%\RMS_installer_ &lt; guid &gt;* -mappen, og finn deretter sluttkoden.

    En vellykket installasjon har en sluttkode på 0 og et annet tall indikerer en mislykket installasjon.

    Filnavnet for eksempel: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  For å bekrefte suksess for kommandoen RMSSetup.exe, må brukeren ha følgende filer opprettet i deres *%localappdata%\microsoft\drm* mappen:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   LOGIKK-&#42;.drm

    Eksempel på en CLC-&#42;.drm-fil:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf; k5b11; k4a10; kac15; k29b2b6980f4c} .drm**

##### Å bekrefte installasjonen suksess for RMS deling av programmer for Office 2010 og Active Directory-RMS

1.  For å bekrefte suksess for Setup.exe-kommandoen på hver datamaskin, kan du søke etter loggfilen for installasjonen i den *%temp%\RMS_installer_ &lt; guid &gt;* -mappen, og identifisere sluttkoden.

    En vellykket installasjon har en sluttkode på 0 og et annet tall indikerer en mislykket installasjon.

    Filnavnet for eksempel: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  For å bekrefte suksess av kommandoen aadrmprep.exe på hver datamaskin, kan du søke etter følgende tekst i loggfilen for installasjonen: **aadrmprep.exe ble avsluttet med statusen vellykket**

    > [!NOTE]
    > Noen ganger kan kan denne installasjonen kjøre to ganger. den første forekomsten mislykkes, og andre er vellykket.

    Hvis du vil kontrollere manuelt registerendringene som dette verktøyet gjør, er de som følger:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn: HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn: HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        ved = "&lt; sertifisering url &gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        Standard = "&lt; default_user &gt;"

##### Å bekrefte installasjonen suksess for deling av programmer og Office-tillegg bare RMS

1.  For å bekrefte suksess for Setup_ipviewer.exe-kommandoen, kan du søke etter følgende tekst i loggfilen for installasjonen: **Installasjonen var vellykket eller feil status: 0**

    Eksempel linjer fra en vellykket installasjon:

    **MSI (s) (F0:B8) [14:19:57:854]: Produkt: Active Directory Rights Management Services Client 2.1 - installasjonen er fullført.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer installerte produktet. Produktnavn: Active Directory Rights Management Services Client 2.1. Produktversjon: 1.0.1179.1. Produktspråket: 1033. Produsent: Microsoft Corporation. Installasjonen var vellykket eller feil status: 0.**

2.  Søk etter følgende tekst i loggfilen for installasjonen for å bekrefte suksess for det Office-tillegget, på hver datamaskin: **Installasjonen var vellykket eller feil status: 0**

    Eksempel linjer fra en vellykket installasjon:

    **MSI (s) (9C: 88) [18:49:04:007]: Produkt: Tillegg for Microsoft RMS Office - Installasjonen er fullført.**

    **MSI (s) (9C: 88) [18:49:04:007]: Windows Installer installerte produktet. Produktnavn: Microsoft RMS Office-tillegg. Produktversjon: 1.0.7. Produktspråket: 1033. Produsent: Microsoft. Installasjonen var vellykket eller feil status: 0.**

### <a name="BKMK_uninstallscripted"></a>Avinstallere kommandoer
Ikke alle installasjonskommandoer som er nødvendige for disse distribusjonene støtte en avinstallasjon-kommando. Du kan avinstallere AD RMS-klienten og deling programmet, og du kan avinstallere Office-tillegg. Bruk følgende kommandoer for å avinstallere disse elementene.

##### Slik avinstallerer du AD RMS-klienten og RMS deling av program

-   Bruk følgende kommandoer:

    -   For 64-biters Windows:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   For 32-biters Windows:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

##### Slik avinstallerer du Office-tillegg

-   Bruk følgende kommandoer:

    -   For 64-biters versjon av Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   For 32-biters versjon av Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

### <a name="BKMK_SuppressAutomaticUpdates"></a>Undertrykke automatiske oppdateringer
Som standard er brukere beskjed hvis det er en nyere versjon av programmet RMS deling, og du blir bedt om å laste den ned. Du kan undertrykke denne meldingen ved å redigere følgende registernøkkel:

1.  Gå til **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** og hvis den ikke allerede finnes, oppretter du en ny nøkkel kalt **RmsSharingApp**.

2.  Velg **RmsSharingApp**, opprette en ny DWORD-verdi av **AllowUpdatePrompt**, og Sett verdien til **0**.

Fordi deling RMS-programmet ikke støttes av WSUS, kan du bruke følgende metode til å teste alle nye versjoner av RMS deling programmet før du distribuerer den til alle brukere:

1.  På datamaskinene til alle brukerne, kan du kjøre et skript for å undertrykke automatiske oppdateringer. På datamaskiner som administratorer bruker til å teste nye versjoner, må du ikke kjøre dette skriptet.

2.  Når en ny versjon er tilgjengelig, kan administratorer laste ned og teste den.

3.  Når testingen er fullført, og eventuelle problemer som er løst, distribuere den nyeste versjonen for alle brukere ved hjelp av automatisk distribuere instruksjonene i denne håndboken.

### <a name="BKMK_DocumentTracking"></a>Azure RMS: Konfigurere sporing av dokument
Hvis du har en [abonnement som støtter dokumentet sporing](https://technet.microsoft.com/en-us/dn858608), den dokumentsporing område er aktivert som standard for alle brukere i organisasjonen.  Viser dokumentet sporing av informasjon, for eksempel e-postadresser til personer som forsøkte å få tilgang til beskyttede dokumenter som brukerne delt, da disse personene prøvde å få tilgang til dem, og deres plassering. Hvis du viser denne informasjonen er forbudt i din organisasjon på grunn av kravene, kan du deaktivere tilgang til dokumentet sporingsområdet ved hjelp av den  [Deaktiver AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) cmdleten. Du kan aktivere tilgang til området på nytt når som helst ved hjelp av den [Aktiver AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), og du kan kontrollere om tilgang er aktivert eller deaktivert ved hjelp av [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

 Hvis du vil kjøre disse cmdlets, må du ha minst versjon **2.3.0.0** av Azure RMS-modul for Windows PowerShell.  For å lese installasjonsinstrukser, kan du se [installere Windows PowerShell for Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx).

> [!TIP]
> Hvis du tidligere har lastet ned og installert modulen, kontrollerer du versjonsnummeret ved å kjøre: `(Get-Module aadrm –ListAvailable).Version`

Følgende URLer brukes for dokumentsporing og må være tillatt (for eksempel legge dem til i klarerte områder hvis du bruker Internet Explorer med utvidet sikkerhet):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > denne URL-adressen er for Bing-kart.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### <a name="BKMK_FederatedDomains"></a>AD RMS: Støtte for flere e-domener i organisasjonen
Hvis du bruker AD RMS, og brukerne i organisasjonen har flere e-domener, må kanskje som et resultat av en sammenslåing eller anskaffelse, du gjøre følgende register redigere:

1.  Gå til **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** og hvis den ikke allerede finnes, oppretter du en ny nøkkel kalt **RmsSharingApp**.

2.  Velg **RmsSharingApp**, opprette en ny Multistrengverdi som heter **FederatedDomains**, og legg deretter til domener og underdomener som organisasjonen din bruker. Jokertegn støttes ikke.

    For eksempel: Har en standard e-post domene av selskapet Coho Vineyard &amp; Vingård **cohovineyardandwinery.com**, men de også bruke e-post-domener som følge av fusjoner, **cohowinery.com**, **eastcoast.cohowinery.com**, og **cohovineyard**. For den **FederatedDomains** Verdidata administratoren angir: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Hvis du ikke gjør dette endre registret, kan ikke brukere bruke innhold som er beskyttet av andre brukere i organisasjonen. Rediger dette registret er ikke nødvendig hvis du bruker Azure RMS.

## <a name="BKMK_AdminOverview"></a>Teknisk oversikt for Microsoft Rights Management program for deling
Microsoft Rights Management deling av programmet er et valgfritt nedlastbare program for Microsoft Windows og andre plattformer som inneholder følgende:

-   Beskyttelse av en enkelt fil eller bulk beskyttelse av flere filer samt alle filer i en valgt mappe.

-   Full støtte for beskyttelse av en hvilken som helst type fil og en innebygd viewer for vanlige filtyper for tekst og bilde.

-   Generell beskyttelse for filer som ikke støtter RMS-beskyttelse.

-   Full interoperabilitet med filer som er beskyttet ved hjelp av Office Information Rights Management (IRM).

-   Full interoperabilitet med PDF-filer som er beskyttet ved hjelp av SharePoint, FCI og støttede PDF-redigeringsverktøy.

Microsoft Rights Management deling programmet bruker den nye [AD RMS-klienten 2.1 runtime](http://www.microsoft.com/download/details.aspx?id=38396). Ved hjelp av gir sluttbrukere funksjonaliteten for AD RMS 2.1, Microsoft Rights Management deling programmet en enkel beskyttelse og forbruk opplevelse.

Du kan opprinnelig beskytte dokumenter ved hjelp av Office 2010 og sende dem til personer i et annet firma, som kan deretter bruke dem ved hjelp av Azure RMS i oktober 2013-utgaven av RMS. I tillegg med denne utgivelsen, kan Hvis du bruker AD RMS i kryptografiske modus 2, du bruke RMS for enkeltpersoner og forbruker innhold fra personer i et annet firma som bruker RMS Azure. Hvis du vil ha mer informasjon om kryptografiske modus 2, kan du se [AD RMS kryptografiske modi](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

### <a name="BKMK_LevelsofProtection"></a>Beskyttelsesnivåer – opprinnelig og generisk
Microsoft Rights Management deling programmet støtter beskyttelse på to forskjellige nivåer, som beskrevet i følgende tabell.

|Typen beskyttelse|Opprinnelig|Generisk|
|---------------------|---------------|------------|
|Beskrivelse|Tekst, bilde, Microsoft Office (Word, Excel, PowerPoint)-filer, PDF-filer og andre filtyper for programmer som støtter AD RMS, gir innebygd beskyttelse en sterk grad av beskyttelse som inkluderer både kryptering og gjennomføring av tillatelser (tillatelser).|For alle andre programmer og filtyper gir generell beskyttelse et nivå av beskyttelse som inkluderer både innkapsling for filen med filtypen .pfile og godkjenning til å kontrollere om en bruker har tillatelse til å åpne filen.|
|Beskyttelse|Filene er fullstendig kryptert, og fremtvinges beskyttelsen på følgende måter:<br /><br />-   Før beskyttet innhold gjengis, må det være vellykket godkjenning for de som mottar filen via e-post eller får tilgang til den via tillatelsene for filen eller delt ressurs.<br />-   I tillegg håndheves bruksrettigheter og policy angitt av innholdseieren når filene er beskyttet fullstendig når innholdet gjengis i IP-visningsprogram (for beskyttede filer i tekst- og bildefiler) eller det tilknyttede programmet (for alle andre filtyper som støttes).|Filbeskyttelse trer i kraft på følgende måter:<br /><br />-   Før beskyttet innhold gjengis, vellykket godkjenning må finne sted for de som er autorisert til å åpne filen, og det er gitt tilgang til den. Hvis godkjenning mislykkes, åpnes ikke filen.<br />-   Bruksrettigheter og policy angitt av innholdseieren vises for å informere autoriserte brukere til den tiltenkte bruk av policyen.<br />-   Overvåk logging av autoriserte brukere åpner og få tilgang til filer forekommer, kan du imidlertid ingen bruksrettigheter håndheves ved å støtte programmer.|
|Standard for filtyper|Dette er standard beskyttelsesnivå for følgende filtyper:<br /><br />-   Tekst-og bildefiler<br />-   Filer for Microsoft Office (Word, Excel, PowerPoint)<br />-   (PDF) Portable document format<br /><br />Hvis du vil ha mer informasjon, se delen nedenfor [Støttede filtyper og filtypeangivelser i filnavn](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes).|Dette er standard-beskyttelse for alle andre filtyper (for eksempel .vsdx, RTF og så videre) ikke støttes gjennom full beskyttelse.|
Du kan endre standard beskyttelsesnivået som gjelder for programmet RMS deling. Du kan endre standardnivået for opprinnelig til generiske, fra generiske til opprinnelig, og forhindrer selv RMS dele programmet i å bruke beskyttelse. Hvis du vil ha mer informasjon, se den [Hvis du endrer standardnivået for beskyttelse av filer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection) delen i dette emnet.

### <a name="BKMK_SupportFileTypes"></a>Støttede filtyper og filtypeangivelser i filnavn
Tabellen nedenfor viser filtypene som støttes internt av deling Microsoft Rights Management-programmet. Den opprinnelige filtypen endres når opprinnelig beskyttet brukes, og disse filene blir skrivebeskyttet for disse filtypene.

I tillegg når RMS deling programmet opprinnelig beskytter en Word, Excel eller PowerPoint-fil som beskytter brukere ved å dele, denne handlingen oppretter automatisk en annen fil som er en kopi av opprinnelige med samme filnavn, men med en **.ppdf** filtype ¹. Denne versjonen av filen sikrer at mottakere som installerer RMS deling programmet alltid kan åpne filen med innebygd beskyttelse som er brukt.

For filer som er generisk beskyttet, er alltid den opprinnelige filtypen endres til .pfile.

> [!WARNING]
> Hvis du har brannmurer, web-proxyer eller sikkerhetsprogramvare som undersøke og iverksette tiltak i henhold til filtyper, må du kanskje konfigurere disse for å støtte disse nye filtyper.

|Opprinnelige filtypen.|RMS-beskyttet filtypen|
|--------------------------|--------------------------|
|txt|.ptxt|
|XML|.pxml|
|JPG|.pjpg|
|JPEG|.ppng|
|PDF|.ppdf|
|PNG|.ppng|
|TIFF|.ptiff|
|BMP|.pbmp|
|GIF|.pgif|
|.giff|.pgiff|
|JPE|.pjpe|
|JFIF|.pjfif|
|.jif|.pjif|
|.JT|.pjt|
¹ PDF-gjengivelse drives av Foxit. Copyright © 2003 – 2014 Foxit Corporation.

Tabellen nedenfor viser en liste over filtyper som Microsoft Rights Management deling programmet støtter i 2016 for Microsoft Office, Office-2013 og Office 2010. For disse filene filtypen ikke endres etter at filen er beskyttet av RMS.

|Filtyper som støttes av Office|Filtyper som støttes av Office|
|----------------------------------|----------------------------------|
|DOC<br /><br />et DOCM<br /><br />DOCX<br /><br />dot<br /><br />dotm<br /><br />dotx<br /><br />.potm<br /><br />potx<br /><br />PPS<br /><br />.ppsm<br /><br />PPSX<br /><br />ppt<br /><br />pptm|PPTX<br /><br />.thmx<br /><br />xla<br /><br />.xlam<br /><br />XLS<br /><br />xlsb<br /><br />xlt<br /><br />xlsm<br /><br />XLSX<br /><br />xltm<br /><br />xltx<br /><br />XPS|

### <a name="BKMK_ChangeDefaultProtection"></a>Hvis du endrer standardnivået for beskyttelse av filer
Du kan endre hvordan RMS deling program beskytter filene ved å redigere registret. Du kan for eksempel tvinge filer som støtter ukomprimert beskyttelse skal beskyttes av programmet RMS deling generisk.

Årsaker til hvorfor du vil gjøre dette:

-   Å sikre at alle brukere kan åpne filen fra sine mobile enheter.

-   Hvis du vil sikre at alle brukere kan åpne filen hvis de ikke har et program støtter som ukomprimert beskyttelse.

-   Å få plass til sikkerhetssystemer som håndtere filer etter deres filtype og kan konfigureres for å tilpasse .pfile-filtypen, men kan ikke konfigureres på nytt for å få plass til flere filtyper for native beskyttelse.

På samme måte kan du tvinge RMS deling programmet til opprinnelig beskyttelse gjelder filer som vil ha generell beskyttelse brukes som standard. Dette kan være nødvendig hvis du har et program som støtter RMS-APIs – for eksempel, en line-of-business-applikasjon som er skrevet av din interne utviklere eller et program som er kjøpt fra en uavhengig programvareleverandør (ISV).

Du kan også tvinge RMS deling av programmet til å blokkere beskyttelse av filer (ikke Bruk opprinnelig beskyttelse eller Generell beskyttelse). Dette kan for eksempel være nødvendig hvis du har et automatisert program eller tjeneste som må være i stand til å åpne en bestemt fil for å behandle innholdet. Når du blokkerer beskyttelse for en filtype, kan ikke brukere bruke RMS deling av programmet til å beskytte en fil med filtypen. Når de prøver, kan de se en melding om at administratoren har forhindret beskyttelse, og de må avbryte sin handling for å beskytte filen.

Hvis du vil konfigurere RMS deling av programmet til å bruke Generell beskyttelse for alle filer som har innebygd beskyttelse som brukes som standard, kan du gjøre følgende redigeringene i registret:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Opprette en ny nøkkel kalt **&#42;**.

    Denne innstillingen angir filer med en hvilken som helst filtype.

2.  I den nye nøkkelen til **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\ &#42;**, opprette en ny strengverdi (REG_SZ) kalt **kryptering** som har dataverdien **Pfile**.

    Denne innstillingen gir RMS deling Applikasjonsbeskyttelse for Bruk generisk.

Disse to innstillingene føre RMS deling Bruk generisk Applikasjonsbeskyttelse til alle filer som har filtypen. Hvis dette er målet ditt, kreves ingen ytterligere konfigurasjon. Du kan imidlertid definere unntak for bestemte filtyper, slik at de fortsatt opprinnelig er beskyttet. Hvis du vil gjøre dette, må du gjøre tre ekstra registret endringer for hver filtype:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Legge til en ny nøkkel som har navnet på filtypen (uten forutgående perioder).

    For eksempel for filer som har en DOCX filtype, oppretter du en nøkkel kalt **DOCX**.

2.  I nøkkelen nylig er lagt til filen type (for eksempel **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), opprette en ny DWORD-verdi kalt **AllowPFILEEncryption** som har en verdi på **0**.

3.  I nøkkelen nylig er lagt til filen type (for eksempel **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), opprette en ny strengverdi kalt **kryptering** som har en verdi på **opprinnelige**.

Som et resultat av disse innstillingene beskyttes generisk alle filer unntatt filer som har filtypen DOCX-filen navnet som opprinnelig er beskyttet av RMS deling programmet.

Gjenta disse tre trinnene for andre filtyper som du vil definere som unntak fordi de støtter opprinnelig beskyttelse, og du vil ikke være generisk beskyttet av RMS deling programmet.

Du kan gjøre lignende registret endringene for andre scenarier ved å endre verdien for den **kryptering** streng som støtter følgende verdier:

-   **Pfile**: Generell beskyttelse

-   **Opprinnelig**: Innebygd beskyttelse

-   **Off**: Blokk-beskyttelse

## Se også
[Rights Management deling program Brukerhåndbok](../Topic/Rights_Management_sharing_application_user_guide.md)

