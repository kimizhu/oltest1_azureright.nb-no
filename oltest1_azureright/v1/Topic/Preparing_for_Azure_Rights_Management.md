---
description: na
keywords: na
title: Preparing for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
---
# Forbereder Azure Rights Management
Når du har registrert deg for et abonnement på sky og opprettet organisasjonen med en konto for [!INCLUDE[o365_1](../Token/o365_1_md.md)] eller Azure Active Directory, er du klar til å aktivere den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] service.

Før du gjør dette, må du imidlertid kontrollere at følgende er på plass:

-   Brukerkontoene og gruppene i skyen du oppretter manuelt eller automatisk opprettet og er synkronisert fra Active Directory Domain Services (AD DS).

    Når du synkroniserer lokale kontoer og grupper, trenger ikke alle attributter som skal synkroniseres. Se dette for en liste over attributter som må synkroniseres for Azure RMS, [Azure RMS delen](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectsync-attributes-synchronized/) fra Azure Active Directory-dokumentasjonen. For enkel distribusjon, anbefaler vi at du bruker [koble til Azure AD](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) å koble til din lokale mapper med Azure Active Directory, men du kan bruke en hvilken som helst mappe synkroniseringsmetoden som oppnår du samme resultat.

-   E-post-grupper i skyen som du vil bruke med Rights Management. Dette kan være innebygde grupper eller manuelt opprettede grupper som inneholder brukere som vil bruke IRM.

    Hvis du har Exchange Online, kan du opprette og bruke e-post grupper ved hjelp av Exchange-administrasjonssenteret. Hvis du har AD DS og synkroniserer til Azure AD, kan du opprette og bruke e-post-grupper som er sikkerhetsgrupper eller distribusjonsgrupper.

## Aktivere IRM
Som standard [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] er deaktivert når du registrerer deg for din [!INCLUDE[o365_2](../Token/o365_2_md.md)] eller Azure AD-konto. Slik aktiverer du [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] for organisasjonen, må du aktivere tjenesten. Hvis du vil ha mer informasjon, se [Aktivering av Azure Rights Management](../Topic/Activating_Azure_Rights_Management.md).

## Se også
[Konfigurere Azure Rights Management](../Topic/Configuring_Azure_Rights_Management.md)

