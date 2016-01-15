---
description: na
keywords: na
title: Frequently Asked Questions for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
---
# Vanlige sp&#248;rsm&#229;l for Azure Rights Management
Noen vanlige spørsmål om Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], også kalt Azure RMS:

## Hva trenger jeg for å distribuere Azure RMS, og hvordan jeg kom i gang?
Kontroller først [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md), som inneholder informasjon om alternativer for abonnement på sky, hvordan du kan bruke de lokale serverne med Azure RMS, hvilke distribusjonsscenarioer ikke er støttet, hvilke enheter og programmer støtte Azure RMS, og en kobling hvis du trenger en liste over IP-adresser og domener for brannmurer eller proxy-servere. Du vil kanskje også Kontroller de andre emnene den [Komme i gang med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md) delen, for å få en grunnleggende forståelse av hvordan [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] kan hjelpe deg med å beskytte organisasjonens data, hvordan det fungerer med programmer, hvordan det sammenligner med den lokale versjonen av Active Directory Rights Management, og forstå uttrykk og forkortelser som er spesifikke for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

Når du er klar til å teste Azure RMS for deg selv eller distribuere den for organisasjonen, bruker du [Veikart for Azure Rights Management-distribusjon](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) for en liste over trinn med koblinger for mer informasjon og fremgangsmåter instruksjoner.

