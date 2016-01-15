---
description: na
keywords: na
title: Azure Rights Management Deployment Roadmap
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
---
# Veikart for Azure Rights Management-distribusjon
Bruk følgende trinn til å forberede, gjennomføre og administrere Azure Rights Management (Azure RMS) for organisasjonen.

Imidlertid Hvis du vil raskt prøve Azure RMS selv, heller enn rulle ut i et produksjonsmiljø, se [Rask Start opplæring for Azure Rights Management](../Topic/Quick_Start_Tutorial_for_Azure_Rights_Management.md).

> [!IMPORTANT]
> Før du gjør de følgende trinnene, må du kontrollere at du har gått gjennom [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md).

## Trinn 1: Kontroller at du har et abonnement som inkluderer Azure Rights Management
Det er mer enn én type abonnement som inkluderer [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Se den [Cloud-abonnementer som støtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) delen i den [Krav for Azure Rights Management](../Topic/Requirements_for_Azure_Rights_Management.md) emne, og kontroller at abonnementet inkluderer funksjonalitet du vil bruke i organisasjonen ved å referere til tabellen i [tilbud for sammenligning av Rights Management Services (RMS)](https://technet.microsoft.com/dn858608).

## Trinn 2: Forberede leier kontoen du bruker Rights Management
Før du begynner å bruke [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], gjøre følgende forberedelser:

1.  Kontroller at din Azure eller Office 365 leier inneholder brukerkontoene og gruppene som skal brukes av Azure RMS til å godkjenne brukere i organisasjonen. Om nødvendig opprette disse konto og grupper, eller synkronisere dem fra den lokale katalogen. Hvis du vil ha mer informasjon, se [Forbereder Azure Rights Management](../Topic/Preparing_for_Azure_Rights_Management.md).

2.  Bestemme om du vil at Microsoft skal behandle leier nøkkelen (standard), eller generere og behandle leier-nøkkelen selv (kjent som gir din egen nøkkel eller BYOK). Legg merke til at for øyeblikket, du ikke kan bruke BYOK Hvis du bruker Exchange Online. Hvis du vil ha mer informasjon, se [Planlegging og implementering av Azure Rights Management leier nøkkelen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

3.  Installere Windows PowerShell-modul for [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] på minst én datamaskin som har Internett-tilgang. Du kan gjøre dette trinnet nå eller senere. Hvis du vil ha mer informasjon, se [Installere Windows PowerShell for Azure Rights Management](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

4.  Hvis du bruker lokale Rights Management services: Utføre en overføring for å flytte nøkler, maler og URL-adresser til skyen. Hvis du vil ha mer informasjon, se [Migrering fra AD RMS til Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).

5.  Aktiver Rights Management, slik at du kan begynne å bruke tjenesten. Hvis det kreves en tretrinns distribusjon, konfigurere brukerkontroller kort for å begrense bruk av bestemte brukere. Hvis du vil ha mer informasjon, se [Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

Du kan også vurdere å konfigurere følgende:

-   Egendefinerte maler hvis standard rettigheter policymaler er ikke nok for organisasjonen. Du kan gjøre dette trinnet nå eller senere. Hvis du vil ha mer informasjon, se [Konfigurere egendefinerte maler for Azure Rights Management](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

-   Bruk kommentarer slik at du kan overvåke hvordan organisasjonen bruker Rights Management. Du kan gjøre dette trinnet nå eller senere. Hvis du vil ha mer informasjon, se [Logging og analysere Azure Rights Management-forbruk](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

## Trinn 3: Konfigurere programmer og tjenester for rettighetsadministrasjon
Konfigurasjon av programmene kan inkludere installere rettighetsadministrasjon deling av programmet og hvordan du aktiverer støtte for information rights management (IRM)-funksjoner i SharePoint Online eller Exchange Online. Hvis du vil ha mer informasjon, se [Konfigurere programmer for Azure Rights Management](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

Hvis du har eksisterende IT-tjenester trenger for å kontrollere filene som vil beskytte Azure RMS, for eksempel data lekkasje forebygging (DLP) løsninger, innhold kryptering gatewayer (CEG) og anti-malware produkter – Konfigurer tjenestekontoer for å være Superbrukere for Azure RMS. Hvis du vil ha mer informasjon, se [Konfigurere Superbrukere for Azure Rights Management og tjenester for oppdagelse eller gjenoppretting av Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

Hvis du har lokale tjenester som du vil bruke med Azure Rights Management, Installer og Konfigurer Rights Management-koblingen. Hvis du vil ha mer informasjon, se [Distribusjon av Azure Rights Management-kobling](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

## Trinn 4: Publisere og bruke rettighetsbeskyttet innhold
Du er nå klar til å publisere og bruke beskyttet innhold, og logg hvordan firmaet ditt bruker Rights Management. Hvis du vil ha mer informasjon, se [Ved hjelp av Azure Rights Management](../Topic/Using_Azure_Rights_Management.md).

## Trinn 5: Administrere Rights Management for leieradministrasjon kontoen etter behov
Når du begynner å bruke [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], kan det hende at [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] modul for Windows PowerShell nyttig å hjelpe skript eller automatisere administrative endringer. Hvis du vil ha mer informasjon, se [Administrasjon av Azure Rights Management ved hjelp av Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

