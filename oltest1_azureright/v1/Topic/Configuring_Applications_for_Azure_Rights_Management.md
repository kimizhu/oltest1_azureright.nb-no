---
description: na
keywords: na
title: Configuring Applications for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
---
# Konfigurere programmer for Azure Rights Management
> [!NOTE]
> Denne informasjonen er for IT-administratorer og konsulenter som har distribuert Azure Rights Management. Hvis du søker etter bruker-Hjelp og informasjon om hvordan du bruker Rights Management for et bestemt program eller hvordan du åpner en fil som er beskyttet av rettigheter, kan du bruke Hjelp og veiledning som følger med programmet.
> 
> For eksempel for Office-programmer, klikker du hjelp-ikonet, og Skriv inn søkeord som **Rights Management** eller **IRM**. Hvis RMS deling av programmer for Windows, kan du se den [Rights Management deling Brukerhåndbok for programmet](http://technet.microsoft.com/library/dn339006.aspx).

Etter at du har distribuert Azure Rights Management (Azure RMS) for din organisasjon, kan du bruke følgende informasjon til å konfigurere programmer og tjenester for å støtte RMS Azure. Disse inkluderer Office-programmer som Word 2013 og Word 2010, og tjenester som Exchange Online (Transportregler, forebygging av tap av data, ikke Videresend og meldingskryptering) og SharePoint Online (beskyttet biblioteker). Hvis du vil ha informasjon om hvordan disse programmene og tjenestene støtter rettighetsbehandling, se [Hvordan programmer støtter Azure rettighetsbehandling](../Topic/How_Applications_Support_Azure_Rights_Management.md).

> [!IMPORTANT]
> Informasjon om støttede versjoner og andre behov, kan du se [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

-   [Office 365: Konfigurasjon for klienter og elektroniske tjenester](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365)

    -   [Exchange Online: IRM-konfigurasjonen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline)

    -   [SharePoint Online- og OneDrive for bedrifter: IRM-konfigurasjonen](#BKMK_SharePointOnline)

-   [2016 for Office og Office-2013: Konfigurasjon for klienter](#BKMK_Office2013Configuration)

-   [Office 2010: Konfigurasjon for klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_Office2010Configuration)

-   [Rights Management program for deling: Installasjon og konfigurasjon for klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp)

    -   [RMS deling av programmer for Windows: Installasjon og konfigurasjon](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingAppforWindows)

    -   [RMS deling program for mobile plattformer: Installasjon](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingAppMovileDevices)

-   [Andre programmer som støtter RMS-APIs: Installasjon og konfigurasjon](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_RMSAPIs)

Hvis du vil konfigurere lokale servere, for eksempel Exchange Server og SharePoint Server, kan du se [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

> [!TIP]
> Eksempler på høyt nivå og skjermbilder av programmer som er konfigurert til å bruke Azure RMS, se den [Azure RMS i aksjon: Administratorer og brukere ser](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures) delen fra den [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emnet.

## <a name="BKMK_O365"></a>Office 365: Konfigurasjon for klienter og elektroniske tjenester
Fordi Office 365 støtter Azure RMS, kreves ingen konfigurasjon av klientdatamaskin støtte for information rights management (IRM)-funksjoner for programmer, for eksempel Word, Excel, PowerPoint, Outlook og Outlook Web App. Alle brukere som har å gjøre er å logge deg på sine Office-programmer med sine [!INCLUDE[o365_1](../Token/o365_1_md.md)] legitimasjon, og de kan beskytte filer og e-post og bruker filer og e-postmeldinger som er beskyttet av andre.

Vi anbefaler imidlertid at du supplere disse programmene med Rights Management deler programmet, slik at brukere kan få fordelen av Office-tillegg. Hvis du vil ha mer informasjon, se den [Rights Management program for deling: Installasjon og konfigurasjon for klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) delen i dette emnet.

### <a name="BKMK_ExchangeOnline"></a>Exchange Online: IRM-konfigurasjonen
Hvis du vil konfigurere Exchange Online for å støtte RMS Azure, må du konfigurere rights management (IRM) tjenesten for Exchange Online. Hvis du vil gjøre dette, kan du bruke Windows PowerShell (uten å måtte installere en separat modul), og kjøre [PowerShell kommandoer for Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Du kan ikke nå konfigurere Exchange Online for å støtte RMS Azure Hvis du bruker en kunde-administrerte leier nøkkel (BYOK) for Azure RMS, i stedet for standardkonfigurasjonen av en Microsoft-administrerte leier nøkkel. Hvis du vil ha mer informasjon, se den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) delen i den [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emnet.
> 
> Hvis du prøver å konfigurere Exchange Online når Azure RMS bruker BYOK, kommandoen til å importere nøkkelen (trinn 5 i fremgangsmåten nedenfor) mislykkes med feilmeldingen **[FailureCategory = Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Disse trinnene gir et vanlig sett med kommandoer som kjøres for å aktivere Exchange Online å bruke RMS Azure:

1.  Hvis dette er første gang at du har brukt Windows PowerShell for Exchange Online på datamaskinen, må du konfigurere Windows PowerShell for å kjøre signerte skript. Starte Windows PowerShell-økt ved hjelp av **Kjør som administrator** alternativet, og skriv deretter inn:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  I Windows PowerShell-økten og logge deg på Exchange Online ved hjelp av en konto som er aktivert for remote Shell-tilgang. Alle kontoer som er opprettet i Exchange Online er aktivert som standard for remote Shell-tilgang, men dette kan være deaktivert (og aktivert) ved hjelp av den   [Sett bruker &lt; UserIdentity &gt; - RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx) kommandoen.

    Hvis du vil logge på, skriver du inn:

    ```
    $Cred = Get-Credential
    ```
    I den **Be om legitimasjon for Windows PowerShell** dialogboks-boksen, angir Office 365-brukernavn og passord.

3.  Koble til Exchange Online-tjenesten ved å kjøre følgende to kommandoer:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Angi plasseringen til nøkkelen Azure RMS leier i henhold til ditt område:

    I Nord-Amerika (og myndigheter abonnementer):

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    For Europa:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    For Asia:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    For Sør-Amerika:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importer konfigurasjonsdata fra Azure RMS til Exchange Online, i form av det klarerte publisering domenet (TPD). Dette inkluderer Azure RMS leier nøkkel og Azure RMS-maler:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    I denne kommandoen, brukte vi navnet på **RMS Online** for Basisnavnet for TPD for Azure RMS i Exchange Online. Når TPD importeres, er det kalt **RMS Online - 1** i Exchange Online.

6.  Aktiver Azure RMS-funksjonalitet slik at IRM-funksjonene er tilgjengelige for Exchange Online:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Når du har kjørt denne kommandoen, aktiveres automatisk Rights Management for Outlook-klient, Outlook Web app og Exchange Active Sync.

7.  Du kan også teste at denne konfigurasjonen er vellykket, ved å bruke følgende kommando:

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    For eksempel: **Test-IRMConfiguration -Sender  adams@contoso.com**

    Denne kommandoen kjører en rekke kontroller som inkluderer bekrefter tilkobling til tjenesten, henter konfigurasjonen, henting av URIer, lisenser og maler. I Windows PowerShell-økten vil du se resultatene av hver, og på slutten, hvis alt går gjennom disse kontrollene: **SAMLEDE RESULTATET: PASS**

8.  Koble den eksterne PowerShell-økten:

    ```
    Remove-PSSession $Session
    ```

Brukere kan nå beskytte sine e-postmeldinger ved hjelp av Azure RMS. I Outlook Web App, kan du for eksempel velger **Angi tillatelser** den utvidede menyen (**...**), og velg deretter **ikke Videresend** eller ett av de tilgjengelige malene til å bruke informasjonsbeskyttelse i e-postmeldingen og vedlegg. Men fordi Outlook Web App bufrer Brukergrensesnittet for en dag, vente på denne tidsperioden, skal være inaktiv før du prøver å bruke informasjonsbeskyttelse av til e-postmeldinger, og når du har kjørt disse kommandoene for konfigurasjon. Før Brukergrensesnittet oppdateres for å gjenspeile den nye konfigurasjonen, vil du ikke ser noen alternativer fra den **Angi tillatelser** menyen.

> [!IMPORTANT]
> Hvis du oppretter nye [egendefinerte maler](https://technet.microsoft.com/library/dn642472.aspx) for Azure RMS eller oppdatere maler, hver gang, må du kjøre følgende kommando i Exchange Online PowerShell (Hvis nødvendig, kjøre trinn 2 og 3 første) til å synkronisere disse endringene til Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Som en Exchange-administrator, kan du nå konfigurere funksjoner som gjelder informasjonsbeskyttelse av automatisk, som [transport regler](https://technet.microsoft.com/library/dd302432.aspx), [datapolicyer tap forebygging (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx), og [beskyttede talemeldinger](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (Unified Messaging).

For detaljerte instruksjoner for å konfigurere Exchange Online for å aktivere IRM-funksjonalitet, kan du se dokumentasjonen i Exchange-biblioteket. For eksempel:

-   [Koble til Exchange Online ved hjelp av ekstern PowerShell](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Konfigurere IRM for å bruke Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

#### Office 365 meldingskryptering
Kjøre de samme trinnene som er dokumentert i den forrige delen, men hvis du ikke vil at malene skal vises før trinn 6, kjører du følgende kommando for å hindre at IRM-maler er tilgjengelige i Outlook Web App og Outlook-klienten: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Så, er du klar til å konfigurere [transport regler](https://technet.microsoft.com/library/dd302432.aspx) til å endre sikkerheten melding automatisk når mottakere er plassert utenfor organisasjonen, og velg den **bruke Office 365 meldingskryptering** alternativet.

Hvis du vil ha mer informasjon om meldingskryptering, se [kryptering i Office 365](https://technet.microsoft.com/library/dn569286.aspx) i Exchange-biblioteket.

### <a name="BKMK_SharePointOnline"></a>SharePoint Online- og OneDrive for bedrifter: IRM-konfigurasjonen
Hvis du vil konfigurere SharePoint Online og OneDrive for bedrifter for å støtte RMS Azure, må du først aktivere tjenesten informasjon rights management (IRM) for SharePoint Online ved hjelp av SharePoint administrasjonssenteret. Deretter eiere kan IRM-beskytte sine SharePoint-lister og dokumentbiblioteker, og brukere kan IRM-beskytte sine OneDrive for Business biblioteket slik at dokumenter som er lagret i det, og deles med andre, er automatisk beskyttet av Azure RMS.

Hvis du vil aktivere rights management (IRM) informasjonstjenesten for SharePoint Online, kan du se følgende instruksjoner fra webområdet for Office:

-   [Sett opp informasjon Rights Management (IRM) i SharePoint administrasjonssenteret](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Denne konfigurasjonen er utført av Office 365-administrator.

#### Konfigurere IRM for biblioteker og lister
Når du har aktivert IRM-tjenesten for SharePoint, kan eiere IRM-beskytte sine SharePoint-dokumentbiblioteker og lister. For instruksjoner, se følgende fra webområdet for Office:

-   [Bruke IRM på lister eller biblioteker](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Denne konfigurasjonen er utført av SharePoint-områdeadministrator.

#### <a name="BKMK_OneDrive"></a>Konfigurere IRM for OneDrive for bedrifter
Når du har aktivert IRM-tjenesten for SharePoint Online, kan deretter brukernes OneDrive for dokumentbibliotek for Business konfigureres for IRM-beskyttelse.  Brukere kan konfigurere dette for seg selv ved hjelp av den **innstillinger** -ikonet i sine OneDrive. Selv om administratorer kan konfigurere Rights Management for brukernes OneDrive for virksomhet ved hjelp av administrasjonssenteret for SharePoint, kan du gjøre dette ved hjelp av Windows PowerShell.

> [!NOTE]
> Hvis du vil ha mer informasjon om hvordan du konfigurerer OneDrive for bedrifter, kan du se dokumentasjonen for Microsoft Office,[definerer OneDrive for bedrifter i Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

##### Konfigurasjon for brukere
Gi brukere med disse instruksjonene slik at brukerne kan konfigurere sin OneDrive for bedrifter og IRM-beskytte sine business-filer.

1.  I OneDrive, klikker du **innstillinger** ikonet for å åpne Innstillinger-menyen, og klikk deretter **innholdet på området**.

2.  Pek på den **dokumenter** side ved side, velger du ellipser (**...**), og klikk deretter **innstillinger.**

3.  På den **innstillinger** side i den **tillatelser og behandling** -delen, klikker du **Information Rights Management**.

4.  På den **Innstillinger for informasjonsbehandling rettigheter** velger **tillatelser for dette biblioteket ved nedlasting** angi ditt valg av navn og en beskrivelse for tillatelser, og du kan også klikke **Vis valg** til å konfigurere valgfrie konfigurasjoner, og klikk deretter **OK**.

    Hvis du vil ha mer informasjon om konfigurasjonsalternativene for, kan du lese instruksjonene i [bruker Information Rights Management til en liste eller et bibliotek](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) fra Office-dokumentasjonen.

Fordi denne konfigurasjonen er avhengig av brukere i stedet for en administrator å beskytte sine OneDrive for Business bibliotek IRM, opplyse brukere om fordelene med å beskytte sine filer og hvordan du gjør dette. For eksempel forklare at når de deler et dokument fra OneDrive for bedrifter, bare de godkjenne personer har tilgang til den med noen begrensninger som de konfigurerer, selv om filen har fått nytt navn, og kopieres til et annet sted.

##### Konfigurasjon for administratorer
Selv om du ikke kan konfigurere IRM for brukernes OneDrive for virksomhet ved hjelp av administrasjonssenteret for SharePoint, kan du gjøre dette ved hjelp av Windows PowerShell. Hvis du vil aktivere IRM for disse bibliotekene, gjør du følgende:

1.  Last ned og installer den [SharePoint Online-klient komponenter SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Last ned og installer den [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Kopiere innholdet i skriptet nedenfor, og gi filen navnet Sett IRMOnOneDriveForBusiness.ps1 på datamaskinen.

    *&#42;&#42;Ansvarsfraskrivelse&#42;&#42;*: Dette eksempelskriptet støttes ikke under et standard kundestøtte for Microsoft-program eller en tjeneste. Dette eksempelskriptet leveres som den er uten garanti av noe slag.

    ```
    # Requires Windows PowerShell version 3 <# Description: Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> # URL will be in the format https://<tenant-name>-admin.sharepoint.com $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.com" $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com", "https://contoso-my.sharepoint.com/personal/user2_contoso_com", "https://contoso-my.sharepoint.com/personal/user3_contoso_com") <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row). Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv" #> $listTitle = "Documents" function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Set-IrmConfiguration { [cmdletbinding()] param( [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List, [parameter(Mandatory=$true)][string]$PolicyTitle, [parameter(Mandatory=$true)][string]$PolicyDescription, [parameter(Mandatory=$false)][switch]$IrmReject, [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate, [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView, [parameter(Mandatory=$false)][switch]$AllowPrint, [parameter(Mandatory=$false)][switch]$AllowScript, [parameter(Mandatory=$false)][switch]$AllowWriteCopy, [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays, [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays, [parameter(Mandatory=$false)][string]$GroupName ) process { Write-Verbose "Applying IRM Configuration on '$($List.Title)'" # reset the value to the default settings $list.InformationRightsManagementSettings.Reset() $list.IrmEnabled = $true # IRM Policy title and description $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription # Set additional IRM library settings # Do not allow users to upload documents that do not support IRM $list.IrmReject = $IrmReject.IsPresent $parsedDate = Get-Date if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate)) { # Stop restricting access to the library at <date> $list.IrmExpire = $true $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate } # Prevent opening documents in the browser for this Document Library $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent # Configure document access rights # Allow viewers to print $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent # Allow viewers to run script and screen reader to function on downloaded documents $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent # Allow viewers to write on a copy of the downloaded document $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent if($DocumentAccessExpireDays) { # After download, document access rights will expire after these number of days (1-365) $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays } # Set group protection and credentials interval if($LicenseCacheExpireDays) { # Users must verify their credentials using this interval (days) $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays } if($GroupName) { # Allow group protection. Default group: $list.InformationRightsManagementSettings.EnableGroupProtection = $true $list.InformationRightsManagementSettings.GroupName             = $GroupName } } end { if($list) { Write-Verbose "Committing IRM configuration settings on '$($list.Title)'" $list.InformationRightsManagementSettings.Update() $list.Update() $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() } } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # connect to Office365 first, required for SharePoint Online cmdlets to run Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential # enumerate each of the specified site URLs foreach($webUrl in $webUrls) { $grantedSiteCollectionAdmin = $false try { # establish the client context and set the credentials to connect to the site $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl) $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # initialize the site and web context $script:clientContext.Load($script:clientContext.Site) $script:clientContext.Load($script:clientContext.Web) $script:clientContext.ExecuteQuery() # load and ensure the tenant admin user account if present on the target SharePoint site $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName) $script:clientContext.Load($tenantAdminUser) $script:clientContext.ExecuteQuery() # check if the tenant admin is a site admin if( -not $tenantAdminUser.IsSiteAdmin ) { try { # grant the tenant admin temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null $grantedSiteCollectionAdmin = $true } catch { Write-Error $_.Exception return } } try { # load the list orlibrary using CSOM $list = $null $list = $script:clientContext.Web.Lists.GetByTitle($listTitle) $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() # **************  ADMIN INSTRUCTIONS  ************** # If necessary, modify the following Set-IrmConfiguration parameters to match your required values # The supplied options and values are for example only # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90 Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" } catch { Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())" } } finally { if($grantedSiteCollectionAdmin) { # remove the temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null } } } Disconnect-SPOService -ErrorAction SilentlyContinue
    ```

4.  Se gjennom skriptet og gjøre følgende endringer:

    1.  Søke etter `$sharepointAdminCenterUrl` og erstatt verdien for eksempel med din egen URL-adressen for SharePoint admin center.

        Du finner denne verdien som primær URL-adresse når du går inn i administrasjonssenteret for SharePoint, og den har følgende format: https://*&lt; tenant_name &gt;*-admin.sharepoint.com

        Hvis du for eksempel leier heter "contoso", vil du angi: **https://contoso-admin.sharepoint.com**

    2.  Søke etter `$tenantAdmin` og erstatte verdien eksemplet med egne kvalifiserte globale administratorkontoen for Office 365.

        Denne verdien er den samme som du bruker til å logge på Office 365 Administrasjonsportal som global administrator og har følgende format: brukernavn ved*&lt; domenenavn leier &gt;*com

        For eksempel hvis Office 365 global administrator brukernavn er "admin" for "en contoso.com" leier domenet, kan du angi: **admin@contoso.com**

    3.  Søke etter `$webUrls` og erstatte verdiene for eksempel med brukernes OneDrive for Business web URL-adresser, legge til eller slette så mange oppføringer som du trenger.

        Du kan også se merknadene i skriptet om hvordan du erstatter denne matrisen ved å importere en. CSV-fil som inneholder alle URL-adresser må du konfigurere.  Vi har laget en annen eksempelskript for å automatisk søke etter og trekke ut URL-adresser for å fylle ut dette. CSV-fil. Når du er klar til å gjøre dette, kan du utvide den [Flere skript til å sende alle OneDrive for Business URL-adresser til en. CSV-fil](#BKMK_Script_OD4B_URLS) delen umiddelbart etter disse trinnene.

        Weben er URL-adressen for brukerens OneDrive for bedrifter i følgende format: https://*&lt; leier navn &gt;*-my.sharepoint.com/personal/*&lt; brukernavn &gt;*_*&lt; leier navn &gt;*_com

        For eksempel hvis brukeren i contoso-leier har brukernavnet "rsimone", kan du angi: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

    4.  Fordi vi bruker skriptet til å konfigurere OneDrive for bedrifter, endres ikke verdien for **Documents** for det `$listTitle` variabel.

    5.  Søke etter `ADMIN INSTRUCTIONS`. Hvis du ikke gjør endringer i denne delen, konfigureres brukerens OneDrive for bedrifter for IRM i policy-tittelen på "Beskyttede filer" og beskrivelsen av "Denne policyen begrenser tilgang til autoriserte brukere".  Ingen andre IRM-alternativer angis, som er sannsynligvis passer for de fleste miljøer. Du kan imidlertid endre foreslått tittel og beskrivelse, og også legge til eventuelle andre IRM-alternativer som passer for ditt miljø. Se eksemplet kommentert i skript for å hjelpe deg med å lage ditt eget sett med parameterne for kommandoen Set-IrmConfiguration.

5.  Lagre skriptet og logge den. Hvis du ikke logger skriptet (sikrere), må Windows PowerShell konfigureres på datamaskinen til å kjøre usignerte skript. Hvis du vil gjøre dette, kjører du en Windows PowerShell-økten med den **Kjør som Administrator** alternativet, og skriver inn: **Set-ExecutionPolicy Unrestricted**. Denne konfigurasjonen kan imidlertid alle usignerte skript kjøre (mindre sikkert).

    Hvis du vil ha mer informasjon om signering av Windows PowerShell-skript, se [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) i PowerShell dokumentasjonsbibliotek.

6.  Kjør skriptet, og hvis du blir bedt om det, må du angi passordet for kontoen for Office 365-administrator. Hvis du endrer skriptet og kjøre den i den samme Windows PowerShell-økten, vil du bli bedt om påloggingsinformasjon.

> [!TIP]
> Du kan også bruke dette skriptet til å konfigurere IRM for en SharePoint Online-biblioteket. For denne konfigurasjonen du vil aktivere alternativet for flere **ikke Tillat brukere å laste opp dokumenter som ikke støtter IRM,**, for å sikre at biblioteket inneholder bare beskyttede dokumenter.    Hvis du vil gjøre dette, legger du til det `-IrmReject` parameter for kommandoen Set-IrmConfiguration i skriptet.
> 
> Du trenger også å endre det `$webUrls` variabel (for eksempel **https://contoso.sharepoint.com**) og  `$listTitle` variabelen (for eksempel **$Reports**).

Hvis du vil deaktivere IRM for brukerens OneDrive for Business biblioteker, kan du utvide den [Skript for å deaktivere IRM for OneDrive for bedrifter](#BKMK_Script_OD4B_DisableIRM) delen.

###### <a name="BKMK_Script_OD4B_URLS"></a>Flere skript til å sende alle OneDrive for Business URL-adresser til en. CSV-fil
Du kan bruke følgende Windows PowerShell-skriptet til å trekke ut URL-adressene for alle brukere OneDrive for Business-biblioteker, som du kan kontroller deretter Rediger eventuelt og deretter importere i det primære skriptet for trinn 4c ovenfor.

Dette skriptet krever også den [SharePoint Online-klient komponenter SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) og [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Følg samme instruksjonene for å kopiere og lime den inn, lagre filen lokalt (for eksempel "rapport-OneDriveForBusinessSiteInfo.ps1"), endrer du   `$sharepointAdminCenterUrl` og `$tenantAdmin` verdier som før, og Kjør skriptet.

*&#42;&#42;Ansvarsfraskrivelse&#42;&#42;*: Dette eksempelskriptet støttes ikke under et standard kundestøtte for Microsoft-program eller en tjeneste. Dette eksempelskriptet leveres som den er uten garanti av noe slag.

```
# Requires Windows PowerShell version 3 <# Description: Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites. Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv"). Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> # URL will be in the format https://<tenant-name>-admin.sharepoint.com $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.onmicrosoft.com" $reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv" $oneDriveForBusinessSiteUrls= @() $resultsProcessed = 0 function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # establish the client context and set the credentials to connect to the site $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl) $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs do { # build the query object $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext) $query.TrimDuplicates        = $false $query.RowLimit              = 500 $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site" $query.StartRow              = $resultsProcessed $query.TotalRowsExactMinimum = 500000 # run the query $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext) $queryResults = $searchExecutor.ExecuteQuery($query) $clientContext.ExecuteQuery() # enumerate the search results and store the site URLs $queryResults.Value[0].ResultRows | % { $oneDriveForBusinessSiteUrls += $_.Path $resultsProcessed++ } } while($resultsProcessed -lt $queryResults.Value.TotalRows) $oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

###### <a name="BKMK_Script_OD4B_DisableIRM"></a>Skript for å deaktivere IRM for OneDrive for bedrifter
Bruk følgende eksempelskript Hvis du vil deaktivere IRM for brukernes OneDrive for bedrifter.

Dette skriptet krever også den [SharePoint Online-klient komponenter SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) og [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Kopiere og lime inn innholdet, lagre filen lokalt (for eksempel "Deaktiver-IRMOnOneDriveForBusiness.ps1") og endre det   `$sharepointAdminCenterUrl` og `$tenantAdmin` verdier. Angi OneDrive for Business URL-adresser manuelt, eller bruke skriptet i forrige inndeling, slik at du kan importere disse, og deretter kjøre skriptet.

*&#42;&#42;Ansvarsfraskrivelse&#42;&#42;*: Dette eksempelskriptet støttes ikke under et standard kundestøtte for Microsoft-program eller en tjeneste. Dette eksempelskriptet leveres som den er uten garanti av noe slag.

```
# Requires Windows PowerShell version 3 <# Description: Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.com" $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com", "https://contoso-my.sharepoint.com/personal/user2_contoso_com", "https://contoso-my.sharepoint.com/personal/person3_contoso_com") <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row). Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv" #> $listTitle = "Documents" function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Remove-IrmConfiguration { [cmdletbinding()] param( [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List ) process { Write-Verbose "Disabling IRM Configuration on '$($List.Title)'" $List.IrmEnabled = $false $List.IrmExpire  = $false $List.IrmReject  = $false $List.InformationRightsManagementSettings.Reset() } end { if($List) { Write-Verbose "Committing IRM configuration settings on '$($list.Title)'" $list.InformationRightsManagementSettings.Update() $list.Update() $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() } } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # connect to Office365 first, required for SharePoint Online cmdlets to run Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential # enumerate each of the specified site URLs foreach($webUrl in $webUrls) { $grantedSiteCollectionAdmin = $false try { # establish the client context and set the credentials to connect to the site $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl) $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # initialize the site and web context $script:clientContext.Load($script:clientContext.Site) $script:clientContext.Load($script:clientContext.Web) $script:clientContext.ExecuteQuery() # load and ensure the tenant admin user account if present on the target SharePoint site $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName) $script:clientContext.Load($tenantAdminUser) $script:clientContext.ExecuteQuery() # check if the tenant admin is a site admin if( -not $tenantAdminUser.IsSiteAdmin ) { try { # grant the tenant admin temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null $grantedSiteCollectionAdmin = $true } catch { Write-Error $_.Exception return } } try { # load the list orlibrary using CSOM $list = $null $list = $script:clientContext.Web.Lists.GetByTitle($listTitle) $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() Remove-IrmConfiguration -List $list } catch { Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())" } } finally { if($grantedSiteCollectionAdmin) { # remove the temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null } } } Disconnect-SPOService -ErrorAction SilentlyContinue
```

## <a name="BKMK_Office2013Configuration"></a>2016 for Office og Office-2013: Konfigurasjon for klienter
Siden disse nyere versjoner av Office støtter opprinnelig Azure RMS, kreves ingen konfigurasjon av klientdatamaskin støtte for information rights management (IRM)-funksjoner for programmer, for eksempel Word, Excel, PowerPoint, Outlook og Outlook Web App. Alle brukere som har å gjøre er å logge deg på sine Office-programmer med sine [!INCLUDE[o365_1](../Token/o365_1_md.md)] legitimasjon, og de kan beskytte filer og e-post og bruker filer og e-postmeldinger som er beskyttet av andre.

Vi anbefaler imidlertid at du supplere disse programmene med Rights Management deler programmet, slik at brukere kan få fordelen av Office-tillegg. Hvis du vil ha mer informasjon, se den [Rights Management program for deling: Installasjon og konfigurasjon for klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) delen i dette emnet.

## <a name="BKMK_Office2010Configuration"></a>Office 2010: Konfigurasjon for klienter
For klientdatamaskiner å bruke Azure RMS med Office 2010, må de ha installert programmet Rights Management deling for Windows. Ingen ytterligere konfigurasjon er nødvendig enn brukere må logge på med sine [!INCLUDE[o365_1](../Token/o365_1_md.md)] legitimasjon de kan beskytte filer og bruke filer som er beskyttet av andre.

Hvis du vil ha mer informasjon om rettighetsadministrasjon deling av programmet, se den [Rights Management program for deling: Installasjon og konfigurasjon for klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) delen i dette emnet.

## <a name="BKMK_SharingApp"></a>Rights Management program for deling: Installasjon og konfigurasjon for klienter
RMS (Rights Management) deler programmet kreves å bruke Azure RMS med Office 2010-klientdatamaskiner, og anbefales for alle datamaskiner og mobile enheter som støtter Azure RMS. RMS deling programmet integreres med Office programmer ved å installere en Office-tillegg slik at brukere enkelt kan beskytte filer og e-post direkte fra båndet. Den tilbyr også Generell beskyttelse for filtyper som ikke støttes internt av Azure RMS, og et dokument sporingsområdet for brukere til å spore og oppheve som de er beskyttet.

### <a name="BKMK_SharingAppforWindows"></a>RMS deling av programmer for Windows: Installasjon og konfigurasjon
Hvis du vil installere og konfigurere RMS deling av programmer for Windows for distribusjon i bedrifter, kan du se den [Rights Management deling program administratorhåndboken](http://technet.microsoft.com/library/dn339003.aspx).

> [!TIP]
> Hvis du vil raskt installere og teste RMS deling program for en enkelt datamaskin, kan du se [laste ned og installere rettighetsadministrasjon deling program](http://technet.microsoft.com/library/dn574734.aspx) fra den [Rights Management deling Brukerhåndbok for programmet](http://technet.microsoft.com/library/dn339006.aspx).

### <a name="BKMK_SharingAppMovileDevices"></a>RMS deling program for mobile plattformer: Installasjon
Hvis du vil installere RMS deling program for mobile plattformer, kan du laste ned den aktuelle app ved hjelp av koblingene på den [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970). Ingen konfigurasjon kreves for å bruke Azure RMS med denne app.

## <a name="BKMK_RMSAPIs"></a>Andre programmer som støtter RMS-APIs: Installasjon og konfigurasjon
Denne kategorien omfatter LOB programmer som er skrevet internt ved hjelp av RMS-SDK og programmer fra programvareleverandører som er skrevet ved hjelp av RMS-SDK. For disse programmene, følger du instruksjonene som følger med programmet.

## Neste trinn
Når du har konfigurert programmene støtte Azure Rights Management, bruker du [Veikart for Azure Rights Management-distribusjon](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til å kontrollere om det finnes andre konfigurasjonstrinn som du vil gjøre før du ruller [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for brukere og administratorer. Hvis ikke, kan du se [Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) for de neste trinnene.

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

