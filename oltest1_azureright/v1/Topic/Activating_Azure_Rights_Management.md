---
description: na
keywords: na
title: Activating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
---
# Aktivering av Azure Rights Management
Når du aktiverer [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (RMS) Azure, organisasjonen kan begynne å beskytte viktige data ved hjelp av programmer og tjenester som støtter denne løsningen for beskyttelse av informasjon. Administratorer kan også administrere og overvåke beskyttede filer og e-postmeldinger som organisasjonen eier. Du må aktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] før du kan begynne å bruke information rights management (IRM)-funksjoner i Office, SharePoint og Exchange og beskytte sensitive eller konfidensielle filer.

Hvis du vil ha mer informasjon om Azure Rights Management før du aktiverer tjenesten, for eksempel hva det løser forretningsproblemer, noen vanlig brukstilfeller og hvordan det fungerer, kan du se [Hva er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md)

> [!IMPORTANT]
> Før du aktiverer [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], må du kontrollere at organisasjonen din har en serviceavtale som inkluderer [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjenester. Hvis ikke, vil du ikke kunne aktivere Azure RMS.
> 
> Hvis du vil ha mer informasjon, se den [Cloud-abonnementer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emnet.

Etter at du har aktivert Azure RMS, alle brukere i organisasjonen kan bruke informasjonsbeskyttelse av på sine filer, og alle brukere kan åpne (forbruker) filer som er beskyttet av Azure RMS. Men hvis du foretrekker det, kan du begrense hvem som kan bruke informasjonsbeskyttelse av ved hjelp av kontrollene for kort for en tretrinns distribusjon. Hvis du vil ha mer informasjon, se den [Konfigurere kort kontroller for en tretrinns distribusjon](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls) delen i dette emnet.

## Når du aktiverer IRM
Bruk en av fremgangsmåtene nedenfor til å aktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

> [!TIP]
> Du kan også bruke Windows PowerShell-cmdlet [Aktiver Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx), for å aktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### Aktivere Rights Management fra Office 365 administrasjonssenteret

1.  Når du har registrert deg for en Office 365-plan som inkluderer Rights Management, [logge på Office 365 med arbeid eller et skoleprosjekt kontoen](https://portal.office.com/) som er administrator for Office 365-distribusjon.

2.  Hvis Office 365 administrasjonssenteret ikke vises automatisk på nytt, velger ikonet app Oppgavevelger i øverst til venstre og velger **Admin**. Den **Admin** side ved side vises bare for Office 365-administratorer.

    > [!TIP]
    > Admin center, se [om Office 365 administrasjonssenteret - Admin hjelp](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  I den venstre ruten utvider du **Innstillinger for**.

4.  Klikk **Rights Management**.

    > [!NOTE]
    > Hvis du ikke ser dette alternativet, kan det være fordi service plan eller produkt versjon kan ikke støtter rettighetsadministrasjon, eller det er ennå ikke oppgradert for å støtte Rights Management.
    > 
    > Bruk informasjonen i den [Cloud-abonnementer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emne for å kontrollere. Hvis din service plan eller produkt versjon støttes, men du ikke ser alternativet Rights Management, kan det være fordi tjenesten ikke er ennå oppgradert. Hvis du trenger hjelp med dette problemet, kan du sende en e-postmelding til [askipteam](mailto:askipteam@microsoft.com?subject=I%20cannot%20activate%20RMS).

5.  På den **RIGHTS MANAGEMENT** klikker du **Behandle**.

6.  På den **rights management** klikker du **aktivere**.

7.  Når du blir spurt **vil du aktivere IRM?**, klikker du **aktivere**.

Nå bør du se **Rights management er aktivert** og muligheten til å deaktivere.

#### Aktivere Rights Management fra Azure Management-portalen

1.  Når du har registrert deg for kontoen din Azure, [logge på Azure Management-portalen](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  I den venstre ruten klikker du **ACTIVE DIRECTORY**.

3.  Fra den **active directory** klikker du **RIGHTS MANAGEMENT**.

4.  Velg mappen som skal behandle for [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], klikker du **Aktiver**, og Bekreft handlingen.

    > [!NOTE]
    > Hvis du ser en feil under aktivering, kan det være fordi tjenesten plan eller produkt-versjonen ikke støtter [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].
    > 
    > Bruk informasjonen i den [Cloud-abonnementer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emne for å bekrefte RMS-støtte. Hvis du trenger hjelp med dette problemet, kan du sende en e-postmelding til [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).

Den **RIGHTS MANAGEMENT STATUS** skal nå vise **aktive** og **Aktiver** alternativet er erstattet med **DEACTIVATE**.

### Rights Management statusverdier og beskrivelser i Azure Management-portalen
I tillegg til den **aktive** status, som angir at Rights Management-tjenesten er aktivert og klar til bruk, du kan også se **inaktiv**, **er ikke tilgjengelig**, eller **ikke godkjent**.

|Status-verdi|Beskrivelse|
|----------------|---------------|
|**Aktiv**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] er aktivert og klar til bruk.|
|**Inaktiv**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] er deaktivert og må aktiveres før organisasjonen kan beskytte filer.|
|**Ikke tilgjengelig**|Den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] -tjenesten er nede. Prøv igjen senere.|
|**Uautorisert**|Du har ikke tillatelse til å vise statusen for den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjenesten. Kontoen er låst, eller du er ikke global administrator for den valgte leier.|

## <a name="BKMK_OnboardingControls"></a>Konfigurere kort kontroller for en tretrinns distribusjon
Hvis du ikke vil at alle brukere skal kunne beskytte filer umiddelbart ved hjelp av Azure RMS, kan du konfigurere brukerkontroller kort ved hjelp av den [Sett AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) Windows PowerShell-kommandoen. Før eller etter at du aktiverer Azure RMS, kan du kjøre denne kommandoen.

> [!IMPORTANT]
> Hvis du vil bruke denne kommandoen, må du ha minst versjon **2.1.0.0** av den [Azure RMS Windows PowerShell-modulen](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Hvis du vil kontrollere hvilken versjon du har installert, kjører du: **(Get-Module aadrm –ListAvailable).Version**

Hvis du vil i utgangspunktet bare administratorer i gruppen "IT-avdelingen" (som har en objekt-ID for fbb99ded-32a0-45f1-b038-38b519009503) skal kunne beskytte innhold til testing, bruker du følgende kommando:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Legg merke til at for dette alternativet, må du angi en gruppe. Du kan angi individuelle brukere.

Eller, hvis du vil sikre at bare brukere som er riktig lisensiert til å bruke RMS Azure kan beskytte innhold:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Når du bruker disse kontrollene for kort, alle brukere i organisasjonen kan alltid bruke beskyttet innhold som er beskyttet av din undergruppe av brukere, men de vil ikke kunne bruke beskyttelse av informasjon om seg selv fra klientprogrammer. Hvis du for eksempel se ikke de i klientene Office standardmaler som publiseres automatisk når Azure RMS er aktivert, eller egendefinerte maler du kan konfigurere.  Serverprogrammer, for eksempel Exchange, kan implementere sine egne per bruker kontroller for RMS-integrering å oppnå det samme resultatet.

## Neste trinn
Nå som du har aktivert [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for organisasjonen, bruker du [Veikart for Azure Rights Management-distribusjon](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til å kontrollere om det finnes andre konfigurasjonstrinn som du kanskje må gjøre før du ruller [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for brukere og administratorer. Du kan for eksempel bruke [egendefinerte maler](http://technet.microsoft.com/library/dn642472.aspx) koble dine lokale servere skal brukes for å gjøre det enklere for brukerne å bruke informasjonsbeskyttelse av i filer, [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] ved å installere den [RMS-kontakt](http://technet.microsoft.com/library/dn375964.aspx), og distribuere den [Rights Management deling program](http://technet.microsoft.com/library/jj585031.aspx) som støtter beskytte alle filtyper på alle enheter. Office-tjenester, for eksempel Exchange Online og SharePoint Online krever mer konfigurasjon før du kan bruke funksjoner (IRM-Information Rights Management). Imidlertid Hvis det er ingen andre konfigurasjon trinn som du trenger å gjøre, se [Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md) for operative veiledning til å støtte en vellykket distribusjon for organisasjonen.

Hvis du vil ha informasjon om hvordan programmene fungerer med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], kan du se [Hvordan programmer støtter Azure rettighetsbehandling](../Topic/How_Applications_Support_Azure_Rights_Management.md).

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

