---
description: na
keywords: na
title: View and use files that have been protected by Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
---
# Vise og bruke filer som er beskyttet av IRM
Når den [RMS (Rights Management) deler program er installert på datamaskinen](https://technet.microsoft.com/library/dn574734%28v=ws.10%29.aspx), du viser en beskyttet fil ved å dobbeltklikke den. Filen kan være et vedlegg i en e-postmelding, eller du kan se den når du bruker Filutforsker.

> [!NOTE]
> Før du kan vise den beskyttede filen, RMS må du først bekrefte at du har tillatelse til å vise filen, det gjør det ved å kontrollere brukernavn og passord. I noen tilfeller kan dette være bufret og du får ikke en melding der du blir spurt om legitimasjon. I andre tilfeller blir du bedt om å oppgi legitimasjon.
> 
> Hvis organisasjonen ikke bruker enten Azure Rights Management (Azure RMS) eller AD RMS, kan du søke om en gratis konto som godtar legitimasjonsbeskrivelsene dine slik at du kan åpne filer som er beskyttet ved hjelp av RMS:
> 
> -   Hvis du vil bruke for denne kontoen, klikker du koblingen skal gjelde for [RMS for enkeltpersoner](http://go.microsoft.com/fwlink/?LinkId=309469).
> 
>     Når du registrerer deg, kan du bruke firmaets e-postadresse i stedet for en personlig e-postadresse. Hvis du registrerer deg fordi du er en e-postmelding en beskyttet vedlegg, kan du bruke samme e-postadressen som ble brukt til å sende deg e-postmeldingen.
> -   Hvis du vil ha mer informasjon, se [RMS for enkeltpersoner og Windows Azure Rights Management](http://technet.microsoft.com/library/dn592127.aspx).

## <a name="BKMK_ViewPFILE"></a>Slik viser du en beskyttet fil
Ved hjelp av File Explorer eller i e-postmeldingen som inneholder vedlegget, dobbeltklikker du den beskyttede filen, og angi dine legitimasjoner Hvis du blir bedt om å gjøre dette.

Hvis du ser to versjoner av filen, men med forskjellige filtyper, åpner du filen med filtypen .ppdf bare hvis den andre filen ikke åpnes. Hvis du ikke kan åpne den .ppdf versjonen enten, først installere det [RMS deling program](http://technet.microsoft.com/library/dn574734.aspx), som vet hvordan du kan åpne filer som har filtypen .ppdf.

> [!NOTE]
> Hvis du vil ha mer informasjon, se "[Hva er filen .ppdf som er opprettet automatisk?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_PPDF)".

Hvordan filen åpnes, avhenger av hvordan den er beskyttet, som du kan fortelle ved å se på filtypen. I hvert tilfelle filen åpnes kan overvåkes og forblir overvåkes så lenge den er beskyttet. I tillegg, hvis filen ble sendt som et e-postvedlegg, kan avsenderen bli varslet via e-post hver gang du åpner filen.

|Filtypen og beskyttelse|Hvis du vil ha mer informasjon|
|---------------------------|----------------------------------|
|Filen har en **.pfile** filtype.<br /><br />Filen ble generisk beskyttet.|Når du åpner filen, ser du en **beskyttet fil** dialogboksen fra deling programmet som forteller deg hvem som beskyttede filen, og du er forventet å overholde medeier tillatelsene. Klikk **Åpne** å lese filen.<br /><br />![](../Image/ADRMS_MSRMSApp_PfilePermission.png)|
|Filen har en **.ppdf** filtype eller er en beskyttet fil tekst eller bilde (som **.ptxt** eller **.pjpg**).<br /><br />Filen har blitt beskyttet opprinnelig som en skrivebeskyttet kopi.|Filen åpnes ved hjelp av visningsprogrammet som installerer RMS deling av programmet. Denne filen er skrivebeskyttet, selv om du lagrer den på en annen plassering eller gi den nytt navn.|
|Andre filtyper.<br /><br />Filen har blitt beskyttet opprinnelig.|Filen åpnes ved hjelp av programmet som er knyttet til den opprinnelige filtypen, og et banner for begrensning vises øverst i filen. Banneret kan vise tillatelsene som er brukt i filen, eller det kan inneholde en kobling for å vise dem. For eksempel vises kanskje følgende der du må klikke **tillatelsen er for øyeblikket begrenset** å se de faktiske tillatelsene som er brukt i filen, og personer som har tilgang til den:<br /><br />![](../Image/ADRMS_MSRMSApp_RestrictedAccess.png)|
For en fullstendig liste over filtyper som støtter rettighetsbehandling, kan du se de [Støttede filtyper og filtypeangivelser i filnavn](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes) delene i den  [Rights Management deling program administratorhåndboken](../Topic/Rights_Management_sharing_application_administrator_guide.md). Hvis din filtypen ikke vises, kan du bruke et websøk for å se om det er en filtype som støttes av et annet program.

> [!NOTE]
> Hvis, etter å ha bekreftet at filen er beskyttet av IRM, og filen åpnes ikke, laster du ned og bruker den [RMS Analyzer tool](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Følg instruksjonene i verktøyet for å løse problemer på datamaskinen som kan forhindre at et beskyttet dokument åpnes.

## <a name="BKMK_UserDefined"></a>Bruke filer som er beskyttet (for eksempel, Rediger og Skriv ut filen)
Hvis du vil mer enn bare å lese den når du har åpnet den beskyttede filen, (for eksempel redigere, kopiere og skrive den ut):

|Filtypen|Instruksjoner|
|------------|-----------------|
|Filen har en **.pfile** filtype.|Lagre den åpne filen, og gi den nye filtypen som er knyttet til programmet du vil bruke.<br /><br />For eksempel hvis en fil er beskyttet ved hjelp av filen navnet document.vsdx.pfile, vise filen og i filen Explorer lagre filen som document.vsdx.<br /><br />Den nye filen er ikke lenger beskyttet. Hvis du vil beskytte den, må du gjøre dette manuelt. For instruksjoner, se [Beskytte en fil på en enhet &#40;beskytte på plass&#41; ved hjelp av rettighetsadministrasjon deling av program](../Topic/Protect_a_file_on_a_device__protect_in-place__by_using_the_Rights_Management_sharing_application.md).|
|Filen har en **.ppdf** filtype eller er en beskyttet fil tekst eller bilde (som **.ptxt** eller **.pjpg**).|Du kan bare vise filen, og hvis du gir nytt navn til eller flytte den, forblir beskyttelsen med filen.|
|Andre filtyper.|Enheten må ha et program som forstår Rights Management til å bruke disse filene. Disse programmene kalles RMS-enlightened programmer. Programmer fra Office-2016, 2013 for Office og Office 2010 (for eksempel Word, Excel, PowerPoint og Outlook) er eksempler på programmer som er enlightened for Rights Management. Men programmer som ikke kommer fra Microsoft, for eksempel andre programvareselskaper og dine egne LOB programmer kan også enlightened for Rights Management.<br /><br />Programmer som er enlightened for rettighetsadministrasjon vet hvordan du åpner filer som er beskyttet av andre Rights Management enlightened programmer. De også beholdes beskyttelsen som skal brukes på dem, selv om du kan redigere filen eller lagre den på et annet navn eller en annen plassering. Disse programmene kan du bruke filen i henhold til tillatelsene som er brukt i filen, slik at hvis du har tillatelse til å bruke filen, kan du gjøre dette. Du kan for eksempel være stand til å redigere filen, men ikke skrive den ut.|

## Eksempler og andre instruksjoner
For eksempler på hvordan du kan bruke IRM deling av programmet, og hvordan-instruksjoner, kan du se følgende deler fra Rights Management-brukerhåndboken for deling program:

-   [Eksempler for å bruke RMS deling av program](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [Hva vil du gjøre?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Se også
[Rights Management deling program Brukerhåndbok](../Topic/Rights_Management_sharing_application_user_guide.md)