Hvis du trenger ytterligere informasjon, ressurser og alternativer for kundestøtte, kan du se [Informasjon og støtte for Azure Rights Management](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

## Kan jeg integrere Azure RMS med min lokale servere?
Ja. Azure RMS kan integreres med dine lokale servere, for eksempel Exchange Server, SharePoint og Windows filservere. Hvis du vil gjøre dette, bruker du den [Rights Management-kontakt](https://technet.microsoft.com/library/dn375964.aspx). Hvis du bare er interessert i å bruke filen klassifisering infrastruktur (FC) med Windows Server, kan du bruke den [RMS beskyttelse cmdlets](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). Du kan også synkronisere og samle Active Directory-domenekontrollere med Azure AD for en mer sømløs godkjenning-opplevelse for brukere, for eksempel ved hjelp av [koble til Azure AD](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure RMS automatisk genererer og behandler XrML sertifikater etter behov, slik at den ikke bruker en lokale PKI. Hvis du vil ha mer informasjon om hvordan Azure RMS bruker sertifikater, se den [Gjennomgang av hvordan Azure RMS fungerer: Bruk først, beskyttelse, innhold forbruk av innhold](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Walthrough) delen i den [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emnet.

## Jeg har en hybrid distribusjon av Exchange med noen brukere på Exchange Online og andre på Exchange-serveren, er dette støttes av Azure RMS?
Absolutt, og fordel er at brukerne skal kunne beskytte sømløst og forbruker beskyttede e-postmeldinger og vedlegg på tvers av to Exchange-distribusjoner. For denne konfigurasjonen, [aktivere Azure RMS](https://technet.microsoft.com/library/jj658941.aspx) og [aktivere IRM for Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), deretter [distribueres og konfigureres RMS-koblingen](https://technet.microsoft.com/library/dn375964.aspx) for Exchange Server.

## Hvis jeg distribuere Azure RMS i produksjon, firmaet deretter låst i løsningen eller risiker å miste tilgangen til innhold som vi beskyttet med Azure RMS?
Nei, du alltid forblir i kontroll over dataene og kan fortsette å få tilgang til den, selv om du bestemmer deg for å ikke lenger bruker Azure RMS. Hvis du vil ha mer informasjon, se [Dekommisjonering og deaktivere Azure Rights Management](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

Men før du avslutte Azure RMS-distribusjon, vil vi gjerne høre fra deg, og forstå hvorfor du tok denne beslutningen. Hvis Azure RMS ikke oppfylle dine forretningskrav, ta kontakt med oss i tilfelle nye funksjoner er planlagt i nær-fremtiden, eller hvis det finnes alternativer. Send en e-postmelding til [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) og vi er glade for å diskutere dine tekniske og forretningsmessige behov.

## Kan jeg kontrollere hvilke av Mine brukere kan bruke Azure RMS for å beskytte innhold?
Ja, har Azure RMS brukerkontroller kort for dette scenariet. Hvis du vil ha mer informasjon, se den [Konfigurere kort kontroller for en tretrinns distribusjon](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls) delen i den [Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md) emnet.

## Kan jeg hindre brukere i å dele beskyttede dokumenter med bestemte organisasjoner?
En av de største fordelene med Azure RMS er at det støtter business-to-business samarbeid uten at du måtte konfigurere eksplisitt klareringer for hver partnerorganisasjon fordi Azure AD tar seg av godkjenning for deg.

Det finnes ingen administrative alternativer til å forhindre brukere fra å dele dokumenter på en sikker måte med bestemte organisasjoner. For eksempel du vil blokkere en organisasjon som du ikke stoler på, eller som har en konkurrerende virksomhet. Forhindrer sending av beskyttede dokumenter til brukere i disse Azure RMS ville ikke organisasjoner gir mening fordi brukerne kan deretter dele dokumentene ubeskyttet, som sannsynligvis er det siste du vil skal skje i dette scenariet! Du vil for eksempel ikke kunne identifisere som deler Konfidensielt for firmaet dokumenter med hvilke brukere i disse organisasjonene, som du kan gjøre når dokumentet (eller e-post) er beskyttet av Azure RMS.

## Når jeg deler et beskyttet dokument med noen utenfor firmaet, hvordan brukeren bli godkjent?
Azure RMS bruker alltid en Azure Active Directory-konto og en tilknyttet e-postadresse for brukergodkjenning, noe som gjør at business-to-business samarbeid sømløs for administratorer. Hvis andre organisasjonen bruker Azure tjenester, har brukerne allerede kontoer i Azure Active Directory, selv om disse kontoene opprettes og administreres av lokale og synkroniseres deretter til Azure.  Hvis organisasjonen har Office 365 under omslagene, bruker denne tjenesten også Azure Active Directory for brukerkontoene.  Hvis brukerens organisasjon ikke har administrerte kontoer i Azure, brukere kan abonnere på [RMS for enkeltpersoner](https://technet.microsoft.com/library/dn592127.aspx), som oppretter en ubehandlet Azure leier og mappen for organisasjonen med en konto for brukeren, slik at denne brukeren kan deretter godkjennes for Azure RMS.

Godkjenningsmetoden for disse kontoene kan variere, avhengig av hvordan administratoren i andre organisasjonen har konfigurert Azure Active Directory-kontoer. De kan for eksempel bruke passord som ble opprettet for disse kontoene, multifaktorautentisering (MFA), federation eller passord som ble opprettet i Active Directory Domain Services og deretter synkroniseres til Azure Active Directory.

## Kan jeg legge til brukere fra utenfor firmaet egendefinerte maler?
Ja.  Oppretter egendefinerte maler som sluttbrukerne (og administratorer) kan velge fra programmer gjør det raskt og enkelt for dem å bruke informasjonsbeskyttelse, ved hjelp av forhåndsdefinerte policyene du angir. En av innstillingene i malen er hvem som skal ha tilgang til innholdet, og du kan angi brukere og grupper fra i organisasjonen, og brukere utenfor organisasjonen.

Hvis du vil angi brukere utenfor organisasjonen, kan du bruke den [Windows PowerShell-modul for Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx). Du kan bruke disse alternativene:

-   **Eksport, Rediger og Importer den oppdaterte malen**:  Dette er den enkleste metoden hvis du vil legge til disse eksterne brukere i en eksisterende mal som inneholder andre grupper. Bruk av [eksport-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet til å eksportere malen til en. CSV-fil som du kan redigere for å legge til de eksterne e-postadressene for disse brukerne og deres rettigheter til eksisterende grupper og rettigheter. Deretter bruker du [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet til å importere denne endringen tilbake til Azure RMS.

-   **Bruker et objekt for definisjon av rettigheter til å opprette eller oppdatere en mal**:    Angi eksterne e-postadressene og deres rettigheter i en rettigheter definisjon-objektet, som du deretter kan bruke til å opprette eller oppdatere en mal. Du angi rettigheter definisjon objektet ved hjelp av den [Ny-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) cmdlet til å opprette en variabel, og deretter angir du denne variabelen til parameteren - RightsDefinition med de [Legg til AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) cmdlet (for en ny mal) eller [Sett AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) cmdlet (Hvis du endrer en eksisterende mal). Men hvis du legger til disse brukerne til en eksisterende mal, må du definere rettigheter definisjon objekter for eksisterende grupper i malene og ikke bare de eksterne brukerne.

Hvis du vil ha mer informasjon om egendefinerte maler, se [Konfigurere egendefinerte maler for Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

## Hvilke enheter og hvilke filtyper som støttes av Azure RMS?
En liste over enheter som støttes, kan du se den [Klientenheter som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices) delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet. Fordi ikke alle støttede enheter kan for tiden støtter alle RMS-funksjoner, må du også kontrollere den [Enheten klientegenskaper](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities) tabellen i det samme emnet.

Azure RMS kan støtte alle filtyper. For tekst, bilde, Microsoft Office (Word, Excel, PowerPoint)-filer, PDF-filer, og noen andre program-filtyper gir Azure RMS enhetlig beskyttelse som inkluderer både kryptering og håndhevelse av tillatelser (tillatelser). For alle andre programmer og filtyper gir generell beskyttelse filen innkapsling og godkjenning for å kontrollere om en bruker har tillatelse til å åpne filen.

For en liste over filtyper som støttes internt av Azure RMS, kan du se den [støttede filtyper og filtypeangivelser i Filnavn](http://technet.microsoft.com/library/dn339003.aspx) delen av den [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/dn339003.aspx). Filtyper som ikke er oppført som støttes ved hjelp av RMS deling av programmer som bruker automatisk Generell beskyttelse til disse filene.

## Når vil du støtte migrering fra AD RMS?
I utgangspunktet støtter ikke Azure RMS migrering fra en lokale distribusjon av Rights Management, for eksempel AD RMS. Men det er nå støttet.

Hvis du vil ha mer informasjon, se [Migrering fra AD RMS til Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).

## Vi virkelig ønsker å bruke BYOK med Azure RMS, men lærte du at dette ikke er kompatible med Exchange Online – Hva er ditt råd?
Ikke la dette gjeldende begrensning forsinke Azure RMS-distribusjon. Hvis du har Exchange Online og vil bruk bringe din egen nøkkel (BYOK), anbefaler vi at du distribuerer Azure RMS i standard Nøkkelbehandling modus nå, der Microsoft genererer og behandler nøkkelen. På denne måten får alle fordelene med å beskytte dine viktige filer og e-post nå, med mulighet for å flytte til BYOK senere (for eksempel når Exchange Online støtter BYOK).

Hvis din firmaets retningslinjer krever at du bruker en hardware sikkerhetsmodul (HSM), og dette ville ellers blokkere Azure RMS-distribusjon, er imidlertid et annet alternativ til å distribuere Azure RMS med BYOK nå, med redusert RMS-funksjonalitet for Exchange. Hvis du vil ha mer informasjon, se den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) delen i den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emnet.

## En funksjon som jeg leter etter virker ikke beskyttet biblioteker til å arbeide med SharePoint, er støtte for Mine funksjonen planlagt?
SharePoint støtter RMS beskyttede dokumenter ved hjelp av IRM beskyttet for øyeblikket, biblioteker, som ikke støtter egendefinerte maler, dokumentsporing og enkelte andre funksjoner.  Hvis du vil ha mer informasjon, kan du utvide den   [SharePoint Online- og OneDrive for bedrifter: IRM-konfigurasjonen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline) delen i den [Hvordan programmer støtter Azure rettighetsbehandling](../Topic/How_Applications_Support_Azure_Rights_Management.md) emnet.

Hvis du er interessert i en bestemt funksjon som ennå ikke er støttet, må du huske å holde øye med kunngjøringer den [RMS Teamblogg](http://blogs.technet.com/b/rms/).

## Hvordan kan jeg konfigurere én stasjon for bedrifter i SharePoint Online, slik at brukere kan trygt dele filer med personer innenfor og utenfor bedriften?
Som standard konfigurere som en Office 365-administrator kan du ikke dette. brukere gjøre.

På samme måte som en SharePoint-områdeadministrator aktiverer og konfigurerer IRM for et SharePoint-bibliotek som de eier, er OneDrive for bedrifter utformet for brukere å aktivere og konfigurere IRM for sine egne OneDrive for Business-biblioteket.  Men ved hjelp av PowerShell, kan du gjøre dette for dem. For instruksjoner, kan du utvide den [SharePoint Online- og OneDrive for bedrifter: IRM-konfigurasjonen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline)  delen i den [Konfigurere programmer for Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) artikkelen.

## Har du noen tips eller triks for en vellykket distribusjon av RMS?
Når øye mange distribusjoner og lytte til våre kunder samarbeider, opplever konsulenter og kundestøtteteknikere – en av de største tipsene vi kan gå på fra: **Utforming og distribuere policyer for enkle rettigheter**.

Fordi Azure RMS støtter deling med alle på en sikker måte, kan du råd til å være ambisiøse med din rekkevidde for beskyttelse av informasjon. Men være konservativ med kriterier for brukerrettigheter. For mange organisasjoner kommer den største forretningslivet fra hindrer data lekkasje ved å bruke standard rettigheter policymalen som begrenser tilgang til personer i organisasjonen. Selvfølgelig kan du få mye mer detaljert enn det som Hvis du trenger – hindre at personer utskrift, redigering osv. Men beholde mer sammensatt begrensningene som unntak for dokumenter som virkelig trenger sikkerhet på høyt nivå, og ikke implementerer disse mer restriktiv policyene på dag én, men planen for en mer tretrinns tilnærming.

## Hvilke funksjoner kan eller ikke kan brukes med ulike abonnementer for Azure RMS?
For betalte abonnementer som støtter Azure RMS (Office 365, Azure RMS Premium og Enterprise mobilitet Suite), er det noen forskjeller i RMS-funksjoner som støttes. For en liste over disse, kan du se [tilbud for sammenligning av Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

Gratis abonnement som støtter Azure RMS (RMS for enkeltpersoner) støtter tid innhold som er beskyttet av Azure RMS. Hvis du vil ha mer informasjon, se [RMS for enkeltpersoner og Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

## Hvor kan jeg få teknisk informasjon om gratis Azure RMS-abonnement (RMS for enkeltpersoner), for eksempel hvordan det virkelig fungerer, hvordan å ta kontroll over kontoer og hvilke domener ikke kan brukes?
Du finner svar på disse spørsmålene i den [RMS for enkeltpersoner og Azure Rights Management](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md) emnet.

## Hvordan vi få tilgang til filer som er beskyttet av en ansatt som har nå forlatt organisasjonen?
Bruk funksjonen superbruker av Azure RMS, som lar godkjente brukere har full eierrettigheter for alle lisenser for bruk som ble gitt av organisasjonens RMS leier. Denne samme funksjonen lar autorisert services-indeks og undersøker filer, etter behov.

Hvis du vil ha mer informasjon, se [Konfigurere Superbrukere for Azure Rights Management og tjenester for oppdagelse eller gjenoppretting av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

## Kan hindre Rights Management skjermavlesninger?
Rettighetsadministrasjon blokkerer skjermavlesninger fra de fleste brukte skjermen innspillingen verktøy, som kan bidra til å unngå tilfeldig eller negligent avsløring av konfidensiell eller sensitiv informasjon. Det finnes imidlertid mange måter at en bruker kan dele dataene som vises på skjermen, og å ta et skjermbilde er bare én måte. For eksempel en bruker utskriftsgjengivelse deling informasjonen som vises kan ta et bilde av den ved hjelp av deres kameratelefon, skrive inn dataene, eller ganske enkelt verbally videresende den til noen.

Som disse eksemplene viser, kan ikke alltid teknologi alene hindre brukere i å dele data som de ikke skal. Mens Rights Management kan bidra til å beskytte dine viktige data ved hjelp av godkjenning og bruk policyer, bør denne enterprise rights management-løsningen brukes sammen med andre kontroller. For eksempel implementere fysisk sikkerhet, skjermen nøye og overvåke personer som har autorisert tilgang til organisasjonens data, og investere i brukeropplæring slik at brukerne forstår hvilke data bør ikke deles.

## Hvor kan jeg finne støtteinformasjon for Azure RMS-for eksempel legal, samsvar og servicenivåavtaler?
Azure RMS støtter andre tjenester, og også avhengig av andre tjenester. Hvis du leter etter informasjon som er relatert til Azure RMS, men ikke om hvordan du bruker tjenesten Azure RMS, kan du se følgende ressurser:

**Juridiske og personvern:**

-   For informasjon om Microsoft Azure: [Microsoft Azure avtale](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   For Microsoft Azure personvern: [Personvernerklæring for Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

**Sikkerhet, samsvar og revisjon:**

Se den [Sikkerhet, samsvar og lovbestemte krav](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMScompliance) delen i den [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emnet. I tillegg:

-   For eksterne sertifiseringer for Azure RMS: [Microsoft Azure klareringssenteret](http://azure.microsoft.com/support/trust-center/)

-   FIPS 140-informasjon: [FIPS 140 validering](https://technet.microsoft.com/library/security/cc750357.aspx)

**Servicenivåavtaler:**

-   Servicenivåavtalen for Azure RMS, etter valgt land: [Servicenivåavtalen](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

-   Servicenivåavtalen for Azure Active Directory: [Servicenivåavtaler](http://azure.microsoft.com/support/legal/sla/)

**Dokumentasjon:**

-   Azure dokumentasjonen for Active Directory-område: [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Azure Active Directory-biblioteket: [Azure Active Directory](http://msdn.microsoft.com/library/azure/jj673460.aspx)

-   Office 365-biblioteket: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## Hva gjør jeg Hvis spørsmålet mitt er ikke her?
Bruk koblingene og ressursene som er oppført i [Informasjon og støtte for Azure Rights Management](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

I tillegg er vanlige spørsmål som er utformet for sluttbrukere:

-   [Vanlige spørsmål for rettighetsadministrasjon deling av programmer for Windows](https://technet.microsoft.com/dn467883)

-   [Vanlige spørsmål for rettighetsadministrasjon deling program for Mobile og Mac-plattformer](https://technet.microsoft.com/dn451248)

-   [Vanlige spørsmål for dokumentet sporing](http://go.microsoft.com/fwlink/?LinkId=523977)

Vanlige spørsmål om siden oppdateres jevnlig, med nye tillegg som er oppført i de månedlige kunngjøringene om dokumentasjon på den [Microsoft Rights Management (RMS) Team](http://blogs.technet.com/b/rms/) blogg.

> [!TIP]
> Du kan bruke den [docs koden](http://blogs.technet.com/b/rms/archive/tags/docs/) på bloggen, til mer enkelt finne disse kunngjøringene i dokumentasjonen.

## Se også
[Komme i gang med Azure Rights Management](../Topic/Getting_Started_with_Azure_Rights_Management.md)

