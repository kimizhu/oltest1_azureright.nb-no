---
description: na
keywords: na
title: Planning and Implementing Your Azure Rights Management Tenant Key
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
---
# Planlegging og implementering av Azure Rights Management leier n&#248;kkelen
Bruk informasjonen i dette emnet for å hjelpe deg med å planlegge og administrere Rights Management service (RMS) leier nøkkelen for Azure RMS. I stedet for Microsoft håndtering leier nøkkelen (standard), kan du for eksempel vil til å administrere din egen leier nøkkel slik at de samsvarer med spesifikke regler som gjelder for organisasjonen.  Behandle leier nøkkelen kalles også for å bringe din egen nøkkel eller BYOK som.

> [!NOTE]
> RMS leier nøkkelen er også kjent som nøkkelen Server LISENSGIVEREN sertifikat (SLC). RMS Azure opprettholder én eller flere taster for hver organisasjon som abonnerer på Azure RMS. Hver gang en nøkkel brukes til RMS i en organisasjon (for eksempel brukernøkler datamaskinen nøkler, krypteringsnøkler for dokument), lenker de kryptografisk RMS leier-tasten.

**Med et raskt blikk:** Bruk tabellen nedenfor som en rask gjennomgang av topologien for anbefalte leier. Deretter bruker du flere inndelinger for mer informasjon.

Hvis du distribuerer Azure RMS ved hjelp av en nøkkel for klientadministrasjon som administreres av Microsoft, kan du endre til BYOK senere. Men kan ikke du endre Azure RMS leier nøkkelen som er fra BYOK som styres av Microsoft.

|Forretningsbehov|Anbefalte leier viktige topologi|
|--------------------|------------------------------------|
|Distribuere Azure RMS raskt og uten å kreve spesiell maskinvare|Styrt av Microsoft|
|Trenger full IRM-funksjonalitet i Exchange Online med Azure RMS|Styrt av Microsoft|
|Nøklene er opprettet av deg og beskyttet i hardware sikkerhetsmodul (HSM)|BYOK<br /><br />For øyeblikket er vil denne konfigurasjonen resultere i redusert IRM-funksjonalitet i Exchange Online. Hvis du vil ha mer informasjon, se den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) delen.|
Bruk avsnittene nedenfor til å hjelpe deg å velge hvilken tast leier topologi skal brukes, forstå leier viktige livssyklusen, hvordan du implementerer bringe din egen nøkkel (BYOK), og hvilke tiltak du skal gjøre neste:

