---
description: na
keywords: na
title: RMS Protection with Windows Server File Classification Infrastructure (FCI)
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
---
# RMS-beskyttelse med Windows Server-filen klassifisering infrastruktur (FCI)
Bruk denne artikkelen for instruksjoner og et skript til å bruke RMS (Rights Management)-klienten med beskyttelse av RMS-verktøyet til å konfigurere File Server Resource Manager og filen klassifisering infrastruktur (FCI).

Denne løsningen kan du beskytte automatisk alle filer i en mappe på en filserver som kjører Windows Server, eller beskytte automatisk filer som oppfyller bestemte kriterier. Hvis du for eksempel filer som er klassifisert som konfidensiell eller sensitiv informasjon. Denne løsningen bruker [Azure Rights Management](../Topic/Azure_Rights_Management.md) (Azure RMS) til å beskytte filer, så du må ha denne teknologien som er distribuert i organisasjonen.

> [!NOTE]
> Selv om Azure RMS inkluderer en [Kontakt](https://technet.microsoft.com/library/dn375964.aspx) som støtter arkiverer klassifisering infrastruktur, at løsningen støtter bare innebygd beskyttelse, for eksempel Office-filer.
> 
> Du må bruke Windows PowerShell for å støtte alle filtyper med filen klassifisering infrastruktur, **RMS beskyttelse** -modulen, som beskrevet i denne artikkelen. Beskyttelse av RMS-cmdlets som RMS deling program, støtte for generell beskyttelse, i tillegg til innebygd beskyttelse, noe som betyr at alle filer kan være beskyttet. Hvis du vil ha mer informasjon om disse ulike beskyttelsesnivåene, se den [Beskyttelsesnivåer – opprinnelig og generisk](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection) delen i den [Rights Management deling program administratorhåndboken](../Topic/Rights_Management_sharing_application_administrator_guide.md).

Instruksjonene nedenfor gjelder for Windows Server 2012 R2 eller Windows Server 2012. Hvis du kjører andre støttede versjoner av Windows, må du kanskje tilpasse noen av trinnene for forskjeller mellom operativsystemversjon og det som er dokumentert i denne artikkelen.

## Forutsetninger for Azure RMS-beskyttelse med Windows Server FCI
Forutsetninger for disse instruksjonene:

-   På hver filserver der du vil kjøre filen Resource Manager med filen klassifisering infrastruktur:

    -   Du har installert File Server Resource Manager som en av rolletjenester for File Services-rollen.

    -   Du har angitt en lokal mappe som inneholder filene for å beskytte med Rights Management. For eksempel C:\FileShare.

    -   Du har installert verktøyet RMS-beskyttelse, inkludert forutsetninger for verktøyet (for eksempel RMS-klienten) og Azure RMS (for eksempel hovedstolen tjenestekontoen). Hvis du vil ha mer informasjon, se [RMS beskyttelse Cmdlets](https://msdn.microsoft.com/library/azure/mt433195.aspx).

    -   Hvis du vil endre det standard beskyttelsesnivået RMS (opprinnelig eller generisk) for bestemte filtyper, du har redigert registret slik det er beskrevet i den [fil-API-konfigurasjon](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx) siden.

    -   Du har en Internett-tilkobling med innstillinger som er konfigurert for en proxy-server hvis nødvendig. For eksempel: `netsh winhttp import proxy source=ie`

-   Du har konfigurert flere forutsetninger for distribusjonen av Azure Rights Management, som beskrevet i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx). Spesielt, har følgende verdier til å koble til Azure RMS ved hjelp av en service principal:

    -   BposTenantId

    -   AppPrincipalId

    -   Symmetrisk nøkkel

-   Du har synkronisert din lokale Active Directory-brukerkontoer med Azure Active Directory eller Office 365, inkludert e-postadressen. Dette er nødvendig for alle brukere som skal ha tilgang til filene etter at de er beskyttet av FCI og Azure RMS. Hvis du ikke gjør dette trinnet (for eksempel i et testmiljø), kan brukere være blokkert fra å få tilgang til disse filene. Hvis du vil ha mer informasjon om denne konfigurasjonen til tjenestekontoen, se [Forbereder Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).

-   Du har identifisert Rights Management malen som skal brukes, som beskytter filene. Kontroller at du kjenner IDen for denne malen ved hjelp av den [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) cmdleten.

## Instruksjonene for å konfigurere File Server Resource Manager FCI Azure RMS-beskyttelse
Følg disse instruksjonene for å beskytte automatisk alle filer i en mappe ved hjelp av et Windows PowerShell-skript som en egendefinert aktivitet. Gjør disse fremgangsmåtene i denne rekkefølgen:

1.  Lagre Windows PowerShell-skriptet

2.  Opprette en klassifisering-egenskap for RMS (Rights Management)

3.  Opprette en regel for klassifisering (Classify for RMS)

4.  Konfigurere planleggingen klassifisering

5.  Opprette en oppgave for egendefinert fil (Beskytt filer med RMS)

6.  Teste konfigurasjonen ved å manuelt kjøre regelen og aktivitet

På slutten av disse instruksjonene, alle filene i den valgte mappen skal klassifiseres med den egendefinerte egenskapen for RMS, og disse filene vil deretter bli beskyttet av IRM. Du kan deretter opprette eller bruke en annen klassifisering egenskap og en regel med en oppgave i filen som beskytter bare de filene for en mer avansert konfigurasjon som beskytter selektivt noen filer og andre ikke.

#### Lagre Windows PowerShell-skriptet

1.  Utvid den [Windows PowerShell-skript Azure RMS beskyttelse ved hjelp av File Server Resource Manager FCI](#BKMK_RMSProtection_Script) delen i denne artikkelen, og kopiere innholdet. Limer inn innholdet i skriptet, og gi filen navnet **RMS-Protect-FCI.ps1** på din egen datamaskin.

2.  Se gjennom skriptet og gjøre følgende endringer:

    -   Søk etter følgende streng og erstatte den med din egen AppPrincipalId som brukes med den [Sett RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet til å koble til Azure RMS:

        ```
        <enter your AppPrincipalId here>
        ```
        Skriptet kan for eksempel se slik ut:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)] [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Søk etter følgende streng og erstatte den med din egen symmetriske nøkkelen som brukes med den [Sett RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet til å koble til Azure RMS:

        ```
        <enter your key here>
        ```
        Skriptet kan for eksempel se slik ut:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Søk etter følgende streng og erstatte den med din egen BposTenantId (leier ID) som brukes med den [Sett RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet til å koble til Azure RMS:

        ```
        <enter your BposTenantId here>
        ```
        Skriptet kan for eksempel se slik ut:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   Hvis serveren kjører Windows Server 2012, må du kanskje laste inn modulen RMSProtection i begynnelsen av skriptet manuelt. Legg til følgende kommando (eller tilsvarende i mappen "Programfiler" er på en annen stasjon enn på C:-stasjonen:

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  Signere skriptet. Hvis du ikke logger skriptet (sikrere), må du konfigurere Windows PowerShell på servere som kjører den. For eksempel kjører et Windows PowerShell-økten med den **Kjør som Administrator** alternativet, og skriver inn: **Set-ExecutionPolicy Unrestricted**. Denne konfigurasjonen kan imidlertid alle usignerte skript kjøre (mindre sikkert).

    Hvis du vil ha mer informasjon om signering av Windows PowerShell-skript, se [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) i PowerShell dokumentasjonsbibliotek.

4.  Lagre filen lokalt på hver server som filen som skal kjøre filen Resource Manager med filen klassifisering infrastruktur. Lagre for eksempel filen i **C:\RMS-Protection**. Sikker denne filen ved hjelp av NTFS-tillatelser, slik at uautoriserte brukere ikke kan endre den.

Du er nå klar til å begynne å konfigurere File Server Resource Manager.

#### Opprette en klassifisering-egenskap for RMS (Rights Management)

-   I File Server Resource Manager, klassifisering Management, opprette en ny lokal egenskap:

    -   **Name**: Type **RMS**

    -   **Beskrivelse**:   Type **Rights Management protection**

    -   **Egenskapstypen**: Velg **Ja/Nei**

    -   **Value**: Velg **Ja**

Vi kan nå opprette en regel for klassifisering som bruker denne egenskapen.

#### Opprette en regel for klassifisering (Classify for RMS)

-   Opprett en ny regel for klassifisering:

    -   På den **Generelt** i kategorien:

        -   **Name**: Type **Classify for RMS**

        -   **Aktivert**: Holde standarden, som er at det er merket av for dette alternativet.

        -   **Beskrivelse**: Type **Classify all files in the &lt;folder name&gt; folder for Rights Management**.

            Erstatte *&lt; mappenavn &gt;* med det valgte mappenavnet. For eksempel **klassifisere alle filene i mappen C:\FileShare for rettighetsadministrasjon**

        -   **Scope**: Legg til den valgte mappen. For eksempel **C:\FileShare**.

            Ikke Merk av for.

    -   På den **klassifisering** i kategorien:

    -   **Klassifiseringsmåte**: Velg **mappen klassifiserer**

    -   **Egenskapen** navn: Velg **RMS**

    -   Egenskapen **verdien**: Velg **Ja**

Selv om du kan kjøre manuelt, klassifisering reglene for pågående operasjoner, vil denne regelen skal kjøres på en plan, slik at nye filer blir klassifisert med RMS-egenskapen.

#### Konfigurere planleggingen klassifisering

-   På den **automatiske klassifiseringen** i kategorien:

    -   **Aktivere fast tidsplan**: Merk av for.

    -   Konfigurere tidsplanen for alle klassifisering regler du vil kjøre, som inkluderer våre nye regelen til å klassifisere filer med RMS-egenskapen.

    -   **Tillat kontinuerlig klassifisering for nye filer**: Merk av for slik at nye filer skal klassifiseres.

    -   Valgfritt: Gjør eventuelle endringer du ønsker, for eksempel hvordan du konfigurerer alternativer for rapporter og varsler.

Nå du har fullført konfigurasjonen klassifisering, er du klar til å konfigurere en oppgave for å bruke RMS-beskyttelse på filene.

#### Opprette en oppgave for egendefinert fil (Beskytt filer med RMS)

-   I **oppgavene for filen**, opprette en ny oppgave i filen:

    -   På den **Generelt** i kategorien:

        -   **Aktivitetsnavn**: Type **Protect files with RMS**

        -   Behold den **aktiverer** avmerkingsboks valgt.

        -   **Beskrivelse**: Type **Protect files in &lt;folder name&gt; with Rights Management and a template by using a Windows PowerShell script.**

            Erstatte *&lt; mappenavn &gt;* med det valgte mappenavnet. For eksempel **beskytter filene i C:\FileShare med Rights Management og en mal ved hjelp av et Windows PowerShell-skriptet**

        -   **Scope**: Velg den valgte mappen. For eksempel **C:\FileShare**.

            Ikke Merk av for.

    -   På den **handlingen** i kategorien:

        -   **Type**: Velg **egendefinert**

        -   **Kjørbar fil**: Angi følgende:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Hvis Windows ikke er på stasjon C:, endre denne banen, eller Bla gjennom til denne filen.

        -   **Argumentet**: Angi følgende ved å angi dine egne verdier for &lt; bane &gt; og &lt; ID for malen &gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Hvis du kopierte skriptet til C:\RMS-Protection og mal-IDen du har identifisert fra forutsetningene er e6ee2481-26b9-45e5-b34a-f744eacd53b0, kan du for eksempel angi følgende:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            I denne kommandoen er **[kildebane]** og **[kilde fil eier e-post]** er begge FCI-spesifikke variabler skriver disse så nøyaktig som de vises i kommandoen ovenfor. Den første som brukes av FCI for å angi den identifiserte filen i mappen automatisk, og andre er for FCI til automatisk å hente e-postadressen for navngitte eieren av den identifiserte filen. Denne kommandoen gjentas for hver fil i mappen, som i vårt eksempel er hver fil i mappen C:\FileShare, som i tillegg har RMS som en filegenskap klassifisering.

            > [!NOTE]
            > Det **-OwnerMail [Source File Owner Email]** parameter og verdi, sikrer du at den opprinnelige eieren av filen er gitt Rights Management-eieren av filen etter at den er beskyttet. Dette sikrer at den opprinnelige eieren av filen har alle Rights Management-rettigheter til sine egne filer. Når filene er opprettet av en domenebruker, hentes e-postadressen automatisk fra Active Directory ved hjelp av brukerkontonavnet i filens eier-egenskapen. Filserveren må være i det samme domenet eller klarerte domenet som brukeren for å gjøre dette.
            > 
            > Når det er mulig, kan du tilordne de opprinnelige eierne til beskyttede dokumenter, for å sikre at disse brukerne fortsette å ha full kontroll over filene som de opprettet. Hvis du bruker variabelen [kilde fil eier e-post] som ovenfor og en fil ikke har imidlertid en domenebruker definert som eier (for eksempel en lokal konto ble brukt til å opprette filen, slik at eieren viser systemet,) skriptet mislykkes.
            > 
            > For filer som ikke har en domenebruker som eieren, kan du kopiere og lagre disse filene selv som en domenebruker, slik at blir du eier for bare disse filene. Eller, hvis du har tillatelser, kan du manuelt endre eieren.  Eller du kan også angi en bestemt e-postadresse (for eksempel ditt eget eller en gruppeadresse for IT-avdelingen) i stedet for [kilde fil eier e-post]-variabel, noe som betyr at alle filene du beskytte ved hjelp av dette skriptet bruker denne e-postadressen til å definere den nye eieren.

    -   **Kjører kommandoen som**: Velg **lokalt System**

    -   På den **betingelse** i kategorien:

        -   **Egenskapen**: Velg **RMS**

        -   **Operatør**: Velg **like**

        -   **Value**: Velg **Ja**

    -   På den **tidsplan** i kategorien:

        -   **Run at**: Konfigurere foretrukne planen.

            Gi god tid for at skriptet skal fullføre. Selv om denne løsningen beskytter alle filene i mappen, kjøres skriptet én gang for hver fil hver gang. Selv om det tar lenger tid enn å beskytte alle filene på samme tid, som har støtte for beskyttelse av RMS-verktøyet, er denne fil av konfigurasjonen for FCI kraftigere. Beskyttede filer kan for eksempel ha forskjellige eiere (beholde den opprinnelige eieren) når du bruker variabelen [kilde fil eier e-post], og denne handlingen ved fil vil være nødvendig hvis du senere endrer konfigurasjonen for å selektivt beskytte filer i stedet for alle filene i en mappe.

        -   **Kjører hele tiden på nye filer**: Merk av for.

#### Teste konfigurasjonen ved å manuelt kjøre regelen og aktivitet

1.  Kjør regelen klassifisering:

    1.  Klikk **klassifisering regler** &gt; **kjører klassifiseringen med alle regler nå**

    2.  Klikk **venter klassifisering for å fullføre**, og klikk deretter **OK**.

2.  Vent til den **kjører klassifisering** Hvis du vil lukke, og deretter vise resultatene i rapporten vises automatisk. Vil du se **1** for den **Egenskaper** -feltet og antall filer i mappen. Bekreft ved å bruke File Explorer og kontrollere egenskapene til filer i den valgte mappen. På den **klassifisering** tab, bør du se **RMS** som navnet på en egenskap og **Ja** for sin **verdien**.

3.  Kjør filen management-oppgaven:

    1.  Klikk **oppgavene for filen** &gt; **beskytte filene med RMS** &gt; **kjører filen Management aktivitet nå**

    2.  Klikk **venter aktiviteten for å fullføre**, og klikk deretter **OK**.

4.  Vent til den **oppgave kjører filen** Hvis du vil lukke, og deretter vise resultatene i rapporten vises automatisk. Du skal se hvor mange filer som finnes i den valgte mappen i den **filer** feltet. Bekreft at filene i den valgte mappen blir nå beskyttet av RMS. For eksempel hvis den valgte mappen er C:\FileShare, skriver du inn følgende i et Windows PowerShell-økten, og Bekreft at noen filer har statusen **UnProtected**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Feilsøkingstips:
    > 
    > -   Hvis du ser **0** i rapporten, i stedet for antall filer i mappen, angir dette skriptet ikke ble kjørt. Først, sjekke selve skriptet ved å laste den inn i Windows PowerShell ISE til å validere skriptinnholdet, og prøv å kjøre den for å se om eventuelle feil, vises. Uten argumenter er angitt, vil skriptet prøver å koble til og godkjenne på RMS Azure.
    > 
    >     -   Hvis skriptet rapporterer at den ikke kan koble til Azure RMS, må du kontrollere verdiene som vises for service principal kontoen, som er angitt i skriptet.  Hvis du vil ha mer informasjon om hvordan du oppretter denne service principal-kontoen, kan du se andre forutsetningen i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)
    >     -   Hvis skriptet rapporterer at det ikke kunne koble til Azure RMS og Azure regionen er utenfor Nord-Amerika, må du kontrollere at du har redigert registret på riktig måte for denne konfigurasjonen. Det er en god test av dette å kjøre Get-RMSTemplate direkte fra Windows PowerShell på serveren. Hvis du vil ha mer informasjon om redigering av registret, kan du se tredje forutsetningen i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx).
    > -   Hvis skriptet alene kjører i Windows PowerShell ISE uten feil, kan du prøve å kjøre den som følger fra en PowerShell-økt, angir et filnavn til å beskytte og uten parameteren - OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File <full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Hvis skriptet kjøres i denne Windows PowerShell-økten, må du kontrollere oppføringene for **Executive** og **argumentet** i filen management oppgavehandling.  Hvis du har angitt **- OwnerEmail [kilde fil eier e-post]**, prøve å fjerne denne parameteren.
    > 
    >         Hvis filen management oppgaven fungerer riktig uten  **- OwnerEmail [kilde fil eier e-post]**, kontroller at ubeskyttede filer har en domenebruker oppført som eieren av filen stedet **SYSTEM**.  Hvis du vil gjøre dette, kan du bruke den **Sikkerhet** for egenskapene for filen, og velg deretter **Avansert**. Den **eier** verdien vises umiddelbart etter filen **navn**. Kontroller også at filserveren er i samme domene eller et klarert domene til å slå opp brukerens e-postadresse fra Active Directory Domain Services.
    > -   Hvis du vil se riktig antall filer i rapporten, men filene er ikke beskyttet, kan du prøve å beskytte filene manuelt ved hjelp av den [Beskytt RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) cmdleten for å se om eventuelle feil, vises.

Når du har bekreftet at disse oppgavene kan kjøres, kan du lukke filen Resource Manager. Nye filer blir automatisk beskyttet, og alle filer som beskyttes på nytt når du planlegger kjører. Beskytte filer på nytt, sikrer du at eventuelle endringer i malen gjelder for filene.

### <a name="BKMK_RMSProtection_Script"></a>Windows PowerShell-skript Azure RMS beskyttelse ved hjelp av File Server Resource Manager FCI
Denne delen inneholder eksempelskript for å kopiere og redigere, som beskrevet i den foregående inndelingen.

*&#42;&#42;Ansvarsfraskrivelse&#42;&#42;: Dette eksempelskriptet støttes ikke under et standard kundestøtte for Microsoft-program eller en tjeneste. Dette eksempelskriptet leveres som den er uten garanti av noe slag.*

```
<# .SYNOPSIS Helper script to protect all file types with Azure RMS and FCI. .DESCRIPTION Protect files with Azure RMS and Windows Server FCI, using an RMS template ID. #> param( [Parameter(Mandatory = $false)] [ValidateScript({ If($_ -eq "") {$true} else { if (Test-Path -Path $_ -PathType Leaf) {$true} else {throw "Can't find file specified"} } })] [string]$File, [Parameter(Mandatory = $false)] [string]$TemplateID, [Parameter(Mandatory = $false)] [string]$OwnerMail, [Parameter(Mandatory = $false)] [string]$AppPrincipalId = "<enter your AppPrincipalId here>", [Parameter(Mandatory = $false)] [string]$SymmetricKey = "<enter your key here>", [Parameter(Mandatory = $false)] [string]$BposTenantId = "<enter your BposTenantId here>" ) # script information [String] $Script:Version = 'version 1.0' [String] $Script:Name = "RMS-Protect-FCI.ps1" #global working variables [switch] $Script:isScriptProcess = $False # Controls the script process. If false, the script gracefully stops running. #**Functions (general helper)*************************************** function Get-ScriptName(){ return $MyInvocation.ScriptName.Substring($MyInvocation.ScriptName.LastIndexOf('\') + 1, $MyInvocation.ScriptName.LastIndexOf('.') - $MyInvocation.ScriptName.LastIndexOf('\') - 1) } #**Functions (script specific)************************************** function Check-Module{ param ([String]$Module = $(Throw "Module name not specified")) [bool]$isResult = $False #try to load the module if (get-module -list -name $Module) { import-module $Module if (get-module -name $Module ) { $isResult = $True } else { $isResult = $False } } else { $isResult = $False } return $isResult } function Protect-File ($ffile, $ftemplateId, $fownermail) { [bool] $returnValue = $false try { If ($OwnerMail -eq $null -or $OwnerMail -eq "") { $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId $returnValue = $true Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId") } else { $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId -OwnerEmail $fownermail $returnValue = $true Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId, set Owner: $fownermail") } } catch { Write-Host ( "ERROR" + "During protection of file: $ffile with Template: $ftemplateId") } return $returnValue } function Set-RMSConnection ($fappId, $fkey, $fbposId) { [bool] $returnValue = $false try { Set-RMSServerAuthentication -AppPrincipalId $fappId -Key $fkey -BposTenantId $fbposId Write-Host ("Information: " + "Connected to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId") $returnValue = $true } catch { Write-Host ("ERROR" + "During connection to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId") } return $returnValue } #**Main Script (Script)********************************************* Write-Host ("-== " + $Script:Name + " " + $Version + " ==-") $Script:isScriptProcess = $True # Validate Azure RMS connection by checking the module and then connection if ($Script:isScriptProcess) { if (Check-Module -Module RMSProtection){ $Script:isScriptProcess = $True } else { Write-Host ("The RMSProtection module is not loaded") -foregroundcolor "yellow" -backgroundcolor "black" $Script:isScriptProcess = $False } } if ($Script:isScriptProcess) { #Write-Host ("Try to connect to Azure RMS with AppId: $AppPrincipalId and BPOSID: $BposTenantId" ) if (Set-RMSConnection $AppPrincipalId $SymmetricKey $BposTenantId) { Write-Host ("Connected to Azure RMS") } else { Write-Host ("Couldn't connect to Azure RMS") -foregroundcolor "yellow" -backgroundcolor "black" $Script:isScriptProcess = $False } } #  Start working loop if ($Script:isScriptProcess) { if ( !(($File -eq $null) -or ($File -eq "")) ) { if (!(Protect-File -ffile $File -ftemplateId $TemplateID -fownermail $OwnerMail)) { $Script:isScriptProcess = $False } } } # Closing if (!$Script:isScriptProcess) { Write-Host "ERROR occurred during script process" -foregroundcolor "red" -backgroundcolor "black"} write-host ("-== " + $Script:Name + " " + $Version + "  ==-") if (!$Script:isScriptProcess) { exit(-1) } else {exit(0)}
```

## Endre instruksjonene for å selektivt beskytte filer
Når du har instruksjonene for foregående jobber, er det deretter veldig enkelt å endre dem for en mer avansert konfigurasjon. Hvis du for eksempel beskytte filer ved hjelp av det samme skriptet, men bare etter filer som inneholder personlige opplysninger, og kanskje velge en mal som er mer restriktiv rettigheter.

Hvis du vil gjøre dette, bruker du en av egenskapene for innebygde klassifisering (for eksempel **personlig identifiserbar informasjon**) eller opprette en ny egenskap. Deretter kan du opprette en ny regel som bruker denne egenskapen. Du kan for eksempel velge den **innhold klassifiserer**, velger du **personlig identifiserbar informasjon** egenskap med en verdi på **Høy**, og konfigurere mønster streng eller et uttrykk som identifiserer filen som skal konfigureres for denne egenskapen (for eksempel strengen "**Fødselsdato**").

Nå alt du trenger å gjøre er å opprette en ny fil oppgave som bruker den samme skript men muligens med en annen mal, og Konfigurer betingelsen for egenskapen klassifisering som du nettopp har konfigurert. For eksempel i stedet for betingelsen som vi tidligere har konfigurert (**RMS** -egenskapen, **like**, **Ja**), velger den **personlig identifiserbar informasjon** egenskapen med den **Operator** satt til **lik** og **verdien** av **Høy**.

