---
description: na
keywords: na
title: Decommissioning and Deactivating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
---
# Dekommisjonering og deaktivere Azure Rights Management
Du har alltid kontroll av om organisasjonen beskytter innholdet ved hjelp av [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS), og hvis du ikke lenger ønsker å bruke denne løsningen for beskyttelse av informasjon, du har forsikring om at du ikke vil bli låst ute fra innhold som tidligere var beskyttet. Hvis du ikke trenger fortsatt tilgang til tidligere beskyttet innhold, kan du ganske enkelt deaktivere tjenesten, men du kan la abonnementet på Azure Rights Management utløper. Hvis du for eksempel vil dette være avhengig av når du har fullført testingen [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] før du distribuerer det i et produksjonsmiljø.

Men hvis du har distribuert [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] i produksjon, må du kontrollere at du har en kopi av Azure Rights Management leier nøkkelen før du deaktiverer tjenesten og gjøre dette før abonnementet utløper, fordi dette vil sikre at du kan beholde tilgang til innhold som er beskyttet av Azure Rights Management etter at tjenesten er deaktivert. Hvis du brukte kommandoen Flytt din egen nøkkel-løsning (BYOK) der du genererer og administrere din egen nøkkel i en HSM, har du allerede Azure Rights Management leier-tasten. Men hvis den ble styrt av Microsoft (standard), kan du se instruksjonene for å eksportere nøkkelen leier i [Operasjoner leietakeradministrasjon nøkkelen Azure Rights Management](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md) emnet.

> [!TIP]
> Selv etter at abonnementet utløper, forblir Azure Rights Management-leier tilgjengelig for bruker innholdstyper for en lengre periode. Imidlertid vil du ikke lenger kunne eksportere nøkkelen leier.

Når du har Azure Rights Management leier nøkkelen, kan du distribuere Rights Management på lokaler (AD RMS) og importere leier nøkkelen som et klarert publisering domene (TPD). Du har følgende alternativer for dekommisjonering Azure Rights Management-distribusjon:

|Hvis dette gjelder for deg...|… Dette gjør du:|
|---------------------------------|--------------------|
|Du vil at alle brukere å fortsette å bruke Rights Management, men bruker en lokale løsning i stedet for å bruke RMS Azure →|Bruk av [Sett AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) cmdlet til å styre distribusjonen av lokale eksisterende brukere når de forbruker innhold som er beskyttet etter denne endringen. Brukere vil automatisk bruke AD RMS-installasjonen til å bruke det beskyttede innholdet.<br /><br />For brukere til å bruke innhold som ble beskyttet før denne endringen omdirigerer klientene til lokale distribusjonen ved hjelp av den **LicensingRedirection** registernøkkelen for 2016 for Office eller Office-2013, som beskrevet i den [service discovery-delen](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) i RMS-klient distribusjon notater og **LicenseServerRedirection** registernøkkelen for Office 2010, som beskrevet i [registerinnstillingene for Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Du vil stoppe ved hjelp av Rights Management-teknologier helt →|Gi administrator for en dedikert [super brukerrettigheter](https://technet.microsoft.com/library/mt147272.aspx) og gi denne personen i [RMS-beskyttelse verktøyet](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Denne administratoren kan deretter bruke verktøyet til bulk-dekryptere filene i mappene som ble beskyttet av Azure Rights Management, slik at filene tilbake til at beskyttelsen oppheves, og derfor kan leses uten en Rights Management-teknologi som Azure RMS- eller AD RMS. Dette verktøyet kan brukes med både Azure RMS og AD RMS, slik at du har valget mellom å dekryptere filer før eller etter at du deaktiverer Azure RMS, eller en kombinasjon.|
|Du kan ikke identifisere alle filer som er beskyttet av Azure RMS, eller du vil at alle brukere skal kunne lese automatisk alle beskyttede filer ble hoppet over →|Distribuere en registerinnstilling på alle klientdatamaskiner ved å bruke den **LicensingRedirection** registernøkkelen for 2016 for Office og Office-2013, som beskrevet i den [service discovery-delen](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) i RMS-klient distribusjon notater, og **LicenseServerRedirection** registernøkkelen for Office 2010, som beskrevet i [registerinnstillingene for Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Også distribuere en annen registerinnstilling til å hindre brukere i å beskytte nye filer ved å angi **DisableCreation** til **1**, som beskrevet i [Office-registerinnstillingene](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Du vil ha en kontrollert, manuell gjenopprettingstjenesten for alle filer som ble tapt →|Gi angitte brukere i en gruppe for data recovery [super brukerrettigheter](https://technet.microsoft.com/library/mt147272.aspx) og gi dem den [RMS-beskyttelse verktøyet](http://www.microsoft.com/en-us/download/details.aspx?id=47256) slik at de kan oppheve filer når du ber om standardbrukere.<br /><br />På alle datamaskiner, kan du distribuere registerinnstilling til å hindre brukere i å beskytte nye filer ved å angi **DisableCreation** til **1**, som beskrevet i [Office-registerinnstillingene](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Hvis du vil ha mer informasjon om prosedyrer i denne tabellen, kan du se følgende ressurser:

-   For informasjon om AD RMS og referanser for distribusjon, kan du se [Active Directory Rights Management Services oversikt](https://technet.microsoft.com/library/hh831364.aspx).

-   For instruksjoner for å importere Azure RMS leier nøkkelen som en TPD-fil, kan du se [legge til en klarert publisering domene](https://technet.microsoft.com/library/cc771460.aspx).

-   Hvis du vil installere Windows PowerShell-modul for Azure RMS, til å angi URL-adressen for overføring, kan du se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Når du er klar til å deaktivere tjenesten Azure RMS for organisasjonen, kan du bruke fremgangsmåten nedenfor.

## Deaktivere rettighetsadministrasjon
Bruk en av fremgangsmåtene nedenfor til å deaktivere [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Du kan også bruke Windows PowerShell-cmdlet [Deaktiver Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx), for å deaktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### For å deaktivere rettighetsadministrasjon fra Office 365 administrasjonssenteret

1.  [Logge på Office 365 med arbeid eller et skoleprosjekt kontoen](https://portal.office.com/) som er administrator for Office 365-distribusjon.

2.  Hvis Office 365 administrasjonssenteret ikke vises automatisk på nytt, velger ikonet app Oppgavevelger i øverst til venstre og velger **Admin**. Den **Admin** side ved side vises bare for Office 365-administratorer.

    > [!TIP]
    > Admin center, se [om Office 365 administrasjonssenteret - Admin hjelp](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  I den venstre ruten utvider du **Innstillinger for**.

4.  Klikk **Rights Management**.

5.  På den **RIGHTS MANAGEMENT** klikker du **Behandle**.

6.  På den **rights management** klikker du **deaktivere**.

7.  Når du blir spurt **vil du deaktivere rettighetsadministrasjon?**, klikker du **deaktivere**.

Nå bør du se **Rights Management er ikke aktivert** og alternativet for å aktivere.

#### For å deaktivere rettighetsadministrasjon fra Azure-Portal

1.  Logg deg på den [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  I den venstre ruten klikker du **ACTIVE DIRECTORY**.

3.  Fra den **active directory** klikker du **RIGHTS MANAGEMENT**.

4.  Velg mappen som skal behandle for [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], klikker du **DEACTIVATE**, og Bekreft handlingen.

Den **RIGHTS MANAGEMENT STATUS** skal nå vise **inaktiv** og **DEACTIVATE** alternativet er erstattet med **Aktiver**.

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