-   [Choose your tenant key topology: Managed by Microsoft (the default) or managed by you (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ChooseTenantKey)

-   [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing)

-   [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK)

-   [Next steps](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_NextSteps)

## <a name="BKMK_ChooseTenantKey"></a>Velg din leier viktige topologi: Styrt av Microsoft (standard) eller styrt av deg (BYOK)
Bestemme hvilke viktige topologi for leieradministrasjon er best for din organisasjon. Som standard Azure RMS genererer leier-nøkkelen, og behandler de fleste aspektene av viktige livssyklusen for leietakeradministrasjon. Dette er det enkleste alternativet med de laveste administrative administrasjonskostnader. I de fleste tilfeller trenger du også ikke å vite at du har en nøkkel for leietakeradministrasjon. Du registrere bare deg for Azure RMS, og resten av key management-prosessen håndteres av Microsoft.

Du bør også full kontroll over din leier nøkkel, som omfatter oppretting av leier nøkkelen og holde kopieringsoriginal på dine lokaler. Dette scenariet blir ofte referert til som gir din egen nøkkel (BYOK). Med dette alternativet skjer følgende:

1.  Du kan generere nøkkelen leier på lokaler, på linje med IT-policyer.

2.  Du overføre sikkert nøkkelen leier fra en Hardware Security Module (HSM) i din besittelse til HSMs som eies og administreres av Microsoft. Leier nøkkelen forlater aldri maskinvare beskyttelse grensen i denne prosessen.

3.  Når du overfører leier nøkkelen til Microsoft, forblir beskyttet av Thales HSMs. Microsoft har samarbeidet med Thales å sikre at leier nøkkelen ikke kan trekkes ut fra Microsofts HSMs.

Men det er valgfritt, du også vil sannsynligvis bruke nær sanntids forbruk logger fra Azure RMS å se nøyaktig hvordan og når leier-nøkkel er i bruk.

> [!NOTE]
> Som en ekstra beskyttelse mål bruker Azure RMS verdener separat sikkerhet for sine datasentre i Nord-Amerika, EMEA (Europa, Midtøsten og Afrika) og Asia. Når du administrerer din egen leier-nøkkelen, er det knyttet til sikkerhet verden av området der RMS-leier er registrert. En leier nøkkel fra europeisk kunde kan for eksempel ikke brukes i datasentre i Nord-Amerika eller Asia.

## <a name="BKMK_OverviewLifecycle"></a>Den viktigste livssyklusen for leier
Hvis du bestemmer deg for at Microsoft skal behandle leier-nøkkelen, håndterer Microsoft mesteparten av viktige lifecycle-operasjoner. Men hvis du bestemmer deg å administrere leier-nøkkelen, er du ansvarlig for mange av operasjonene som viktige livssyklus og noen flere prosedyrer.

Følgende diagrammer viser og sammenligner disse to alternativene. Det første diagrammet viser hvor lite administrator administrasjonskostnader som det er for deg i standardkonfigurasjonen når styrer Microsoft leier nøkkelen.

![](../Image/RMS_BYOK_cloud.png)

Det andre diagrammet viser ekstra trinnene som kreves når du administrerer din egen nøkkel for leietakeradministrasjon.

![](../Image/RMS_BYOK_onprem.png)

Hvis du velger å la Microsoft administrere leier-nøkkelen, ikke ytterligere handling er nødvendig for å generere nøkkelen og du kan hoppe over de følgende delene og gå direkte til [Next steps](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_NextSteps).

Hvis du bestemmer deg for å administrere leier-nøkkelen selv, kan du lese nedenfor for mer informasjon.

### Hvis du vil ha mer informasjon om HSMs for Thales og Microsoft-tillegg
Azure RMS bruker Thales HSMs til å beskytte dine nøkler.

Thales e-sikkerhet er en ledende global leverandør på datakryptering og cyber-sikkerhetsløsninger til finanstjenester, høy teknologi, produksjon, myndigheter og teknologi sektorer. Med en 40-års banerekord for å beskytte bedriftens og offentlig informasjon, Thales løsninger brukes av fire av de fem største energi og aerospace selskaper, 22 NATO-land, og sikre mer enn 80 prosent av verden over betalingstransaksjoner.

Microsoft har samarbeidet med Thales å forbedre tilstanden til grafikk for HSMs. Disse forbedringene kan du nyte typiske fordelene vertsbaserte tjenester uten å oppgi kontroll over nøklene. Disse forbedringene kan spesielt Microsoft behandle HSMs slik at du ikke trenger. Som en skytjeneste Azure RMS, skaleres på kort varsel som dekker organisasjonens bruk topper. Samtidig beskyttes nøkkelen i Microsofts HSMs: Beholder du kontrollen over viktige lifecycle fordi du generere nøkkelen og overføre den til Microsofts HSMs.

Hvis du vil ha mer informasjon, se [HSMs Thales og Azure RMS](http://www.thales-esecurity.com/msrms/cloud) på webområdet Thales.

## <a name="BKMK_Pricing"></a>BYOK priser og begrensninger
Organisasjonen som har et IT-administrert Azure abonnement kan bruke BYOK og logge bruken uten ekstra kostnad. Organisasjoner som bruker RMS for personer kan ikke bruke BYOK og logging fordi de ikke har en Leieradministrator for å konfigurere disse funksjonene.

> [!NOTE]
> Hvis du vil ha mer informasjon om RMS for enkeltpersoner, se [RMS for enkeltpersoner og Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

![](../Image/RMS_BYOK_noExchange.png)

BYOK og logging fungerer sømløst med hvert program som integreres med Azure RMS. Dette inkluderer sky tjenester, for eksempel SharePoint Online, lokale servere som kjører Exchange og SharePoint som fungerer med Azure RMS ved hjelp av RMS-kontakt og klientprogrammer, for eksempel Office-2013. Du vil få nøkkelbruk logger uavhengig av hvilken programmet foretar forespørsler av Azure RMS.

Det finnes ett unntak: For øyeblikket **Azure RMS-BYOK er ikke kompatibel med Exchange Online**.  Hvis du vil bruke Exchange Online, anbefaler vi at du distribuerer Azure RMS i standard Nøkkelbehandling modus nå, der Microsoft genererer og behandler nøkkelen. Du har muligheten til å flytte til BYOK senere, for eksempel når Exchange Online støtter Azure RMS-BYOK. Hvis du ikke kan vente, er imidlertid et annet alternativ til å distribuere Azure RMS med BYOK nå, med redusert RMS-funksjonalitet for Exchange Online (ubeskyttet e-post og ubeskyttede vedlegg forblir funksjonell):

-   Beskyttede e-postmeldinger eller beskyttet vedlegg i Outlook Web Access kan ikke vises.

-   Beskyttede e-postmeldinger på mobile enheter som bruker Exchange ActiveSync IRM kan ikke vises.

-   Transport dekryptering (for eksempel for å søke etter skadelig programvare) og journal dekryptering er ikke mulig, derfor beskyttet e-post og beskyttet vedlegg vil bli hoppet over.

-   Transport beskyttelse regler og data tap forebygging (DLP) som fremtvinger IRM-policyer er ikke mulig, så RMS-beskyttelse ikke kan brukes ved hjelp av disse metodene.

-   Server-basert Søk etter beskyttede e-postmeldinger, slik at beskyttede e-postmeldinger vil bli hoppet over.

Når du bruker Azure RMS-BYOK med redusert RMS-funksjonalitet for Exchange Online, vil RMS arbeide med e postklienter i Outlook på Windows og Mac, og andre e-postklienter som ikke bruker Exchange ActiveSync IRM.

Hvis du overfører til Azure RMS fra AD RMS, kanskje du har importert nøkkelen som et klarert publisering domene (TPD) til Exchange Online (også kalt BYOK i Exchange-terminologi, som er atskilt fra Azure RMS-BYOK). I dette scenariet må du fjerne TPD fra Exchange Online for å unngå konflikt mellom maler og policyer. Hvis du vil ha mer informasjon, se [Fjern-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) fra Exchange Online-cmdleter biblioteket.

Noen ganger er Azure RMS-BYOK-unntak for Exchange Online ikke et problem i praksis. Organisasjoner som trenger BYOK og logging kjører for eksempel data programmer (Exchange, SharePoint, Office) lokale, og bruk Azure RMS for funksjoner som ikke er lett tilgjengelige med lokale AD RMS (for eksempel samarbeid med andre selskaper og tilgang fra mobile klienter). Både BYOK og logging arbeid Vel i dette scenariet, og føre til at selskapet har full kontroll over sine Azure RMS-abonnement.

## <a name="BKMK_ImplementBYOK"></a>Implementering av bringe din egen nøkkel (BYOK)
Bruk informasjon og prosedyrer i denne delen hvis du har valgt å generere og behandle dine leier-tasten. Plasser den situasjonen din egen nøkkel (BYOK):

-   [Prerequisites for BYOK](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Preqs)

-   [Generate and transfer your tenant key – over the Internet](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOK_Internet)

-   [Generate and transfer your tenant key – in person](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOK_InPerson)

> [!IMPORTANT]
> Hvis du allerede har begynt å bruke [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (tjenesten er aktivert), og du har brukere som kjører Office 2010, kan du kontakte Microsofts kundestøttetjeneste (CSS) før du kjører disse prosedyrene. Avhengig av situasjonen og krav, kan du fortsatt bruke BYOK, men med noen begrensninger eller flere trinn.
> 
> Også kontakte CSS Hvis organisasjonen har bestemte retningslinjer for håndtering av nøkler.

### <a name="BKMK_Preqs"></a>Forutsetninger for BYOK
Se følgende tabell for en liste over forutsetninger for å bringe din egen nøkkel (BYOK).

|Krav|Hvis du vil ha mer informasjon|
|--------|----------------------------------|
|Et abonnement som støtter Azure RMS|Hvis du vil ha mer informasjon om hvilke abonnementer som er tilgjengelige, se den [Cloud-abonnementer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet.|
|Du bruker ikke RMS for enkeltpersoner eller Exchange Online. Eller, hvis du bruker Exchange Online, du forstår og godtar begrensningene ved bruk av BYOK med denne konfigurasjonen.|Hvis du vil ha mer informasjon om begrensninger og gjeldende begrensninger for BYOK, se den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) delen i dette emnet. **Important:** BYOK er for øyeblikket ikke kompatible med Exchange Online.|
|Thales HSM, smartkort og for støtteprogramvare<br /><br />Hvis du migrerer fra AD RMS til Azure RMS ved hjelp av programvare for å maskinvarenøkkelen, må du ha en minste versjon av 11.62 for Thales-drivere.|Du må ha tilgang til en Thales Hardware sikkerhetsmodul og grunnleggende operativ kunnskap om Thales HSMs. Se [Thales Hardware sikkerhetsmodul](http://www.thales-esecurity.com/msrms/buy) for listen over kompatible modeller, eller kjøpe en HSM Hvis du ikke har en.|
|Hvis du vil overføre leier nøkkelen over Internett i stedet for å være fysisk tilstede i Redmond, USA:<br /><br />1.  En frakoblet x 64-arbeidsstasjon med en minste Windows-operativsystem Windows 7 og Thales nShield-programvare som er minst versjon 11.62.<br />    Hvis denne arbeidsstasjonen kjører Windows 7, må du [installere Microsoft for .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br />2.  En arbeidsstasjon som er koblet til Internett og har en minimum Windows-operativsystem på Windows 7.<br />3.  En USB-stasjon eller annen bærbar lagringsenhet med minst 16 MB ledig plass.|Disse forutsetningene er ikke obligatoriske Hvis du reiser til Redmond og overføre leier nøkkelen i person.<br /><br />Av sikkerhetsgrunner anbefaler vi at den første arbeidsstasjonen ikke er koblet til et nettverk. Men er dette ikke et program gjennomført. **Note:** I instruksjonene som følger, kalles denne arbeidsstasjonen frakoblet arbeidsstasjonen.<br />I tillegg hvis de leier nøkkelen for nettverk produksjon, anbefaler vi at du bruker en ekstra, separat arbeidsstasjon ned verktøysettet og laste opp nøkkelen for leietakeradministrasjon. Men du kan bruke den samme arbeidsstasjonen til testing, som den første. **Note:** I instruksjonene som følger, kalles denne andre arbeidsstasjonen Internett-tilkoblede arbeidsstasjonen.|
|Valgfritt: Azure abonnement|Hvis du vil logge på leier nøkkelbruk (og bruk av Rights Management), må du ha et abonnement på Azure og tilstrekkelig lagringsplass på Azure til å lagre loggene.|
Fremgangsmåten for å generere og bruke en egen nøkkel til leier avhenger av om du vil gjøre dette via Internett eller i personen:

-   **Over Internett:** Dette krever noen ekstra konfigurasjonstrinn, som å laste ned og bruke et verktøysett og Windows PowerShell-cmdleter. Du har imidlertid ikke være fysisk i et Microsoft-funksjonen til å overføre nøkkelen leier. Sikkerheten er ivaretatt av følgende metoder:

    -   Du kan generere nøkkelen leier fra en frakoblet arbeidsstasjon, noe som reduserer angrep overflaten.

    -   Nøkkelen for leieradministrasjon er kryptert med en Key Exchange Key (KEK), som forblir kryptert før det overføres til Azure RMS-HSMs. Bare kryptert versjon av nøkkelen leier beholder den opprinnelige arbeidsstasjonen.

    -   Et verktøy egenskapene på leier nøkkelen som binder leier nøkkelen til Azure RMS sikkerhet verden. Så når Azure RMS-HSMs motta og dekryptere leier-nøkkel, kan bare disse HSMs bruke den. Leier nøkkelen kan ikke eksporteres. Denne bindingen gjennomføres av Thales-HSMs.

    -   Den nøkkelen Exchange Key (KEK) som brukes til å kryptere leier-nøkkelen genereres i Azure RMS-HSMs og er ikke eksporterbar. HSMs gjennomføre at det kan være ingen tydelig versjon av KEK utenfor HSMs. I tillegg inneholder verktøysettet attestation fra Thales at KEK er ikke eksporteres og ble generert i en ekte HSM som ble produsert av Thales.

    -   Verktøysettet inneholder attestation fra Thales som Azure RMS sikkerhet verden også ble generert på en ekte HSM produsert av Thales. Dette viser du at Microsoft bruker ekte maskinvare.

    -   Microsoft bruker separate KEKs samt skille sikkerhet verdener i hver geografiske område, som sikrer at nøkkelen leier kan bare brukes i datasentre i området det ble kryptert. En leier nøkkel fra europeisk kunde kan for eksempel ikke brukes i datasentre i Nord-Amerika eller Asia.

    > [!NOTE]
    > Leier nøkkelen kan trygt flytte gjennom ikke-klarerte datamaskiner og nettverk fordi det er kryptert og sikret med nivå tilgangskontrolltillatelser, noe som gjør det brukes bare i din HSMs og Microsofts HSMs for Azure RMS. Du kan bruke skript som finnes i verktøysettet for å bekrefte sikkerhetsinnstillingene i bruk og lese mer informasjon om hvordan dette fungerer fra Thales: [Maskinvarenøkkelen management i RMS-Cloud](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **Personlig:** Dette krever at du kontakter Microsoft kundestøttetjeneste (CSS) for å planlegge en avtale for overføring for Azure RMS. Du må reise til et Microsoft office i Redmond, Washington, USA til å overføre leier nøkkelen til Azure RMS sikkerhet verden.

### <a name="BKMK_BYOK_Internet"></a>Generere og overføre nøkkelen leier – over Internett
Bruk fremgangsmåtene nedenfor hvis du vil overføre leier nøkkelen over Internett i stedet for å reise til et Microsoft-funksjonen til å overføre nøkkelen leier i person:

-   [Prepare your Internet-connected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareWorkstation)

-   [Prepare your disconnected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_DisconnectedPrepareWorkstation)

-   [Generate your tenant key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate)

-   [Prepare your tenant key for transfer](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer)

-   [Transfer your tenant key to Azure RMS](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer)

#### <a name="BKMK_InternetPrepareWorkstation"></a>Klargjør Internett-tilkoblede arbeidsstasjonen
Hvis du vil forberede din arbeidsstasjon som er koblet til Internett, følger du disse 3 trinnene:

-   [Step 1: Install Windows PowerShell for Azure Rights Management](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation1)

-   [Step 2: Get your Azure Active Directory tenant ID](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation2)

-   [Step 3: Download the BYOK toolset](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation3)

##### <a name="BKMK_PrepareInternetConnectedWorkstation1"></a>Trinn 1: Installere Windows PowerShell for Azure Rights Management
Fra Internett-tilkoblede-arbeidsstasjon, kan du laste ned og installere Windows PowerShell-modul for Azure Rights Management.

> [!NOTE]
> Hvis du har lastet ned denne modulen for Windows PowerShell, kan du kjøre følgende kommando for å kontrollere at versjonsnummeret for din er minst 2.1.0.0: `(Get-Module aadrm -ListAvailable).Version`

For å lese installasjonsinstrukser, kan du se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

##### <a name="BKMK_PrepareInternetConnectedWorkstation2"></a>Trinn 2: Få din leier Azure Active Directory-ID
Start Windows PowerShell med den **Kjør som administrator** alternativet, og deretter kjører du følgende kommandoer:

-   Bruk av [koble til AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) cmdlet til å koble til Azure RMS-tjenesten:

    ```
    Connect-AadrmService
    ```
    Når du blir spurt, skriver du inn din [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for klientadministrasjon administratorlegitimasjon (vanligvis bruker du en konto som er en global administrator for Azure Active Directory eller Office 365).

-   Bruk av [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet til å vise konfigurasjonen av din leier:

    ```
    Get-AadrmConfiguration
    ```
    Fra utdataene, lagre GUIDEN fra den første linjen (BPOSId). Dette er din Azure Active Directory leier-ID som du vil trenge senere når du klargjør leier nøkkelen for opplasting.

-   Bruk av [Koble fra AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet til å koble fra Azure RMS-tjenesten før du er klar til å laste opp din nøkkel:

    ```
    Disconnect-AadrmService
    ```

Ikke Lukk vinduet Windows PowerShell.

##### <a name="BKMK_PrepareInternetConnectedWorkstation3"></a>Trinn 3: Last ned BYOK-verktøysettet
Gå til Microsoft Download Center og [laste ned verktøysettet BYOK](http://go.microsoft.com/fwlink/?LinkId=335781) for din region:

|Region|Navn på installasjonspakke|
|----------|------------------------------|
|Nord-Amerika|AzureRMS-BYOK-verktøy-de forente States.zip|
|Europa|BYOK-AzureRMS-Europe.zip-verktøy|
|Asia|BYOK-AzureRMS-AsiaPacific.zip-verktøy|
Verktøysettet inneholder følgende:

-   En Key Exchange Key (KEK)-pakken som har et navn som begynner med **BYOK-KEK-pkg -**.

-   En sikkerhet verden-pakken som har et navn som begynner med **BYOK-SecurityWorld-pkg -**.

-   Et python-skript som heter **verifykeypackage.py**.

-   En kommandolinje kjørbar fil som heter **KeyTransferRemote.exe**, en metadatafil som heter **KeyTransferRemote.exe.config**, og tilhørende DLL-filer.

-   En Visual C++-pakken, kalt **vcredist_x64.exe**.

Kopier pakken til en USB-enhet eller andre bærbare lagringsenheter.

#### <a name="BKMK_DisconnectedPrepareWorkstation"></a>Forberede pulten frakoblet
Hvis du vil forberede din arbeidsstasjon som ikke er koblet til et nettverk (Internett eller det lokale nettverket), fremgangsmåte 2:

-   [Step 1: Prepare the disconnected workstation with Thales HSM](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareDisconnectedWorkstation1)

-   [Step 2: Install the BYOK toolset on the disconnected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareDisconnectedWorkstation2)

##### <a name="BKMK_PrepareDisconnectedWorkstation1"></a>Trinn 1: Forberede frakoblet arbeidsstasjon med Thales HSM
Installere programvaren nCipher (Thales) støtte på en Windows-datamaskin på frakoblet-arbeidsstasjon, og fest deretter en Thales HSM til denne datamaskinen.

Kontroller at verktøyene for Thales er i banen til **(%nfast_home%\bin** og **%nfast_home%\python\bin**). Skriv for eksempel følgende:

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Hvis du vil ha mer informasjon, se brukerhåndboken som følger med Thales-HSM, eller gå til webområdet for Thales for Azure RMS på [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

##### <a name="BKMK_PrepareDisconnectedWorkstation2"></a>Trinn 2: Installere verktøysettet BYOK på arbeidsstasjonen frakoblet
Kopier BYOK toolset pakken fra USB-stasjon eller andre bærbare lagringsenheter, og gjør deretter følgende:

1.  Pakk ut filene fra den nedlastede pakken til en mappe.

2.  Kjør vcredist_x64.exe fra denne mappen.

3.  Følg instruksjonene for installasjon av Visual C++ runtime-komponenter for Visual Studio 2012.

#### <a name="BKMK_InternetGenerate"></a>Generer leier-nøkkel
På frakoblet arbeidsstasjonen, følge disse 3 trinnene til å generere leier nøkkelen:

-   [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1)

-   [Step 2: Validate the downloaded package](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate2)

-   [Step 3: Create a new key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate3)

##### <a name="BKMK_InternetGenerate1"></a>Trinn 1: Opprette en verden for sikkerhet
Start en ledetekst, og Kjør programmet Thales ny verden.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Dette programmet oppretter et **Sikkerhet verden** -filen i % NFAST_KMDATA%\local\world, som tilsvarer C:\ProgramData\nCipher\Key Management Settings\User-mappen. Du kan bruke forskjellige verdier for quorum, men i vårt eksempel blir du bedt om å angi tre tomme kort og PIN-koder for hver enkelt. Deretter må en hvilken som helst to kort ha administrativ tilgang til sikkerhet verden (den angitte kvorum).  Disse kortene blir den **satt av Administrator-kort** for den nye verden for sikkerhet. På dette stadiet, kan du angi passord eller PIN-kode for hvert kort som ACS, eller legge den til senere med en kommando.

> [!TIP]
> Du kan kontrollere gjeldende Konfigurasjonsstatus for din HSM ved hjelp av den `nkminfo` kommandoen.

Deretter gjør du følgende:

1.  Installer Thales CNG-leverandøren som beskrevet i dokumentasjonen for Thales, og konfigurere den til å bruke den nye verden for sikkerhet.

2.  Ta sikkerhetskopi av filen verden i **%nfast_kmdata%\local**. Sikre og beskytte filen verden, Administrator-kort og deres pinner, og kontroller at ingen enkelt person har tilgang til mer enn ett kort.

##### <a name="BKMK_InternetGenerate2"></a>Trinn 2: Validere den nedlastede pakken
Dette trinnet er valgfritt, men anbefales slik at du kan bekrefte følgende:

-   Key Exchange nøkkelen som er inkludert i verktøysettet som er generert fra en ekte Thales HSM.

-   Hash-koden for Azure RMS sikkerhet verden som er inkludert i verktøysettet som er generert i en ekte Thales HSM.

-   Key er Exchange ikke kan eksporteres.

> [!NOTE]
> Hvis du vil validere den nedlastede pakken, HSM må være tilkoblet, slått på, og må ha en sikkerhet verden på den (for eksempel det du nettopp har opprettet).

###### Validere den nedlastede pakken

1.  Kjøre skriptet verifykeypackage.py ved å binde en av følgende, avhengig av din region:

    -   For Nord-Amerika:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   For Europa:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   For Asia:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > Thales-programvaren har en Python tolk ved %NFAST_HOME%\python\bin

2.  Bekreft at du ser følgende, som indikerer vellykket validering: **Resultat:  SUKSESS**

Dette skriptet validerer signataren kjeden opptil rotnøkkelen for Thales. Hash-koden for denne rotnøkkel er innebygd i skriptet, og verdien bør være **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Du kan også bekrefte denne verdien separat ved å gå til [Thales webområde](http://www.thalesesec.com/).

Du er nå klar til å opprette en ny nøkkel, blir nøkkelen RMS leier.

##### <a name="BKMK_InternetGenerate3"></a>Trinn 3: Opprette en ny nøkkel
Generere en CNG nøkkel ved hjelp av Thales **generatekey** og **cngimport** programmer.

Kjør følgende kommando for å generere nøkkelen:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Når du kjører denne kommandoen, bruker du disse instruksjonene:

-   For nøkkelstørrelse, vi anbefaler 2048, men også støtte 1024-biters RSA-nøkler for eksisterende AD RMS-kunder som har slike nøkler og overfører til Azure RMS.

-   Erstatt verdien for *contosokey* for den **fra styreenhet ble** og **plainname** med en strengverdi. Hvis du vil minimere administrative administrasjonskostnader og redusere risikoen for feil, anbefaler vi at du bruker samme verdi for begge, og bruke alle små bokstaver.

-   Pubexp blir stående tomt felt (standard) i dette eksemplet, men du kan angi bestemte verdier. Hvis du vil ha mer informasjon, se dokumentasjonen for Thales.

Kjør følgende kommando for å importere nøkkelen til CNG:

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
Når du kjører denne kommandoen, bruker du disse instruksjonene:

-   Erstatte *contosokey* med den samme verdien som er angitt i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) fra den *generere leier-nøkkel* delen.

-   Bruk av **- M** alternativet slik at nøkkelen er egnet for dette scenariet. Uten dette blir den resulterende nøkkelen en brukerspesifikk nøkkel for gjeldende bruker.

Denne kommandoen oppretter en Tokenized nøkkel-fil i mappen %NFAST_KMDATA%\local med en navnet starter med **key_caping_** etterfulgt av en SID. For eksempel: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Denne filen inneholder en kryptert nøkkel.

> [!TIP]
> Du kan vise gjeldende Konfigurasjonsstatus av nøklene ved hjelp av `nkminfo –k` kommandoen.

Sikkerhetskopiere denne filen med Tokenized nøkkelen på et trygt sted.

> [!IMPORTANT]
> Når du overfører senere nøkkelen til Azure RMS, kan ikke Microsoft eksportere denne nøkkelen tilbake til deg slik at det blir svært viktig at du sikkerhetskopierer hverdagen nøkkel og sikkerhet trygg. Kontakt Thales for veiledning og beste praksis for sikkerhetskopiering av nøkkelen.

Nå er du klar til å overføre leier nøkkelen til Azure RMS.

#### <a name="BKMK_InternetPrepareTransfer"></a>Forberede leier nøkkelen for overføring
På den frakoblede arbeidsstasjonen følger disse 4 trinn for å klargjøre leier nøkkelen:

-   [Step 1: Create a copy of your key with reduced permissions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer1)

-   [Step 2: Inspect the new copy of the key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer2)

-   [Step 3: Encrypt your key by using Microsoft’s Key Exchange Key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer3)

-   [Step 4: Copy your key transfer package to the Internet-connected workstation](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetPrepareTransfer4)

##### <a name="BKMK_InternetPrepareTransfer1"></a>Trinn 1: Opprett en kopi av nøkkelen med redusert tillatelser
Hvis du vil redusere tillatelsene for leieradministrasjon-nøkkelen, gjør du følgende:

-   Fra en ledetekst kjører du en av følgende, avhengig av din region:

    -   For Nord-Amerika:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   For Europa:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   For Asia:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

Når du kjører denne kommandoen, erstatter *contosokey* med den samme verdien du anga i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) fra den *generere leier-nøkkel* delen.

Du blir bedt om å plugge sikkerhet verden ACS kortene, og hvis angitt passord eller PIN-koden...

Når kommandoen er fullført, vil du se **resultat: Vellykket** og kopien av leier nøkkelen med redusert tillatelsene blir i filen som heter key_xferacId_*&lt; contosokey &gt;*.

##### <a name="BKMK_InternetPrepareTransfer2"></a>Trinn 2: Undersøke den nye kopien av nøkkelen
Du kan også kjøre for Thales verktøy for å bekrefte minimal tillatelsene på den nye nøkkelen for leieradministrasjon:

-   aclprint.PY:

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe:

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

Når du kjører denne kommandoen, erstatter *contosokey* med den samme verdien du anga i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) fra den *generere leier-nøkkel* delen.

##### <a name="BKMK_InternetPrepareTransfer3"></a>Trinn 3: Kryptere nøkkelen ved hjelp av Microsofts nøkkel utvekslingsnøkkel
Kjør en av følgende kommandoer, avhengig av din region:

-   For Nord-Amerika:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   For Europa:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   For Asia:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

Når du kjører denne kommandoen, bruker du disse instruksjonene:

-   Erstatte *contosokey* med IDen som du brukte til å generere nøkkelen i [Step 1: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetGenerate1) fra den *generere leier-nøkkel* delen.

-   Erstatte *GUID* med Azure Active Directory for klientadministrasjon ID du hentet i [Step 2: Get your Azure Active Directory tenant ID](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_PrepareInternetConnectedWorkstation2) fra den *forberede arbeidsstasjonen din Internett-tilkoblet* delen.

-   Erstatte *ContosoFirstKey* med en etikett som skal brukes for din utdatafil.

Når dette er fullført den viser **resultat: Vellykket** og det vil være en ny fil i gjeldende mappe med følgende navn: TransferPackage -*ContosoFirstkey*.byok

##### <a name="BKMK_InternetPrepareTransfer4"></a>Trinn 4: Kopier pakken for overføring til Internett-tilkoblede arbeidsstasjonen
Bruk en USB-enhet eller andre bærbare lagringsenheter for å kopiere utdatafilen fra det forrige trinnet (KeyTransferPackage -*ContosoFirstkey*.byok) på Internett-tilkoblede arbeidsstasjonen.

> [!NOTE]
> Bruke fremgangsmåter for sikkerhet for å beskytte filen fordi den inneholder den private nøkkelen.

#### <a name="BKMK_InternetTransfer"></a>Overføre leier nøkkelen til Azure RMS
Følg disse 3 trinnene for å overføre nye leier nøkkelen til Azure RMS på Internett-tilkoblede-arbeidsstasjon:

-   [Step 1: Connect to Azure RMS](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer1)

-   [Step 2: Upload the key package](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer2)

-   [Step 3: Enumerate your tenant keys – as needed](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_InternetTransfer3)

##### <a name="BKMK_InternetTransfer1"></a>Trinn 1: Koble til Azure RMS
Gå tilbake til vinduet Windows PowerShell, og Skriv inn følgende:

1.  Koble til den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] tjenesten:

    ```
    Connect-AadrmService
    ```

2.  Bruk av [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) cmdleten for å se den gjeldende konfigurasjonen for leieradministrasjon nøkkel:

    ```
    Get-AadrmKeys
    ```

##### <a name="BKMK_InternetTransfer2"></a>Trinn 2: Last opp viktige pakken
Bruk av [Legg til AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) cmdlet til å laste opp viktige overføring-pakken som du kopierte fra den frakoblede arbeidsstasjonen:

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> Du blir bedt om å bekrefte handlingen. Det er viktig å forstå at denne handlingen kan ikke angres. Når du laster opp en leier nøkkel, blir den automatisk i organisasjonen din primære leier nøkkel, og brukere vil begynne å bruke denne nøkkelen for leieradministrasjon når de beskytter dokumenter og filer.

Hvis opplastingen er fullført, vises følgende melding: **Rights management-tjenesten ble lagt til nøkkelen.**

Forventer en replikeringsforsinkelse for at endringen skal videreføres til alle [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] datasentre.

##### <a name="BKMK_InternetTransfer3"></a>Trinn 3: Nummerere leier nøklene – etter behov
Bruk cmdleten Get-AadrmKeys på nytt for å se endringen i leier-nøkkel, og når du vil se en liste over leier nøklene. Leier tastene vises er nøkkelen første leier Microsoft generert for deg og alle nøkler som leier du har lagt til:

```
Get-AadrmKeys
```
Nøkkelen for klientadministrasjon som er merket som **aktive** er den som organisasjonen bruker til å beskytte dokumenter og filer.

Du har nå fullført alle trinnene som kreves for ta med din egen nøkkel via Internett og kan gå til [Next steps](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_NextSteps).

### <a name="BKMK_BYOK_InPerson"></a>Generere og overføre leier nøkkelen – personlig
Bruk følgende fremgangsmåte hvis du ikke ønsker å overføre nøkkelen leier over Internett, men overføre leier nøkkelen i person i stedet.

-   [Generate your tenant key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateKey)

-   [Transfer your tenant key to Azure RMS](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Transfer)

#### <a name="BKMK_GenerateKey"></a>Generer leier-nøkkel
For å generere leier nøkkelen, følger du disse 3 trinnene:

-   [Step 1: Prepare a workstation with Thales HSM](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey1)

-   [Step 2: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey2)

-   [Step 3: Create a new key](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey3)

##### <a name="BKMK_GenerateYourKey1"></a>Trinn 1: Forberede en arbeidsstasjon med Thales HSM
Installere programvaren for nCipher (Thales)-støtte på en Windows-datamaskin. Knytte en Thales HSM til datamaskinen. Kontroller at verktøyene for Thales er i banen. Hvis du vil ha mer informasjon, se brukerhåndboken som følger med Thales-HSM, eller gå til webområdet for Thales for Azure RMS på [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

##### <a name="BKMK_GenerateYourKey2"></a>Trinn 2: Opprette en verden for sikkerhet
Start en ledetekst, og Kjør programmet Thales ny verden.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Dette programmet oppretter et **Sikkerhet verden** -filen i % NFAST_KMDATA%\local\world, som tilsvarer C:\ProgramData\nCipher\Key Management Settings\User-mappen. Du kan bruke forskjellige verdier for quorum, men i vårt eksempel blir du bedt om å angi tre tomme kort og PIN-koder for hver enkelt. Deretter vil en hvilken som helst to kort gi full tilgang til verdens sikkerhet.  Disse kortene blir den **satt av Administrator-kort** for den nye verden for sikkerhet.

Deretter gjør du følgende:

1.  Installer Thales CNG-leverandøren som beskrevet i dokumentasjonen for Thales, og konfigurere den til å bruke den nye verden for sikkerhet.

2.  Sikkerhetskopiere filen verden. Sikre og beskytte filen verden, Administrator-kort og deres pinner, og kontroller at ingen enkelt person har tilgang til mer enn ett kort.

Du er nå klar til å opprette en ny nøkkel, blir nøkkelen RMS leier.

##### <a name="BKMK_GenerateYourKey3"></a>Trinn 3: Opprette en ny nøkkel
Generere en CNG nøkkel ved hjelp av Thales **generatekey** og **cngimport** programmer.

Kjør følgende kommando for å generere nøkkelen:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Når du kjører denne kommandoen, bruker du disse instruksjonene:

-   For nøkkelstørrelse, vi anbefaler 2048, men også støtte 1024-biters RSA-nøkler for eksisterende AD RMS-kunder som har slike nøkler og overfører til Azure RMS.

-   Erstatt verdien for *contosokey* for den **fra styreenhet ble** og **plainname** med en strengverdi. Hvis du vil minimere administrative administrasjonskostnader og redusere risikoen for feil, anbefaler vi at du bruker samme verdi for begge, og bruke alle små bokstaver.

-   Pubexp blir stående tomt felt (standard) i dette eksemplet, men du kan angi bestemte verdier. Hvis du vil ha mer informasjon, se dokumentasjonen for Thales.

Kjør følgende kommando for å importere nøkkelen til CNG:

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
Når du kjører denne kommandoen, bruker du disse instruksjonene:

-   Erstatte *contosokey* med samme verdi som du angav i trinn 1.

-   Bruk av **- M** alternativet slik at nøkkelen er egnet for dette scenariet. Uten dette blir den resulterende nøkkelen en brukerspesifikk nøkkel for gjeldende bruker.

Denne kommandoen oppretter en Tokenized nøkkel-fil i mappen %NFAST_KMDATA%\local med en navnet starter med **key_caping_** etterfulgt av en SID. For eksempel: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Denne filen inneholder en kryptert nøkkel.

Sikkerhetskopiere denne filen med Tokenized nøkkelen på et trygt sted.

> [!IMPORTANT]
> Når du senere overføre nøkkelen til Azure RMS, har Microsoft en ikke-reverserbar kopi av nøkkelen. Dette betyr at ingen kan hente nøkkelen fra HSMs hos Microsoft. Dette lar deg beholde full kontroll over leier-tasten. Derfor blir det svært viktig at du sikkerhetskopierer hverdagen nøkkel og sikkerhet trygg. Kontakt Thales for veiledning og beste praksis for sikkerhetskopiering av nøkkelen.

Nå er du klar til å overføre leier nøkkelen til Azure RMS.

#### <a name="BKMK_Transfer"></a>Overføre leier nøkkelen til Azure RMS
Når du har generert en egen nøkkel, må du overføre det til Azure RMS før du bruker den. Denne overføringen er en manuell prosess som krever at du flyr til Microsoft-kontoret i Redmond, Washington, USA for det høyeste nivået av sikkerhet. For å fullføre denne prosessen, følger du disse 3 trinnene:

-   [Step 1: Bring your key to Microsoft](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_TransferYourKey1)

-   [Step 2: Transfer your key to the Window Azure RMS security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_TransferYourKey2)

-   [Step 3: Closing procedures](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_TransferYourKey3)

###### Trinn 1: Plasser nøkkelen til Microsoft

-   Kontakt Microsoft kundestøttetjeneste (CSS) til å planlegge en avtale for overføring for Azure RMS. Ta følgende til Microsoft i Redmond:

    -   Et kvorum med Administrative kortene. Hvis du har fulgt instruksjonene tidligere i [Step 2: Create a security world](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_GenerateYourKey2), disse er to av de tre kortene.

    -   Personell som er autorisert til å utføre Administrative kortene og pinner, vanligvis to (en for hvert kort).

    -   Sikkerhet verden filen (% NFAST_KMDATA%\local\world) på en USB-stasjon.

    -   Tokenized nøkkel filen på en USB-stasjon.

###### Trinn 2: Overføre nøkkelen til vinduet Azure RMS sikkerhet verden

1.  Når du kommer til Microsoft for å overføre nøkkelen, skjer følgende:

    -   Microsoft gir deg en frakoblet arbeidsstasjon som har en Thales HSM knyttet, Thales programvare installert og en Forhåndslastede Azure RMS sikkerhet verden-fil i mappen C:\Temp\Destination.

    -   På denne arbeidsstasjonen laste du din sikkerhet verden og Tokenized nøkkel-fil fra USB-stasjonen til mappen C:\Temp\Source.

    -   Azure RMS-operatorer overføre sikkert nøkkelen til Azure RMS sikkerhet verden ved hjelp av verktøy for Thales.

    Denne prosessen vil se omtrent slik ut, der den siste parameteren med nøkkel-xfer-im i dette eksemplet er erstattet med Tokenized nøkkel filnavnet:

    **C:\ &gt; mk-reprogram.exe--eieren c:\Temp\Destination legge til c:\Temp\Source**

    **C:\ &gt; nøkkel-xfer-im.exe c:\Temp\Source c:\Temp\Destination - modulen c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  MK-omprogrammere spør du og Azure RMS-operatorer kobler til sine respektive Administrator-kort og pinner. Disse kommandoene utdatafil en Tokenized nøkkelen i C:\Temp\Destination som inneholder nøkkelen beskyttet av Azure RMS sikkerhet verden.

###### Trinn 3: Lukke prosedyrer

-   I ditt nærvær gjør Azure RMS-operatorer du følgende:

    -   Kjøre et verktøy som Microsoft utviklet i samarbeid med Thales som fjerner to tillatelsene: Tillatelse til å gjenopprette nøkkelen, og tillatelse til å endre tillatelser. Når dette er gjort, låses denne kopien av nøkkelen til Azure RMS sikkerhet verden. Thales HSMs tillater ikke Azure RMs-operatorer med kortene sine Administrator gjenopprette ren tekst-kopi av nøkkelen.

    -   Kopier den resulterende nøkkelfilen til en USB-enhet senere laste opp til Azure RMS-tjenesten.

    -   Fabrikkinnstillingene for HSM, og Tørk arbeidsstasjonen ren.

Du har nå fullført alle trinnene som kreves for ta med din egen nøkkel i person, og kan gå tilbake til organisasjonen for de neste trinnene.

## <a name="BKMK_NextSteps"></a>Neste trinn

1.  Begynne å bruke leier-nøkkelen:

    -   Hvis du ikke allerede har gjort det, må du aktivere Rights Management nå, slik at organisasjonen kan begynne å bruke RMS. Brukere begynne umiddelbart å bruke leier-tasten (administreres av Microsoft eller administrert av deg).

        Hvis du vil ha mer informasjon om produktaktivering, kan du se [Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

    -   Hvis du hadde allerede aktivert Rights Management og deretter besluttet å behandle leier nøkkelen, brukere gradvis overgang fra den gamle leier nøkkelen til den nye nøkkelen leier, og denne forskjøvet overgang kan ta et par uker å fullføre. Dokumenter og filer som er beskyttet med nøkkelen gamle leier forblir tilgjengelig for autoriserte brukere.

2.  Vurder å aktivere av brukslogging, som logger hver transaksjon som utfører RMS.

    Hvis du har valgt å behandle leier nøkkelen, inkluderer logging informasjon om hvordan du bruker nøkkelen leier. Se følgende eksempel på en loggfil som vises i Microsoft Excel der de **dekryptere** og **SignDigest** forespørselstyper viser at nøkkelen for klientadministrasjon som brukes.

    ![](../Image/RMS_Logging.gif)

    Hvis du vil ha mer informasjon om av brukslogging, se [Logging og analysere Azure Rights Management-forbruk](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

3.  Oppretthold leier-tasten.

    Hvis du vil ha mer informasjon, se [Operasjoner leietakeradministrasjon nøkkelen Azure Rights Management](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md).

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

