---
description: na
keywords: na
title: Installing Windows PowerShell for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
---
# Installere Windows PowerShell for Azure Rights Management
Bruk informasjonen nedenfor for å hjelpe deg med å installere Windows PowerShell for Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS).

Du kan bruke denne modulen for Windows PowerShell til å administrere [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] fra kommandolinjen ved hjelp av en hvilken som helst datamaskin som har en Internett-tilkobling, og som oppfyller forutsetningene som er oppført i neste avsnitt. Windows PowerShell for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] støtter skript for automatisering eller kan være nødvendig for konfigurasjon av avanserte scenarier. Hvis du vil ha mer informasjon om administrative oppgaver og konfigurasjoner som modulen støtter, se [Administrasjon av Azure Rights Management ved hjelp av Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Forutsetninger
Denne tabellen inneholder forutsetningene for å installere og bruke Windows PowerShell for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

|Krav|Hvis du vil ha mer informasjon|
|--------|----------------------------------|
|En versjon av Windows som støtter den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administrasjonsmodulen|Kontroller listen over operativsystemer som støttes i den **Systemkrav** delen av den [nedlastingssiden for administrasjonsverktøy for Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Minimumsversjon av Windows PowerShell: 2.0|Støtte for den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administrasjonsmodulen introduseres i Windows PowerShell 2.0.<br /><br />Som standard i de fleste Windows-operativsystemer installert med minst versjon 2.0 av Windows PowerShell. Hvis du må installere Windows PowerShell 2.0, kan du se [installere Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx). **Tip:** Du kan kontrollere hvilken versjon av Windows PowerShell som du kjører ved å skrive inn **$PSVersionTable** i en Windows PowerShell-økt.|
|Minste versjon av Microsoft .NET Framework: 4.5 **Tip:** Denne versjonen av Microsoft .NET Framework er inkludert i senere operativsystemer, så du bør bare trenger å installere den manuelt hvis klientoperativsystemet er mindre enn Windows 8.0 eller server-operativsystemet er mindre enn Windows Server 2012.|Hvis dette ikke allerede er installert, kan du laste ned den [Microsoft for .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Denne versjonen av Microsoft .NET Framework er nødvendig for noen av klassene som den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administrasjonsmodulen brukes.|
|Microsoft Online Services Sign-In Assistant 7.0|Microsoft Online Services Sign In hjelperen er nødvendig for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] godkjenning.<br /><br />Hvis du vil ha mer informasjon, kan du se [Download Center: Assistent for IT-teknikere RTW for Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=41950).|

## Slik installerer du administrasjonsmodulen Rights Management

1.  Gå til Microsoft Download Center og [laste ned verktøyet for Azure Rights Management-Administrasjon](https://go.microsoft.com/fwlink/?LinkId=257721), som inneholder den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] Administrasjon-modul for Windows PowerShell.

2.  Fra den lokale mappen der du lastet ned og lagret den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] installer filen, dobbeltklikker du den kjørbare filen som du lastet ned for plattformen (WindowsAzureADRightsManagementAdministration_x64 eller WindowsAzureADRightsManagementAdministration_x86.exe) for å starte Azure AD Rights Management Administrasjon installasjonsveiviseren.

3.  Fullføre veiviseren.

Windows PowerShell for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] er nå installert.

## Neste trinn
Hvis du vil se hvilke cmdleter som er tilgjengelige, kan du starte Windows PowerShell med den **Kjør som administrator** alternativet, og Skriv inn følgende:

```
Get-Command -Module aadrm
```
Bruk `the Get-Help <cmdlet_name>` kommando for å se Hjelp for en bestemt cmdlet.

For mer informasjon:

-   Fullstendig liste over cmdleter som er tilgjengelige: [Azure Rights Management-cmdleter](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Liste over største konfigurasjon scenarier som støtter Windows PowerShell: [Administrasjon av Azure Rights Management ved hjelp av Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

Før du kan kjøre kommandoer som konfigurerer den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] service, må du koble til tjenesten ved hjelp av den [koble til AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) cmdleten. Når du er ferdig med å kjøre konfigurasjonskommandoer som du vil koble fra tjenesten ved hjelp av den [Koble fra AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdleten.

> [!NOTE]
> Hvis du ennå ikke har aktivert [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], kan du gjøre dette etter at du har koblet til tjenesten, ved hjelp av den [Aktiver Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) cmdleten.

## Se også
[Administrasjon av Azure Rights Management ved hjelp av Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

