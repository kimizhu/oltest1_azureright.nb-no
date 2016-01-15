---
description: na
keywords: na
title: Configuring Super Users for Azure Rights Management and Discovery Services or Data Recovery
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
---
# Konfigurere Superbrukere for Azure Rights Management og tjenester for oppdagelse eller gjenoppretting av Data
Superbruker-funksjon i Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) sikrer at autoriserte personer og tjenester kan alltid lese og kontrollere data som beskytter Azure RMS for organisasjonen. Og eventuelt fjerne beskyttelsen, eller endre beskyttelsen som tidligere ble brukt. En super bruker har alltid full eierrettigheter for alle lisenser for bruk som ble gitt av organisasjonens RMS leier. Denne funksjonen blir noen ganger referert til som "logikk over data", og er et viktig element i å beholde kontrollen over organisasjonens data. Du vil for eksempel bruke denne funksjonen for en hvilken som helst av følgende scenarier:

-   En ansatt forlater organisasjonen, og du trenger å lese de beskyttede filene.

-   En IT-administrator må fjerne den gjeldende policyen for beskyttelse som ble konfigurert for filer og bruke en ny policy for beskyttelse.

-   Exchange Server må indeks-postbokser i søk.

-   Du har eksisterende IT-tjenester for forebygging (DLP) dataløsninger for tap, innhold kryptering gatewayer (CEG) og beskyttelse mot skadelig programvare-produkter som trenger å kontrollere filene som allerede er beskyttet.

-   Trenger du å masseredigere dekryptere filer for overvåking, juridiske eller andre kompatibilitetsårsaker.

Superbruker-funksjonen er ikke aktivert som standard, og ingen brukere er tilordnet denne rollen. Det er aktivert for deg automatisk hvis du konfigurerer Rights Management-koblingen for Exchange, og det er ikke nødvendig for standardtjenester som kjører Exchange Online, SharePoint Online, eller SharePoint Server.

Hvis du må manuelt aktivere funksjonen superbruker, kan du bruke Windows PowerShell-cmdlet [Aktiver AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx), og deretter tilordne brukere (eller tjenestekontoer) etter behov ved hjelp av den [Legg til AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) cmdleten. Du kan ha én eller flere Superbrukere for organisasjonen din, men du må legge til individuelle brukere. grupper støttes ikke.

> [!NOTE]
> Hvis du ennå ikke har installert Windows PowerShell-modul for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Gode fremgangsmåter for sikkerhet for funksjonen superbruker:

-   Begrense og overvåke administratorer som er tilordnet en global administrator for din Office 365 eller Azure RMS leier, eller som er tildelt rollen som GlobalAdministrator ved hjelp av den [Legg til AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) cmdleten. Disse brukerne kan aktivere funksjonen super bruker tilordne brukere (og seg selv) som Superbrukere og potensielt dekryptere alle filer som beskytter din organisasjon.

-   Hvis du vil se hvilke brukere og tjenestekontoer som er tilordnet som super-brukere, kan du bruke den [cmdleten Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx).  Som alle administrative handlinger, kan du aktivere deaktivere funksjonen super, og legger til eller fjerner Superbrukere logges, og kan overvåkes ved hjelp av den [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) kommandoen. Når Superbrukere dekryptere filer, denne handlingen er logget og kan overvåkes med [Trafikklogging](https://technet.microsoft.com/library/dn529121.aspx).

-   Hvis du ikke trenger super bruker funksjonen for daglige tjenester, aktiverer du funksjonen bare når du trenger det, og deaktivere den på nytt ved hjelp av den [Deaktiver AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) cmdleten.

Følgende loggen henting viser enkelte eksempel fra å bruke cmdleten Get-AadrmAdminLog. I dette eksemplet bekrefter administratoren for Contoso Ltd. at superbruker-funksjonen er deaktivert, legger til Richard Simone som en superbruker, kontrollerer at Richard er bare super brukeren konfigurert for Azure RMS, og deretter aktiverer super bruker funksjonen slik at Richard nå kan dekryptere noen filer som er beskyttet av en ansatt som har nå forlatt selskapet.

`2015-08-01T18:58:20	admin@contoso.com	GetSuperUserFeatureState	Passed	Disabled`
`2015-08-01T18:59:44	admin@contoso.com	AddSuperUser -id rsimone@contoso.com	Passed	True`
`2015-08-01T19:00:51	admin@contoso.com	GetSuperUser	Passed	rsimone@contoso.com`
`2015-08-01T19:01:45	admin@contoso.com	SetSuperUserFeatureState -state Enabled	Passed	True`

## <a name="BKMK_RMSProtectionModule"></a>Skriptalternativer for Superbrukere
Ofte, noen som er tilordnet en super bruker for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] må du fjerne beskyttelsen fra flere filer på flere steder. Det er mulig å gjøre dette manuelt, men det er mer effektiv (og ofte mer pålitelig) til skript på dette. Du gjør dette, [laste ned verktøyet RMS beskyttelse](http://www.microsoft.com/en-us/download/details.aspx?id=47256). Deretter bruker du  [Opphev RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) cmdlet, og [Beskytt RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx)   cmdleten etter behov.

> [!IMPORTANT]
> Selv om beskyttelse av RMS-verktøyet er utviklet for Superbrukere til bulk Opphev filer for gjenopprettingsformål, den gjeldende versjonen av verktøyet støtter ikke brukergodkjenning for Azure RMS. Til denne begrensningen er løst, må du bruke en service principal-konto til å godkjenne med Azure RMS før du kan fjerne beskyttelsen fra filer.  For mer informasjon og instruksjoner, kan du se [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/azure/mt433202.aspx).

Hvis du vil ha mer informasjon om disse cmdlets, se [RMS beskyttelse Cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> RMSProtection Windows PowerShell-modulen som leveres med verktøyet RMS-beskyttelse er forskjellig fra, og supplerer hovedvinduet [Windows PowerShell-modul for Azure Rights Management](https://technet.microsoft.com/library/jj585027.aspx). Den støtter både Azure RMS og AD RMS.

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

