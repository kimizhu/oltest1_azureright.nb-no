---
description: na
keywords: na
title: Configuring Custom Templates for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
---
# Konfigurere egendefinerte maler for Azure Rights Management
Etter at du har aktivert Azure Rights Management (Azure RMS), er brukere automatisk kunne bruke to standardmaler som gjør det enkelt for dem å bruke policyer på sensitive filer som begrenser tilgangen til autoriserte brukere i organisasjonen. Disse to maler har begrensninger for policyen følgende rettigheter:

-   Skrivebeskyttet visning for beskyttet innhold

    -   Navn: **&lt; navn &gt; organisasjon - konfidensiell Vis bare**

    -   Bestemt tillatelse: Vis innhold

-   Lese eller endre tillatelser for beskyttet innhold

    -   Navn: **&lt; navn &gt; organisasjon - konfidensiell**

    -   Bestemte tillatelser: Vise innhold, lagre filen, redigere innhold, vise tildelte rettigheter, tillate makroer, Forward, svar, svar til alle

I tillegg til [RMS deling program](http://technet.microsoft.com/library/dn339006.aspx) lar brukere definere sitt eget sett med tillatelser. Og for Outlook-klienten og Outlook Web Access, kan brukere velge den **ikke Videresend** alternativ for e-postmeldinger.

Standardmalene kan være tilstrekkelig for mange organisasjoner. Men hvis du vil opprette dine egne egendefinerte policymaler for rettigheter, kan du gjøre dette. Grunnene for å opprette en egendefinert mal, omfatter følgende:

-   Du vil bruke en mal for å gi rettigheter til et delsett av brukerne i organisasjonen i stedet for alle brukere.

-   Du vil bare et delsett av brukerne skal kunne se og velge en mal (mal avdelinger) fra programmer i stedet for alle brukere i organisasjonen-se, og du kan velge malen.

-   Du vil definere en egendefinert høyre for en mal, for eksempel Vis og Rediger, men ikke kopiere og skrive ut.

-   Du vil konfigurere flere alternativer i en mal som inneholder en utløpsdato, og om innholdet kan åpnes uten en Internett-tilkobling.

Hvis brukerne skal kunne velge en egendefinert mal som inneholder innstillinger som disse, må du først opprette en egendefinert mal, konfigureres og deretter publisere den.

Bruk de følgende delene for å konfigurere og bruke egendefinerte maler:

-   [Hvordan du kan opprette, konfigurere og publisere en egendefinert mal](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToConfigureCustomTemplates)

-   [Slik kopierer du en mal](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates)

-   [Slik fjerner du maler (arkiv)](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToArchiveTemplates)

-   [Oppdatering av maler for brukerne](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates)

-   [Windows PowerShell-referanse](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_PowerShellTemplates)

## <a name="BKMK_HowToConfigureCustomTemplates"></a>Hvordan du kan opprette, konfigurere og publisere en egendefinert mal
Du kan opprette og behandle egendefinerte maler i Azure Management-portalen. Du kan gjøre dette direkte fra Azure Management-portalen, eller du kan logge på administrasjonssenteret Office 365, og velg den **Avanserte funksjoner for** for Rights Management, som sender deg til Azure Management-portalen.

Bruk følgende fremgangsmåter til å opprette, konfigurere og publisere egendefinerte maler for Rights Management.

#### Opprette en egendefinert mal

1.  Avhengig av om du logge på Office 365 administrasjonssenteret, eller Azure-Portal, gjør du ett av følgende:

    -   Fra den [Office 365 administrasjonssenteret](https://portal.office.com/):

        1.  I den venstre ruten klikker du **tjenesteinnstillinger**.

        2.  Fra den **tjenesteinnstillinger** klikker du **rights management**.

        3.  I den **beskytte informasjon** -delen, klikker du **Behandle**.

        4.  I den **rights management** -delen, klikker du **Avanserte funksjoner for**.

            > [!NOTE]
            > Hvis du ikke har aktivert Rights Management, klikker du først **aktivere** og bekrefte handlingen. Hvis du vil ha mer informasjon, se [Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).
            > 
            > Hvis du ikke har klikket **Avanserte funksjoner** før, når IRM er aktivert, følger du den på skjermen instruksjonene for å få en gratis Azure abonnement som er nødvendige for å få tilgang til portalen Azure.

            Velge **Avanserte funksjoner** laster Azure portalen, der du kan administrere **RIGHTS MANAGEMENT** for organisasjonens Azure Active Directory.

    -   Fra den [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  I den venstre ruten klikker du **ACTIVE DIRECTORY**.

        2.  Fra den **active directory** klikker du **RIGHTS MANAGEMENT**.

        3.  Velg mappen som skal behandle for Rights Management.

        4.  Hvis du ikke har aktivert Rights Management, klikker du **Aktiver** og bekrefte handlingen.

            > [!NOTE]
            > Hvis du vil ha mer informasjon, se [Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

2.  Opprette en ny mal:

    -   I Azure portal fra den **Komme i gang med Rights Management** Hurtigsøk startside, klikker du **opprette en ny policy rettighetsmal**.

        Hvis du ikke ser denne siden umiddelbart når du har fulgt instruksjonene for Office 365, kan du bruke navigation-instruksjonene ovenfor, for Azure portal.

3.  På de **legger til en ny policy rettighetsmal** side, velger du et språk som du skal skrive inn malen navnet og beskrivelsen som brukere vil se (du kan legge til flere språk for senere). Deretter skriver du inn et unikt navn og en beskrivelse, og klikk på fullført-knappen.

Fra den **Komme i gang med Rights Management** Hurtigsøk startside, klikk **administrere din policymaler for rettigheter**. Vil du se den nylig opprettede malen legges til i listen over skjemamaler med statusen **arkivert**. På dette stadiet, malen er opprettet, men ikke konfigurert, og er ikke synlige for brukerne.

#### Konfigurere og publisere en egendefinert mal

1.  Velg den nylig opprettede malen fra den **maler** side i Azure Management-portalen.

2.  Fra den **malen har blitt lagt til** Hurtigsøk startside, klikker du **Komme i gang** fra trinn 1, **konfigurere rettigheter for brukere og grupper,** deretter **Kom i gang nå** eller **legge til**, og deretter velger du brukere og grupper som har rettigheter til å bruke innhold som er beskyttet av den nye malen.

    > [!NOTE]
    > Brukerne eller gruppene som du velger, må ha en e-postadresse. Dette vil nesten alltid være tilfellet i et produksjonsmiljø, men i et enkelt testing miljø, må du kanskje legge til e-postadresser til brukerkontoer eller grupper.

    Som beste praksis, kan du bruke grupper i stedet for brukere, noe som forenkler administrasjonen av malene. Hvis du har Active Directory på lokaler og synkroniserer til Azure AD, kan du bruke e-post-grupper som er enten sikkerhetsgrupper eller distribusjonsgrupper. Hvis du vil gi tilgang til alle brukere i organisasjonen, vil det være mer effektivt å kopiere en av standardmalene som i stedet for å angi flere grupper. Hvis du vil ha mer informasjon, se den [Slik kopierer du en mal](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates) delen i dette emnet.

    > [!TIP]
    > Du kan senere legge til brukere fra utenfor organisasjonen til malen ved hjelp av den [Windows PowerShell-modul for Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx) og ved å bruke én av følgende metoder:
    > 
    > -   **Eksport, Rediger og Importer den oppdaterte malen**:  Dette er den enkleste metoden for å legge til eksterne brukere i en eksisterende mal som inneholder andre grupper. Bruk av [eksport-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) cmdlet til å eksportere malen til en. CSV-fil som du kan redigere for å legge til de eksterne e-postadressene for disse brukerne og deres rettigheter til eksisterende grupper og rettigheter. Deretter bruker du [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) cmdlet til å importere denne endringen tilbake til Azure RMS.
    > -   **Bruker et objekt for definisjon av rettigheter til å oppdatere en mal**:    Angi eksterne e-postadressene og deres rettigheter i en rettigheter definisjon-objektet, som du deretter kan bruke til å oppdatere malen. Du angi rettigheter definisjon objektet ved hjelp av den [Ny-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) cmdlet til å opprette en variabel, og deretter angir du denne variabelen til parameteren - RightsDefinition med de [Sett AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) cmdlet til å endre en eksisterende mal. Men hvis du legger til disse brukerne til en eksisterende mal, må du også definere rettigheter definisjon objekter for eksisterende grupper i malene og ikke bare de nye, eksterne brukerne.

3.  Klikk Neste, og Tildel deretter én av de oppførte rettighetene til valgte brukere og grupper.

    Bruk beskrivelsen vises for mer informasjon om hver rettighet (og egendefinerte rettigheter). Mer informasjon er også tilgjengelig i [Konfigurere bruksrettigheter for Azure Rights Management](../Topic/Configuring_Usage_Rights_for_Azure_Rights_Management.md). Programmer som støtter RMS kan imidlertid variere i hvordan de implementere disse rettighetene. Se dokumentasjonen for sine og gjøre dine egne tester med programmer som brukerne bruker til å kontrollere virkemåten før du distribuerer malen for brukere. Hvis du vil vise denne malen til bare administratorer for denne testingen, gjøre denne malen et avdelinger (trinn 6).

4.  Hvis du valgte **egendefinerte**, klikk Neste-knappen, og velg deretter de egendefinerte rettighetene.

    Men du kan bruke en hvilken som helst kombinasjon av rettighetene som er tilgjengelige i enkelte programmer, kanskje noen rettigheter har avhengigheter på andre individuelle rettigheter. Når dette er tilfellet, er avhengige rettigheter automatisk valgt.

    > [!TIP]
    > Vurder å legge til den **Kopier og trekke ut innhold** høyre og gi dette til valgte administratorer eller personell i andre roller som har ansvar for datagjenoppretting. Gi denne rettigheten, lar dem fjerne beskyttelsen ved behov, fra filer og e-postmeldinger som skal beskyttes ved hjelp av denne malen. Denne muligheten til å fjerne beskyttelsen på mal-nivået gir mer nyansert kontroll enn når du bruker funksjonen superbruker.

5.  Klikk fullført.

6.  Hvis du vil at malen skal vises for en undergruppe av brukere når de ser en liste over maler i programmer: Klikk **OMFANG** til å konfigurere dette som en mal for avdelinger, og klikk **Kom i gang nå**. Hvis ikke, går du til trinn 9.

    Mer informasjon om avdelinger maler: Som standard ser alle malene som er publisert for alle brukerne i Azure-katalogen og de kan deretter velge dem fra programmer når de ønsker å beskytte innhold. Hvis du vil at bestemte brukere bare se noen av de publiserte malene, må du begrense maler for disse brukerne. Deretter bare disse brukerne skal kunne velge disse malene. Andre brukere som du ikke angir ser ikke malene, og derfor kan ikke velges. Denne teknikken kan gjøre for å velge riktig mal enklere for brukerne, særlig når du oppretter maler som er utformet for å brukes av spesifikke grupper eller avdelinger. Brukerne ser bare maler som er utformet for dem deretter.

    Du har for eksempel opprettet en mal for personalavdelingen som gjelder skrivebeskyttet tillatelse for medlemmer i økonomiavdelingen. Slik at bare medlemmer i personalavdelingen kan bruke denne malen når de bruker rettighetsadministrasjon deling program, kalt omfang malen for e-post-aktiverte gruppen HumanResources. Deretter, bare medlemmer av denne gruppen se og kan bruke denne malen.

7.  På den **mal SYNLIGHET** velger brukere og grupper som kan se og velge malen fra RMS-enlightened-programmer. Som må før, som beste praksis, Bruk grupper i stedet for brukere, og brukerne eller gruppene du velger ha en e-postadresse.

8.  Klikk Neste, og avgjør om du trenger å konfigurere programkompatibilitet for malen for avdelinger. Hvis du gjør dette, klikker du **APPLICATION COMPATIBILITY**, merker du den, og klikk **fullført**.

    Hvorfor du må kanskje konfigurere programkompatibilitet? Ikke alle programmer kan støtte avdelinger maler. Hvis du vil gjøre dette, må det først godkjenne programmet med RMS-tjenesten før du laster ned maler. Hvis godkjenningsprosessen ikke oppstår, som standard, ingen av avdelinger malene lastes ned. Du kan overstyre denne virkemåten ved å angi at alle avdelinger malene skal laste ned, ved å konfigurere programkompatibilitet og velge den **Vis denne malen for alle brukere når programmene ikke støtter brukeridentiteten** merket.

    For eksempel, hvis du ikke konfigurerer programkompatibilitet for malen avdelinger i eksemplet vårt personale, se bare brukere i personalavdelingen malen avdelinger når de bruker RMS deling programmet, men ingen brukere se malen avdelinger når de bruker Outlook Web Access (OWA) fra Exchange Server-2013 Exchange OWA og Exchange ActiveSync for øyeblikket støtter ikke maler for avdelinger. Hvis du vil overstyre denne standardvirkemåten ved å konfigurere programkompatibilitet, ser bare brukere i personalavdelingen avdelingsnivå malen når de bruker RMS deling av programmet, men alle brukere se malen avdelinger når de bruker Outlook Web Access (OWA). Hvis brukerne bruker OWA eller Exchange ActiveSync fra Exchange Online, alle brukere vil se malene avdelinger eller ingen brukere vil se malene avdeling, basert på mal-status (arkivering eller publiserte) i Exchange Online.

    > [!NOTE]
    > Hvis du har programmer som ennå ikke støtter avdelingsnivå maler, kan du bruke en [Egendefinert RMS-malen nedlasting skript](http://go.microsoft.com/fwlink/?LinkId=524506) eller andre verktøy til å distribuere disse malene i mappen lokale RMS-klienten. Disse programmene vises deretter riktig avdelingsnivå malene til bare de brukerne og gruppene som du valgte for mal-området:
    > 
    > -   Office 2010, klient-mappen er **%localappdata%\Microsoft\DRM\Templates**.
    > -   Du kan kopiere og lime malfilene til andre datamaskiner fra en klientdatamaskin som er lastet ned alle malene.
    > 
    > Office-2016 støtter maler for avdelinger, og så støtter Office-2013 har de siste oppdateringene for Office ([KB 3054853](https://support.microsoft.com/kb/3054853)).

9. Klikk **Konfigurer** og legge til flere språk som brukerne bruker, sammen med navnet på og beskrivelsen av denne malen på dette språket. Når du har brukere med flere språk, er det viktig å legge til hvert språk de bruker, og angi et navn og en beskrivelse i dette språket. Brukerne ser deretter navnet på og beskrivelsen av malen på samme språk som sin klient-operativsystem, som sikrer at de forstår policyen som gjelder for et dokument eller en e-postmelding. Hvis det ikke samsvarer ikke med sine klientoperativsystem, går navnet og beskrivelsen som ser de tilbake til språket og beskrivelsen du definerte da du først opprettet malen.

    Deretter sjekker du om du vil gjøre endringer i følgende innstillinger:

    |Innstillingen|Hvis du vil ha mer informasjon|
    |-----------------|----------------------------------|
    |**utløpsdato for innhold**|Angi en dato eller et antall dager for denne malen når filer som er beskyttet av malen ikke åpnes. Du kan angi en dato eller et antall dager fra tidspunktet for beskyttelse brukes for filen.<br /><br />Når du angir en dato, er det effektive midnatt i gjeldende tidssone.|
    |**frakoblet tilgang**|Bruk denne innstillingen til å balansere noen sikkerhetskrav at du har mot behovene som brukerne må være i stand til å åpne beskyttede filer når de ikke har en Internett-tilkobling.<br /><br />Hvis du angir at innholdet er ikke tilgjengelig uten en Internett-tilkobling eller innholdet er bare tilgjengelig for et angitt antall dager, når denne terskelen er nådd, brukere må være godkjent på nytt og deres tilgang er logget. Når dette skjer, hvis legitimasjonen ikke blir bufret, blir brukere bedt om å logge på før de kan åpne filen.<br /><br />I tillegg til godkjenning på nytt er policyen og gruppemedlemskap for brukeren på nytt evaluert. Dette betyr at brukerne får forskjellige tilgangsresultater for den samme filen hvis det er endringer i medlemskapet policy eller en gruppe fra når de sist åpnet filen.|

10. Når du er sikker på at malen er konfigurert på riktig måte for brukere, klikker du **Publiser** å gjøre malen synlig for brukere, og klikk deretter **Lagre**.

11. Klikk Tilbake-knappen i Management-portalen for å gå tilbake til den **maler** -siden der malen nå har en oppdatert status på **publisert**.

Hvis du vil gjøre endringer i malen, merker du den og deretter bruke Hurtigstart-trinn. Eller velg ett av følgende alternativer:

-   Du legger til flere brukere og grupper, og definerer rettighetene for disse brukerne og gruppene: Klikk **rettigheter**, deretter **legge til**.

-   Slik fjerner du brukere eller grupper som du tidligere har valgt: Klikk **rettigheter**, merker du brukeren eller gruppen fra listen, og klikk deretter **SLETTER**.

-   Slik endrer du hvilke brukere som kan se maler å velge dem fra programmer: Klikk **OMFANG**, deretter **legge til** eller **SLETTER**, eller **APPLICATION COMPATIBILITY**.

-   Du kan bruke malen ikke lenger synlig for alle brukere: Klikk **Konfigurer**, klikker du **ARKIV**, og klikk deretter **Lagre**.

-   Foreta andre konfigurasjonsendringer: Klikk **Konfigurer**, foreta endringene, og klikk deretter **Lagre**.

> [!WARNING]
> Når du gjør endringer i en mal som ble lagret tidligere, se klienter ikke disse endringene i malen til maler er oppdatert på sine datamaskiner. Hvis du vil ha mer informasjon, se den [Oppdatering av maler for brukerne](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates) delen i dette emnet.

## <a name="BKMK_HowToCopyTemplates"></a>Slik kopierer du en mal
Hvis du vil opprette en ny mal som er veldig like innstillinger til en eksisterende mal, velger du den opprinnelige malen på den **maler** klikker du **Kopier**, angi et unikt navn og gjør endringene du trenger.

> [!IMPORTANT]
> Når du kopierer en mal, den **publisert** eller **arkivert** status kopieres også. Så hvis du kopierer et publisert mal, umiddelbar statusen vil være publisert, med mindre du endrer den.

Du kan kopiere egendefinerte maler og standardmalene. Som beste praksis, kan du kopiere en av standardmalene som i stedet for å opprette en ny egendefinert mal hvis du vil at malen skal gi rettigheter til alle brukerne i organisasjonen. Denne metoden betyr at du ikke trenger å opprette eller velge flere grupper til å angi alle brukere. I dette scenariet, må du angi et nytt navn og beskrivelse for den kopierte malen for flere språk.

## <a name="BKMK_HowToArchiveTemplates"></a>Slik fjerner du maler (arkiv)
Standardmaler kan ikke slettes, men de kan arkiveres slik at brukerne ikke ser dem.

På samme måte, hvis du har publisert en egendefinert mal og ikke lenger vil at brukere skal kunne se det, du kan redigere malen og velger **ARKIV** og **Lagre** fra den **Konfigurer** siden. Du kan velge den fra den **maler** siden og velg **ARKIV**.

Fordi du ikke kan redigere standardmalene, hvis du vil arkivere disse malene må du bruke det **ARKIV** alternativ fra den **maler** siden. Du kan arkivere Outlook **ikke Videresend** alternativet.

#### Slik fjerner du en standardmal

-   Fra den **maler** velger du standardmalen, og klikk **ARKIV**.

Statusen endres fra **publisert** til **arkivert**. Hvis du ombestemmer deg, velger du malen og velger **Publiser**.

## <a name="BKMK_RefreshingTemplates"></a>Oppdatering av maler for brukerne
Når du bruker Azure RMS, ned maler automatisk til klientmaskiner slik at brukere kan velge dem fra sine programmer. Du må imidlertid ta forholdsregler Hvis du gjør endringer i listen over maler:

|Program eller tjeneste|Hvordan maler er oppdatert etter endringer|
|--------------------------|----------------------------------------------|
|Exchange Online|Manuell konfigurasjon kreves for å oppdatere maler.<br /><br />For at konfigurasjonstrinnene, utvider du delen nedenfor [Exchange Online bare: Slik konfigurerer du Exchange for å laste ned endret egendefinerte maler](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_ExchangeOnlineTemplatesUpdate).|
|Office 365|Automatisk oppdatert – ingen flere trinn kreves.|
|2016 for Office og Office-2013<br /><br />Deling av programmer for Windows RMS|Automatisk oppdatert – en tidsplan:<br /><br />-   For disse senere versjoner av Office: Standard oppdateringsintervall er hver 7 dager.<br />-   For RMS deling av programmer for Windows: Fra og med versjon 1.0.1784.0, er standard oppdateringsintervall hver 1 dag. Tidligere versjoner har en standard Oppdateringsintervall for hver 7 dager.<br /><br />Utvid delen nedenfor for å fremtvinge en oppdatering tidligere enn denne tidsplanen [2016 for Office, Office-2013 og RMS deling av programmer for Windows: Slik tvinger du en oppdatering for et endret egendefinert mal](#BKMK_Office2013ForceUpdate).|
|Office 2010|Oppdatert når brukere logger seg.<br /><br />Hvis du vil fremtvinge en oppdatering, kan du be eller tvinge brukere til å logge av, og Logg på igjen på nytt. Eller, kan du se delen nedenfor [Office 2010: Slik tvinger du en oppdatering for et endret egendefinert mal](#BKMK_Office2010ForceUpdate).|
For mobile enheter som bruker RMS deler programmet, maler automatisk nedlasting (og oppdatert om nødvendig) uten ytterligere konfigurasjon er nødvendig.

### <a name="BKMK_ExchangeOnlineTemplatesUpdate"></a>Exchange Online bare: Slik konfigurerer du Exchange for å laste ned endret egendefinerte maler
Hvis du allerede har konfigurert (IRM-Information Rights Management) for Exchange Online, ned egendefinerte maler ikke for brukere, før du gjør følgende endringer ved hjelp av Windows PowerShell i Exchange Online.

> [!NOTE]
> Hvis du vil ha mer informasjon om hvordan du bruker Windows PowerShell i Exchange Online, kan du se [ved hjelp av PowerShell med Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Du må gjøre dette hver gang du endrer en mal.

##### Oppdatere maler for Exchange Online

1.  Hvis du bruker Windows PowerShell i Exchange Online, koble til tjenesten:

    1.  Oppgi Office 365-brukernavn og passord:

        ```
        $Cred = Get-Credential
        ```

    2.  Koble til Exchange Online-tjenesten ved å kjøre følgende to kommandoer:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Bruk av [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) cmdlet å importere på nytt klarerte publisering domenet (TPD) fra Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Hvis navnet på TPD er for eksempel **RMS Online - 1** (et vanlig navn for mange organisasjoner), skriver du inn: **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Hvis du vil kontrollere navnet ditt TPD, kan du bruke den [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) cmdleten.

3.  Vent noen minutter for å bekrefte at malene er importert, og deretter kjøre den [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) cmdlet og angi Type for alle. For eksempel:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > Det er nyttig å beholde en kopi av utdata, slik at du kan enkelt kopiere navn eller GUIDer Hvis du arkiverer en mal senere.

4.  For hver importerte malen som du vil skal være tilgjengelige i Outlook Web App, må du bruke den [Sett RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet og angi typen til distribuert:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Fordi Outlook Web Access bufrer Brukergrensesnittet i 24 timer, kan ikke brukerne se den nye malen for opp til en dag.

Hvis du arkiverer en mal (egendefinert eller standard) og bruke Exchange Online med Office 365 brukere vil se arkiverte maler hvis de bruker Outlook Web App eller mobile enheter som bruker Exchange ActiveSync-protokollen.

Slik at brukere kan ikke lenger se disse malene, koble til tjenesten ved hjelp av Windows PowerShell i Exchange Online, og bruk deretter den [Sett RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet ved å kjøre følgende kommando:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

### <a name="BKMK_Office2013ForceUpdate"></a>2016 for Office, Office-2013 og RMS deling av programmer for Windows: Slik tvinger du en oppdatering for et endret egendefinert mal
Du kan endre automatiske tidsplanen ved å redigere registret på datamaskinene som kjører Office-2016, Office 2013 eller RMS (Rights Management) deling av programmer for Windows, slik at endrede maler oppdateres oftere enn standardverdien på datamaskiner. Du kan også tvinge en umiddelbar oppdatering ved å slette de eksisterende data i en registerverdi.

> [!WARNING]
> Hvis du bruker Registerredigering på feil måte, kan du forårsake alvorlige problemer som krever at du installerer operativsystemet på nytt. Microsoft kan ikke garantere at du kan løse problemer som er forårsaket av feil bruk av Registerredigering. Bruk Registerredigering på egen risiko.

##### Å endre tidsplanen for automatisk

1.  Registerredigering, opprette og angi en av følgende registerverdier:

    -   Angi en oppdateringsfrekvens i dager (minimum 1 dag):  Opprett en ny registerverdi kalt **TemplateUpdateFrequency** og definere en heltallsverdi for data, som angir frekvensen i dager for å laste ned eventuelle endringer til nedlastede malen. Bruk tabellen nedenfor til å finne registerbane for å opprette denne nye registerverdien.

        |Registerbane|Type|Verdi|
        |----------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequency|

    -   Angi en oppdateringsfrekvens i sekunder (minimum 1 sekund):  Opprett en ny registerverdi kalt **TemplateUpdateFrequencyInSeconds** og definere en heltallsverdi for data, som angir frekvensen i sekunder å laste ned eventuelle endringer til nedlastede malen. Bruk tabellen nedenfor til å finne registerbane for å opprette denne nye registerverdien.

        |Registerbane|Type|Verdi|
        |----------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequencyInSeconds|

    Kontroller at du oppretter og sette inn én av disse registerverdiene ikke begge deler. Hvis begge er til stede, **TemplateUpdateFrequency** ignoreres.

2.  Hvis du vil tvinge en umiddelbar oppdatering av malene, kan du gå til neste prosedyre. Hvis ikke, Start Office-programmer og forekomster av File Explorer nå.

##### Hvis du vil tvinge en umiddelbar oppdatering

1.  Bruk av Registerredigering, slette data for det **LastUpdatedTime** verdi. Dataene kan for eksempel vise **2015-04-20T15:52**; slette 2015-04-20T15:52 slik at ingen data vises. Bruk tabellen nedenfor til å finne registerbane Hvis du vil slette denne verdien registerdata.

    |Registerbane|Type|Verdi|
    |----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\ &lt; MicrosoftRMS_FQDN &gt; \Template|REG_SZ|LastUpdatedTime|
    > [!TIP]
    > I registerbane, *&lt; MicrosoftRMS_FQDN &gt;* refererer til Microsoft RMS-tjenesten FQDN. Hvis du vil kontrollere denne verdien:
    > 
    > 1.  Kjøre den [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdleten for Azure RMS. Hvis du ikke allerede har installert Windows PowerShell-modul for Azure RMS, se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).
    > 2.  Fra utdataene, kan du identifisere den **LicensingIntranetDistributionPointUrl** verdi.
    > 
    >     For eksempel: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  Fra-verdien, kan du fjerne **https://** og **/_wmcs/lisensiering** fra denne strengen. Den gjenværende verdien er tjenesten Microsoft RMS FQDN. I vårt eksempel være tjenesten Microsoft RMS FQDN følgende verdi:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Slette følgende mappe og alle filer den inneholder: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Start Office-programmer og forekomster av File Explorer på nytt.

### <a name="BKMK_Office2010ForceUpdate"></a>Office 2010: Slik tvinger du en oppdatering for et endret egendefinert mal
Du kan angi en verdi ved å redigere registret på datamaskinene som kjører Office 2010, slik at endrede maler er oppdatert på datamaskiner uten å vente for brukere å logge av og på igjen. Du kan også tvinge en umiddelbar oppdatering ved å slette de eksisterende data i en registerverdi.

> [!WARNING]
> Hvis du bruker Registerredigering på feil måte, kan du forårsake alvorlige problemer som krever at du installerer operativsystemet på nytt. Microsoft kan ikke garantere at du kan løse problemer som er forårsaket av feil bruk av Registerredigering. Bruk Registerredigering på egen risiko.

##### Slik endrer du oppdateringsfrekvensen

1.  Ved hjelp av Registerredigering, opprette en ny registerverdi kalt **UpdateFrequency** og definere en heltallsverdi for data, som angir frekvensen i dager for å laste ned eventuelle endringer til nedlastede malen. Bruk tabellen nedenfor til å finne registerbane for å opprette denne nye registerverdien.

    |Registerbane|Type|Verdi|
    |----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_DWORD|UpdateFrequency|

2.  Hvis du vil tvinge en umiddelbar oppdatering av malene, kan du gå til neste prosedyre. Hvis ikke, Start Office-programmene nå.

##### Hvis du vil tvinge en umiddelbar oppdatering

1.  Bruk av Registerredigering, slette data for det **LastUpdatedTime** verdi. Dataene kan for eksempel vise **2015-04-20T15:52**; slette 2015-04-20T15:52 slik at ingen data vises. Bruk tabellen nedenfor til å finne registerbane Hvis du vil slette denne verdien registerdata.

    |Registerbane|Type|Verdi|
    |----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_SZ|lastUpdatedTime|

2.  Slette følgende mappe og alle filer den inneholder: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Start Office-programmene.

## <a name="BKMK_PowerShellTemplates"></a>Windows PowerShell-referanse
Alt du kan gjøre i Azure Management Portal til å opprette og behandle maler, kan du gjøre fra kommandolinjen ved hjelp av Windows PowerShell. I tillegg kan du eksportere og importere maler, slik at du kan kopiere malene mellom leiere eller utføre bulk redigeringer av komplekse egenskaper i maler, for eksempel flerspråklige navn og beskrivelser.

Du kan også bruke eksport og import for å sikkerhetskopiere og gjenopprette de egendefinerte malene som beste praksis, jevnlig sikkerhetskopiere egendefinerte maler, slik at hvis du gjør en endring som ikke er beregnet, kan du enkelt gå tilbake til en tidligere versjon.

> [!IMPORTANT]
> Hvis du vil bruke Windows PowerShell til å opprette og administrere Azure RMS policymaler for rettigheter, må du ha minst versjon 2.0.0.0 av den [Windows PowerShell-modul for Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Hvis du tidligere har installert denne Windows PowerShell-modulen, kjører du følgende kommando i en PowerShell-vinduet for å kontrollere versjonsnummeret: `(Get-Module aadrm -ListAvailable).Version`

For å lese installasjonsinstrukser, kan du se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Cmdlets som støtter å opprette og administrere maler:

-   [Legge til AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Eksport av AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Importer AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [Nye AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Fjern AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Sett AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)

## Neste trinn
Når du har konfigurert egendefinerte maler for Azure Rights Management, bruker du [Veikart for Azure Rights Management-distribusjon](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til å kontrollere om det finnes andre konfigurasjonstrinn som du vil gjøre før du ruller [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for brukere og administratorer. Hvis det ikke er noen andre konfigurasjonstrinn du trenger å gjøre, se [Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) for operative veiledning til å støtte en vellykket distribusjon for organisasjonen.

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

