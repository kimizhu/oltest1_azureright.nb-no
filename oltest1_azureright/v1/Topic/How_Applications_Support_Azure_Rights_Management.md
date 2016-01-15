---
description: na
keywords: na
title: How Applications Support Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
---
# Hvordan programmer st&#248;tter Azure rettighetsbehandling
Bruk informasjonen nedenfor for å hjelpe deg med å forstå hvordan sluttbrukeren programmer (for eksempel i Office-programmer, Word, Excel, PowerPoint og Outlook) og tjenester (for eksempel Exchange og SharePoint) kan bruke Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] til å beskytte organisasjonens data:

-   [RMS deling program for Windows og mobile plattformer](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharingAppIntro)

-   [Office-programmer: Word, Excel, PowerPoint, Outlook](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_OfficeAppsIntro)

    -   [Exchange Online og Exchange Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_ExchangeIntro)

    -   [SharePoint Online og SharePoint Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharePointIntro)

-   [Servere som kjører Windows Server og bruke filen klassifisering infrastruktur (FCI)](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_FCIIntro)

-   [Andre programmer som støtter RMS-APIs](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_APIAppsIntro)

> [!NOTE]
> Kontrollere programmer og versjoner som [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) støtter, kan du se [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

I noen tilfeller brukes informasjonsbeskyttelse automatisk, i henhold til policyene du konfigurerer. Dette er for eksempel tilfellet med SharePoint-biblioteker, klassifisert filer og Exchange Transportregler. I andre tilfeller må brukere bruke informasjonsbeskyttelse seg fra sine programmer, enten ved å velge en mal eller velge bestemte alternativer. Dette er for eksempel tilfellet når brukere dele en fil via e-post eller beskytte en fil i stedet ved å begrense tilgangen til eller bruken til valgte brukere eller brukere utenfor organisasjonen.

Maler gjør det enklere for brukere (og administratorer konfigurere policyer) til å bruke riktig nivå av beskyttelse og begrense tilgangen til personer i organisasjonen. Selv om [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] leveres med to standardmaler sannsynligvis vil du opprette egendefinerte maler for å redusere ganger når de har til å angi flere alternativer. Hvis du vil ha mer informasjon, se [Konfigurere egendefinerte maler for Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

For tilfellene der brukerne må bruke informasjonsbeskyttelse, må du gi dem veiledning og instruksjonene for hvordan og når du gjør dette. Instruksjonene bør være spesifikke for programmet og versjoner som de bruker og hvordan de bruker dem, og retningslinjer for når og hvordan for å bruke informasjon beskyttelse må være riktig for din virksomhet. Hvis du vil ha mer informasjon, se [Hjelpe brukere til å beskytte filer ved hjelp av Azure Rights Management](../Topic/Helping_Users_to_Protect_Files_by_Using_Azure_Rights_Management.md).

Hvis du vil ha informasjon om hvordan du konfigurerer disse programmene for Azure RMS, se [Konfigurere programmer for Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

> [!TIP]
> Eksempler og skjermbilder av programmer som bruker RMS Azure, se den [Azure RMS i aksjon: Administratorer og brukere ser](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures) delen fra den [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emnet.

## <a name="BKMK_SharingAppIntro"></a>RMS deling program for Windows og mobile plattformer
RMS-deling-programmet er et gratis, nedlastbart program som er nødvendig for å støtte Office 2010, men også anbefalt for Windows-datamaskiner, Mac datamaskiner og mobile enheter. En av fordelene er at den kan bruke Generell beskyttelse for programmer og filer som ikke støtter innebygd [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], noe som betyr at alle filer kan være beskyttet. Hvis du vil ha mer informasjon om de forskjellige beskyttelsesnivåene, se den [nivå av beskyttelse – opprinnelig og generell](http://technet.microsoft.com/library/dn339003.aspx) delen fra den [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/dn339003.aspx).

Når brukere beskytter filene ved å bruke RMS kan deling program, de også spore dokumenter som de er beskyttet og oppheve tilgang til dem hvis det er nødvendig. Dette gjøres ved hjelp av den [dokumentsporing området](http://go.microsoft.com/fwlink/?LinkId=529562).

For Windows-datamaskiner, integreres med RMS deling program uhindret, og forbedrer programmene som brukerne allerede bruker:

-   En Office-tillegget for Word, Excel, PowerPoint og Outlook er installert. Dette gir brukere med en **del beskyttet** -knappen på båndet, som aktiverer en enkelt å bruke dialogboksen Innstillinger som er mest brukt til å beskytte filer som skal være en e-postmelding. Denne knappen gir også en rask måte å få tilgang til dokumentet sporingsområdet.

-   En ny Høyreklikk alternativet for Filutforsker. Dette gir brukere med en **beskytte på stedet** alternativ, som aktiverer en enkelt å bruke dialogboksen Innstillinger som er mest brukt til å beskytte filer som er lagret på en disk.

-   Et vindu for å åpne filer som er beskyttet av [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. Dette visningsprogrammet startes automatisk når det er ingen andre program installert som kan åpne den beskyttede filen.

-   Bakserveren konfigurasjonen for Office 2010 som gjør at Word, Excel, PowerPoint og Outlook fra denne pakken fungerer sømløst med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

Selv om deling av programmer for Windows RMS kan lastes ned og installeres for en enkelt datamaskin ved hjelp av den [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970), den støtter også en enterprise-distribusjon for stille installasjon og tilpasset konfigurering. Hvis du vil ha mer informasjon, kan du se følgende ressurser:

-   [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/dn339003.aspx)

-   [Rights Management deling program Brukerhåndbok](http://technet.microsoft.com/library/dn339006.aspx)

RMS deling program for mobile enheter som støtter de mest brukte mobile enhetene, for eksempel iPad og iPhone, Android, Windows Phone og Windows rett Brukere kan laste ned denne app fra det aktuelle lageret, og det finnes koblinger til disse fra den [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="BKMK_OfficeAppsIntro"></a>Office-programmer: Word, Excel, PowerPoint, Outlook
Disse programmene støtter rettighetsbehandling ved hjelp av IRM (IRM) opprinnelig og la brukerne bruke beskyttelse til et lagret dokument eller en e-postmelding som skal sendes. Brukere kan bruke maler eller velge svært tilpassede innstillinger for begrensninger for tilgang, rettigheter og bruk. Brukere kan for eksempel konfigurere en fil slik at den kan bare åpnes av personer i organisasjonen, eller kontroll om filen kan redigeres, eller begrenset til skrivebeskyttet, eller hindre at det skrives ut. Et utløpstidspunkt kan konfigureres for tid-sensitive filer, (direkte av brukere eller ved å bruke en mal) for når filen kan ikke åpnes. For Outlook, kan brukere også velge den **ikke Videresend** alternativet for å hindre at data lekkasje.

### <a name="BKMK_ExchangeIntro"></a>Exchange Online og Exchange Server
Når du bruker Exchange Online og Exchange Server, kan du bruke informasjonen rights management (IRM)-integrasjon, som gir mer informasjon om løsninger for beskyttelse:

-   **Exchange ActiveSync IRM** slik at mobile enheter kan beskytte og bruke beskyttede e-postmeldinger.

-   RMS-støtte for den **Outlook Web App**, implementert for Outlook-klienten på samme måte, slik at brukere kan beskytte e-postmeldinger med maler, eller ved å angi alternativer, og brukere kan lese og bruke beskyttede e-postmeldinger som sendes til dem.

-   **Beskyttelse regler** for Outlook-klienter som en administrator konfigurerer for å bruke automatisk RMS-malene til å sende e-post meldinger for angitt mottakere. For eksempel når intern e-post sendes til den juridiske avdelingen, de bare kan leses av medlemmer av den juridiske avdelingen, og kan ikke videresendes. Brukere ser beskyttelse brukes i e-postmeldingen før du sender den, og som standard, de kan fjerne den hvis de finner ut at det ikke er nødvendig. E-postmeldinger krypteres før de sendes. Hvis du vil ha mer informasjon, se [Outlook-regler for beskyttelse mot](http://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) og [oppretter du en regel for beskyttelse av Outlook](http://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) i Exchange-biblioteket.

-   **Transport regler** at en administrator konfigurerer for å bruke RMS-maler automatisk på e-post meldinger basert på Egenskaper, for eksempel avsender, mottaker, Meldingsemne og innholdet. Disse er lignende i konsept til regler for beskyttelse, men ikke la brukere fjerne beskyttelsen, kan brukes på Outlook Web Access og e-post sendt av mobile enheter og ikke kryptere e-postmeldinger før de sendes fra klienten. Hvis du vil ha mer informasjon, se [opprette en regel for beskyttelse av Transport](http://technet.microsoft.com/library/dd302432.aspx) i Exchange-biblioteket.

-   **Datapolicyer tap forebygging (DLP)** som inneholder sett med vilkår for å filtrere e-postmeldinger, og ta forholdsregler for å hindre tap av data for konfidensiell eller sensitiv innhold (for eksempel personlige opplysninger eller kredittkortinformasjon). Tips for policy kan brukes når sensitive data oppdages, til å varsle brukere de skal bruke informasjonsbeskyttelse, basert på informasjonen i e-postmeldingen. Hvis du vil ha mer informasjon, se [Data tap forebygging](http://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) i Exchange-biblioteket.

-   **Office 365 meldingskryptering** at bruker transport regler for å sende kryptert e-post til personer utenfor firmaet, og e-postmeldingen blir lest i en webleser med et grensesnitt som ligner på Outlook Web App. Du kan tilpasse tekst for ansvarsfraskrivelse og toppteksten i selskapets krypterte e-postmeldinger, og selv legge til firmalogoen. Hvis du vil ha mer informasjon, se [Office 365 meldingskryptering](http://office.microsoft.com/o365-message-encryption-FX104179182.aspx) fra webområdet for Office.

Hvis du bruker Exchange Server, kan du bruke beskyttelsesfunksjonene informasjon med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] ved å distribuere RMS-kobling, som fungerer som et relay mellom lokale servere og RMS cloud-tjeneste. Hvis du vil ha mer informasjon, se [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

### <a name="BKMK_SharePointIntro"></a>SharePoint Online og SharePoint Server
Når du bruker SharePoint Online eller SharePoint Server, kan du bruke informasjonen rights management (IRM)-integrasjon, som gjør at administratorer beskytte lister eller biblioteker, slik at når en bruker sjekker ut et dokument, filen er beskyttet slik at bare autoriserte personer kan vise og bruke filen etter informasjon beskyttelse policyene du angir. For eksempel kan filen være skrivebeskyttet, deaktivere kopiering av tekst, kan ikke lagre en lokal kopi, og forhindre utskrift av filen.

For lister og biblioteker brukes alltid informasjon om beskyttelse av en administrator aldri en sluttbruker. Og det er brukt på listen eller biblioteket nivå for alle dokumenter i beholderen, og ikke på individuelle filer.  Hvis du bruker SharePoint Online, kan brukere også bruke IRM til sine OneDrive for Business-biblioteket.

IRM-tjenesten må først aktiveres for SharePoint. Deretter angir du IRM (Information Rights Management) for et bibliotek. Når det gjelder SharePoint Online og OneDrive for bedrifter, kan brukerne også angi Information Rights Management for sine OneDrive for Business-biblioteket. SharePoint bruker ikke policymaler for rettigheter, selv om det er SharePoint konfigurasjonsinnstillinger som du kan velge som samsvarer mest mulig med innstillingene som du kan angi i maler.

Hvis du bruker SharePoint Server, kan du bruke beskyttelsesfunksjonene informasjon med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] ved å distribuere RMS-kobling, som fungerer som et relay mellom lokale servere og RMS cloud-tjeneste. Hvis du vil ha mer informasjon, se [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

> [!NOTE]
> Det finnes enkelte begrensninger når du bruker IRM med SharePoint:
> 
> -   Du kan ikke bruke standard eller egendefinerte maler som du administrerer i Azure portal.
> -   Filer som har en. PPDF-filtypen for beskyttet PDF-filer støttes ikke. Filer som har. PDF-filtypen, og som er opprinnelig beskyttet av RMS støttes når du bruker en PDF-leser som støtter RMS.
> -   Fordi Office på mobile enheter ikke støtter ennå RMS, disse enhetene må bruke en webleser til å vise filer som er beskyttet av RMS, og filene er skrivebeskyttet.

Azure RMS gjelder bruksbegrensninger og datakryptering for dokumenter når de er lastet ned fra SharePoint, og ikke når dokumentet er første opprettes i SharePoint eller lastes opp til biblioteket. Hvis du vil ha informasjon om hvordan dokumenter er beskyttet før de er lastet ned, kan du se [datakryptering i OneDrive for bedrifter og SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) fra SharePoint-dokumentasjonen.

Hvis du vil ha mer informasjon om hvordan du bruker Azure RMS med SharePoint, kan du se følgende artikkel fra Office-blogg: [Hva er nytt med Information Rights Management i SharePoint og SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## <a name="BKMK_FCIIntro"></a>Servere som kjører Windows Server og bruke filen klassifisering infrastruktur (FCI)
Når du konfigurerer Windows-Server til å bruke filen klassifisering infrastruktur, kan denne funksjonen File Server Resource Manager skanne lokale filer og avgjøre om de inneholder sensitive data. For filer som oppfyller disse kriteriene, kodes de med klassifisering egenskaper som definerer en administrator. Filen klassifisering infrastruktur kan da automatisk, i henhold til klassifiseringen. En av disse handlingene inkluderer å bruke informasjonsbeskyttelse av ved hjelp av [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] og distribusjon av Rights Management-koblingen (også kjent som RMS-kontakt). Office-filer er deretter automatisk beskyttet av Azure RMS.

Vil du beskytte alle filtyper, må du ikke bruke RMS-koblingen, men i stedet kjøre et Windows PowerShell-skript ved hjelp av cmdleter fra den [RMS-beskyttelse verktøyet](https://www.microsoft.com/en-us/download/details.aspx?id=47256).

Klassifisering-policyer er fullt ut konfigurerbar og svært utvidbar, slik at du kan hindre potensielle data lekkasje fra uautorisert og autoriserte brukere. Det kan også bidra til å redusere risikoen for at data lekkasje av nettverksadministratorer fordi du kan konfigurere policyer som ikke krever disse administratorer har tilgang til filene.

For instruksjoner for å distribuere og konfigurere RMS-kontakt for Office-filer, kan du se [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

For instruksjoner for å bruke Windows PowerShell-skriptet for alle filtyper, kan du se [RMS-beskyttelse med Windows Server-filen klassifisering infrastruktur &#40;FCI&#41;](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md).

## <a name="BKMK_APIAppsIntro"></a>Andre programmer som støtter RMS-APIs
Ved å bruke RMS-SDK, kan de interne utviklerne skrive LOB programmer støtter [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Hvordan informasjonsbeskyttelse er integrert med disse programmene, avhengig av hvordan de er skrevet. Hvis du for eksempel integreringen kan brukes automatisk med minimal brukermedvirkning kreves, eller for en mer tilpasset opplevelse, brukere kan bli bedt om å konfigurere innstillinger for å bruke informasjonsbeskyttelse av på filer. Hvis du vil ha mer informasjon om SDK, se den [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx).

På samme måte tilbyr mange programvareleverandører programmer for å gi informasjon beskyttelse løsninger, også kalt rettigheter (ERM) produkter for virksomhetsstyring. En populær eksempel er en PDF-leser som støtter [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] for bestemte plattformer. Du kan bruke tabellen i den [Enheten klientegenskaper](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities) delen av den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet til å identifisere programmer som støtter RMS (RMS-enlightened programmer), og deretter bruke et websøk til å kjøpe eller laste ned programmet.

> [!TIP]
> For programmer som nylig utgitte, kontrollere RMS fellesskapet kanaler, som vises i [Informasjon og støtte for Azure Rights Management](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

## Se også
[Komme i gang med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

