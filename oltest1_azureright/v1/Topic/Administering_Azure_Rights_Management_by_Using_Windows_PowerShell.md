---
description: na
keywords: na
title: Administering Azure Rights Management by Using Windows PowerShell
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
---
# Administrasjon av Azure Rights Management ved hjelp av Windows PowerShell
Selv om du kan aktivere Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) ved hjelp av den [!INCLUDE[o365_2](../Token/o365_2_md.md)] administrasjonssenteret eller Azure portal, kan du også bruke Windows PowerShell-modul for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (AADRM) for å gjøre dette.

Etter at du har aktivert [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], ytterligere administrasjon for tjenesten er kanskje ikke nødvendig. Imidlertid noen scenarier for avansert konfigurasjon krever at du bruker Windows PowerShell-modul for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Tabellen nedenfor viser noen av scenariene for avansert konfigurasjon som bruker Windows PowerShell. For en fullstendig liste over tilgjengelige cmdlets med mer informasjon om hver enkelt, kan du se [Azure Rights Management Cmdlets](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Hvis du må installere Windows PowerShell-modul for [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Det finnes også en ekstra modul for Windows PowerShell, **RMSProtection**, som støtter både Azure RMS og AD RMS. Denne modulen støtter beskytte og fjerne beskyttelsen fra flere filer, slik at for eksempel kan du bulk-beskytte alle filene i en mappe. Hvis du vil ha mer informasjon, se den [Skriptalternativer for Superbrukere](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md#BKMK_RMSProtectionModule) delen i den [Konfigurere Superbrukere for Azure Rights Management og tjenester for oppdagelse eller gjenoppretting av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md) emnet.

|Hvis du vil...|.. .bruke følgende cmdleter|
|------------------|-------------------------------|
|Migrere fra lokale Rights Management (AD RMS eller Windows RMS) til [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Importer AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Koble til eller fra den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjeneste for organisasjonen.|[Koble AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Koble AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Generere og behandle dine egne leier nøkkel – ta din egen nøkkel (BYOK)-scenario.|[Legge til AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Aktivere eller deaktivere den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjeneste for organisasjonen.|[Aktiver Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Deaktiver Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Deaktivere eller aktivere dokumentet sporingsområdet for Azure Rights Management.|[Deaktiver AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Aktiver AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Konfigurere kort kontroller for en tretrinns distribusjon av Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Sett AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Opprett og administrer policymaler for rettigheter for organisasjonen.|[Legge til AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Eksport av AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Importer AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[Nye AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Fjern AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Sett AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Konfigurer maksimalt antall dager som kan få tilgang til innhold som organisasjonen beskytter uten en Internett-tilkobling (Bruk lisens gyldighetsperioden).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Sett AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Administrere funksjonen superbruker av [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] for organisasjonen.|[Aktiver AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Deaktiver AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Legge til AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Fjern AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629405.aspx)|
|Behandle brukere og grupper som har tillatelse til å administrere den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjeneste for organisasjonen.|[Legge til AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Fjern AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Få en logg over [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administrative oppgaver for organisasjonen.|[Get-AadrmAdminLog](http://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Logg og analysere brukslogging [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Aktiver AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629421.aspx)<br /><br />[Get-AadrmUsageLog](http://msdn.microsoft.com/library/azure/dn629401.aspx)<br /><br />[Get-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629425.aspx)<br /><br />[Get-AadrmUsageLogLastCounterValue](http://msdn.microsoft.com/library/azure/dn629423.aspx)<br /><br />[Get-AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629419.aspx)<br /><br />[Sett AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629426.aspx)<br /><br />[Deaktiver AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629404.aspx)|
|Vise gjeldende [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjenestekonfigurasjon for organisasjonen.|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Overføre organisasjonen fra [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] til en lokale AD RMS-distribusjon.|[Sett AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

## Se også
[Azure Rights Management](../Topic/Azure_Rights_Management.md)

