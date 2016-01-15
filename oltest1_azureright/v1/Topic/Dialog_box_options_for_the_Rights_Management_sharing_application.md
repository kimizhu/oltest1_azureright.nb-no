---
description: na
keywords: na
title: Dialog box options for the Rights Management sharing application
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a
---
# Alternativene i dialogboksen for rettighetsadministrasjon deling av program
Bruke denne informasjonen til å angi alternativer i RMS deling program **legge til beskyttelse av** dialogboks eller **del beskyttet** dialogboks. Vil du se denne dialogboksen når du [beskytte en fil for å dele](http://technet.microsoft.com/library/dn574735.aspx) eller [beskytte en fil i stedet](http://technet.microsoft.com/library/dn574733.aspx) og velge egendefinerte tillatelser.

> [!IMPORTANT]
> Hvis alternativene du ser er forskjellige fra de som beskrives her, har du sannsynligvis ikke den nyeste versjonen av deling programmet installert. Du kan laste ned den nyeste versjonen fra den [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) siden.
> 
> Hvordan vet du Hvis du har den nyeste versjonen? Se etter **Microsoft Rights Management deling program** vises i programmer og funksjoner, og sjekk det tilsvarende versjonsnummeret. Hvis du vil se, og Bruk alternativene i tabellen, versjonen må være på minst **1.0.1770.0**. Du kan sjekke det nyeste versjonsnummeret fra nedlastingssiden.

I tillegg til alternativene du kan velge, kanskje du også lurer på:

-   [Hva er filen .ppdf som er opprettet automatisk?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_PPDF)

-   [Hva er forskjellen mellom Generell beskyttelse og innebygd (ukomprimert) beskyttelse?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative)

|Alternativet|Beskrivelse|
|----------------|---------------|
|**BRUKERE**|Hvis du ikke allerede har angitt en e-postadresse fra Outlook, kan du skrive inn e-postadressene til personene som du vil ikke kunne åpne filen.<br /><br />Hvis organisasjonen bruker den lokale versjonen av Rights Management (AD RMS), er e-postadressene du kan angi begrenset til personer i organisasjonen. Når det gjelder, og du prøver å angi ekstern e-postadresser, vil du se en melding som sier at konfigurasjonen til firmaet muliggjør deling av beskyttet innhold bare i firmaet. Hvis organisasjonen bruker Azure RMS, kan disse e-postadresser imidlertid være for personer i organisasjonen, eller for personer i en annen organisasjon.<br /><br />For eksempel: janetm@contoso.com; p.dover@Fabrikam.com|
|**Generell beskyttelse**|Hvis dette alternativet er valgt, betyr det at den merkede filen ikke kan beskyttes opprinnelig. Hvis du vil ha mer informasjon, kan du se. [Hva er forskjellen mellom Generell beskyttelse og innebygd (ukomprimert) beskyttelse?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative) i dette emnet.|
|**Viewer – Vis bare**<br /><br />**Redaktør – Vis og Rediger**<br /><br />**Medforfatter – Vis, Rediger, Kopier og Skriv ut**<br /><br />**Medeier – alle tillatelser** **Note:** Alle disse alternativene har en runde ikon foran navnet, som representerer en globus i verden. Dette ikonet blir brukt fordi det vanligvis at du velger ett av disse alternativene når du sender din tilknytning til noen i en annen organisasjon.|Velg ett av disse alternativene hvis du vil definere rettighetene for beskyttet dokumentet. Klikk alternativet for å vise en beskrivelse.<br /><br />Når du velger ett av disse alternativene, bare personene du angir i **brukere** har rettighetene du angir for å åpne og bruke dokumentet. Hvis de videresender til noen andre, vil for eksempel at dokumentet ikke åpnes.|
|Policymaler som systemansvarlig konfigurerer.<br /><br />Hvis for eksempel firmaet ditt heter Contoso, Ltd.: **Contoso, Ltd. - konfidensiell Vis bare** **Note:** Alle disse alternativene ha en firkantet ikon foran navnet, som representerer et kontorbygg. Dette ikonet blir brukt fordi det vanligvis at du velger ett av disse alternativene når du sender din tilknytning til noen i organisasjonen.|Når du deler et dokument med personer som arbeider for organisasjonen, kan du se de tilgjengelige policymalene som systemansvarlig konfigurerer. Velg én av disse når dokumentet ikke skal deles utenfor organisasjonen.<br /><br />Når du velger ett av disse alternativene, vil administratoren definerer rettighetene for dokumentet, og hvem som kan åpne.|
|**Disse dokumentene utløp**|Velg dette alternativet bare for tid-sensitive filer som du valgte brukere skal kunne åpne etter en dato du angir. Du kan fremdeles åpne den opprinnelige filen, men etter midnatt (tidssone), på dagen du angir, vil andre ikke kunne åpne filen.<br /><br />Dette alternativet er ikke tilgjengelig hvis du velger en policymal som systemansvarlig konfigurerer.|
|**Send meg e-post når noen prøver å åpne disse dokumentene**|**Note:** Dette alternativet er i forhåndsvisning.<br />Velg dette alternativet hvis du vil motta e-postvarsler når noen prøver å åpne dokumentet som du skal beskytte. E-postmeldingen vil si hvem som forsøkte å åpne den, når og om de var vellykket.<br /><br />Dette alternativet er bare tilgjengelig hvis organisasjonen bruker Azure RMS. Hvis organisasjonen bruker den lokale versjonen av Rights Management (AD RMS), vises ikke dette alternativet.|
|**Tillat meg å kalle tilbake tilgangen til disse dokumentene direkte**|Velg dette alternativet hvis du vil tilbakekalle tilgangen til dokumentene senere ved hjelp av dokumentsporing området, og opphevelse skal tre i kraft umiddelbart. Angi dette alternativet betyr som mens dokumentet ikke er opphevet, må brukere alltid imidlertid en Internett-tilkobling skal lese dokumentet, hver gang de åpner den. Det kan være noen scenarier der brukere kan ikke koble enheten til Internett, og brukere kan ikke lese dokumentet slik du hadde tenkt.<br /><br />Hvis du ikke velger dette alternativet, kan du fremdeles oppheve dokumentene senere, ved hjelp av dokumentet sporingsområdet. Men fordi brukerne ikke trenger en Internett-tilkobling skal lese dokumentet alltid, vet de ikke umiddelbart at dokumentet er opphevet, og kan fortsette å lese den før de neste godkjenner med Azure RMS. Maksimalt antall dager som noen kan fortsette å lese et beskyttet dokument som du har opphevet er 30 dager som standard, men en administrator kan endre denne verdien til å være større enn 30 dager eller færre.<br /><br />Dette alternativet er bare tilgjengelig hvis organisasjonen bruker Azure RMS. Hvis organisasjonen bruker den lokale versjonen av Rights Management (AD RMS), vises ikke dette alternativet.|

## <a name="BKMK_GenericNative"></a>Hva er forskjellen mellom Generell beskyttelse og innebygd (ukomprimert) beskyttelse?

-   Når du **beskytte generisk en fil**, uautoriserte personer kan ikke åpne filen. Men etter at autoriserte personer åpner filen, kan deretter videresende den ubeskyttet til andre personer eller lagre den på et sted som andre kan få tilgang. De gjør imidlertid se en melding som forteller dem hvilke tillatelser de har for filen, og de blir bedt om å overholde disse, men denne typen beskyttelse ikke kan håndheves. Når du beskytter generisk en fil, kan du begrense tillatelser ytterligere godkjenning. For eksempel du kan ikke begrense innholdet til skrivebeskyttet eller ikke skrives ut.:

    > [!NOTE]
    > En generisk beskyttet fil har alltid en filtype av **.pfile**.

-   I sammenligning, når du bruker den **innebygd beskyttelse (ukomprimert)** av Rights Management med programmer som støtter dette (for eksempel Office-filer), beskyttelsen gjelder for filen selv om filen sendes deretter til noen annen person eller lagret på et annet sted. Og når du beskytter disse filene, kan du bruke restriktive tillatelser som skrivebeskyttet, eller tillatelse til å redigere, men ikke skrive ut eller kopiere. Du kan for eksempel velge **Viewer – Vis bare**, slik at innholdet ikke kan redigeres, skrives ut eller kopieres.

Hvis du vil ha mer teknisk informasjon, se den [Beskyttelsesnivåer – opprinnelig og generisk](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection) delen i den [Rights Management deling program administratorhåndboken](../Topic/Rights_Management_sharing_application_administrator_guide.md).

## <a name="BKMK_PPDF"></a>Hva er filen .ppdf som er opprettet automatisk?

-   Når du deler en beskyttet fil via e-post (delt beskyttet), RMS deling programmet automatisk oppretter en **.ppdf** versjon av filen for Word, Excel, PowerPoint eller PDF-fil. Dette er en skrivebeskyttet beskyttet versjon av filen som bare autoriserte personer kan åpne, og sikrer at mottakerne kan alltid lese vedlegget, selv om de bruker en mobil enhet som ikke har et program som støtter rettighetsbehandling. Gi disse personene har RMS deling app installert, vil de kunne lese vedlegget.

    Bruk begrensningen fremtvinges i dette scenariet, i motsetning til en generisk beskyttet fil. Mottakeren kan ikke lagre denne versjonen av filen, og hvis de videresender vedlegget til en annen, forblir de opprinnelige begrensningene med dokumentet. Bare personer som er autorisert for beskyttet dokument, vil kunne åpne den.

    > [!NOTE]
    > En .ppdf-fil opprettes automatisk når du deler beskyttet (delt via e-post), men ikke blir opprettet når du beskytter på stedet.

## Eksempler og andre instruksjoner
For eksempler på hvordan du kan bruke IRM deling av programmet, og hvordan-instruksjoner, kan du se følgende deler fra Rights Management-brukerhåndboken for deling program:

-   [Eksempler for å bruke RMS deling av program](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [Hva vil du gjøre?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Se også
[Rights Management deling program Brukerhåndbok](../Topic/Rights_Management_sharing_application_user_guide.md)

