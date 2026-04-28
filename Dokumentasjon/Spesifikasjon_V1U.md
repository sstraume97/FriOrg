# FriOrg

_Fagsystem for frivillige og ideelle organisasjoner_

Bygget på Microsoft 365

## Funksjonell spesifikasjon og strategisk konsept
---

Versjon 1.0 - utvidet utgave

April 2026

# **Forord til versjon 1.0**

Versjon 0.9 av denne spesifikasjonen beskrev FriOrg som et solid, integrert fagsystem på Microsoft 365 - et alternativ til dagens fragmenterte verktøyflora. Versjon 1.0 går et skritt videre. Etter en gjennomgang av konkurransebildet og brukernes faktiske smertepunkter har vi løftet ambisjonen fra «godt integrert system» til «strategisk plattform med reelle konkurransefortrinn».

De viktigste tilleggene i denne utgaven:

- Vedtektsmotor som leser organisasjonens egne vedtekter og validerer at vedtak, valg og innkallinger følger dem.
- AI-assistent over saksarkivet med Microsoft Copilot - naturlig språk-søk, automatiske oppsummeringer, utkast til møtereferat og forslag til svar.
- Frivillighetstimer og dugnadslogg med direkte kobling til Frifond-rapportering og søkbarhet.
- Outlook-add-in som viser medlemskontekst sidestilt e-postene daglig leder mottar.
- Arvtaker-modul som strukturerer overdragelse av verv - onboarding, sjekklister og tilgangsoverføring.
- Sponsor- og giverdatabase med automatisk §6-50-rapportering til Skatteetaten og pipeline for storgivere.
- Krise- og hendelseshåndtering med anonym varsling, audit-trail og eskalering - bygget for organisasjoner som driver leirer, idrett, helserelatert arbeid.
- Multi-tenant for paraplyorganisasjoner, anonymisert benchmarking på tvers av kunder, og forberedelser for nordisk utvidelse.

Disse tilleggene posisjonerer FriOrg som «neste generasjon», ikke «enda et medlemsregister». Vi er fortsatt åpne for diskusjon om prioritering og rekkefølge.

# **1\. Innledning**

## **1.1 Bakgrunn og formål**

FriOrg skal være et helhetlig fagsystem for frivillige og ideelle organisasjoner i Norge. Systemet samler funksjonalitet som i dag dekkes av et titalls løsrevne verktøy - medlemsregister, regnskap, kommunikasjon, arrangement, søknader - i én plattform som er tilpasset frivillig sektors særegne behov.

Mange organisasjoner sliter med fragmenterte løsninger som hverken snakker sammen eller speiler organisasjonenes virkelighet. Tillitsvalgte skifter, lokallag opprettes og legges ned, medlemmer melder seg inn og ut, og rapporteringskrav fra Frifond, Bufdir, Lotteritilsynet og Skatteetaten endrer seg. FriOrg skal gjøre det enklere å drive forening - fra det minste lokallaget til den største landsorganisasjonen.

Med versjon 1.0 av spesifikasjonen utvider vi ambisjonen. FriOrg skal ikke bare digitalisere det som finnes; vi skal løse smertepunkter konkurrentene ikke har rørt - vedtektsfortolkning, kunnskapsoverdragelse mellom tillitsvalgte, AI-assistert saksbehandling og direkte verdikobling mellom frivillig innsats og rapportering.

## **1.2 Designprinsipper**

- **Bygges på Microsoft 365:** Utnytter eksisterende investeringer i Outlook, Teams, SharePoint, Power BI og Entra ID. FriOrg skal ikke duplisere det Microsoft allerede leverer - vi skal forsterke det.
- **Skalerbart fra lite til stort:** Et lokallag med 30 medlemmer og en landsorganisasjon med 50 000 skal kunne bruke samme system, med ulik konfigurasjon.
- **Frivillig-vennlig:** Tillitsvalgte er ikke IT-eksperter. Grensesnittet skal være selvforklarende, og standardoppgaver skal kunne løses uten opplæring.
- **Personvernforsterket:** GDPR-compliance er innebygd, ikke et tillegg. Slettefrister, samtykker og dataminimering er standardfunksjonalitet.
- **Norsk regulatorisk kontekst:** Direkte integrasjon med Brønnøysund, Altinn, Frifond, KORG og momskompensasjonsordningen.
- **Åpen og integrerbar:** REST API og webhooks for tilkobling til andre systemer. App-marketplace lar tredjepartsutviklere bygge på FriOrg. Ingen «vendor lock-in».
- **AI-forsterket, ikke AI-erstattet:** Microsoft Copilot er integrert i hele løsningen, men menneskelig dømmekraft styrer alle vedtak og kommunikasjon utad.

## **1.3 Målgrupper**

FriOrg har flere ulike brukergrupper med ulike behov. Spesifikasjonen tar utgangspunkt i følgende roller:

- **Daglig leder / generalsekretær** - overordnet drift, rapportering, økonomistyring, strategiske beslutninger.
- **Organisasjonsrådgiver / administrasjon** - løpende medlemshåndtering, fakturering, kommunikasjon, saksbehandling.
- **Lokallagsleder (frivillig)** - drift av eget lokallag, arrangement, medlemskontakt.
- **Tillitsvalgt med spesifikt verv** - likepersonkoordinator, økonomiansvarlig, ungdomsleder, brukermedvirker.
- **Vanlig medlem** - «Min side», påmelding, kontingent, kontaktinfo, samtykker.
- **Eksterne søkere og deltakere** - ikke-medlemmer som melder seg på arrangement eller søker om medlemskap.
- **Givere og sponsorer** - privatpersoner og virksomheter som donerer eller støtter prosjekt.
- **Revisor og kontrollkomité** - eksterne kontrollorganer med begrenset, lese-tilgang.

# **2\. Arkitektur og plattform**

## **2.1 Microsoft 365 som fundament**

FriOrg er bygget som en Microsoft 365-applikasjon. Det innebærer at organisasjonens egen tenant er hjemmebasen - data ligger i SharePoint og Dataverse, identitet håndteres av Entra ID, og kontorverktøyene Outlook, Word, Excel, Teams og OneNote er en integrert del av brukeropplevelsen.

Dette er en strategisk forutsetning, ikke en begrensning. Bygger man på M365 får man enterprise-grade infrastruktur (sikkerhet, lagring, tilgangsstyring, dokumentversjonering, samhandling) gratis i tilbud, og kan i stedet konsentrere utviklingsressursene om frivillig sektors særegne behov. Konkurrenter som bygger sin egen stack må allokere store deler av utviklingsbudsjettet til områder Microsoft løser bedre.

### **2.1.1 Tekniske bærebjelker**

| **Komponent**                    | **Funksjon i FriOrg**                                                                                                            |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Microsoft Dataverse**          | Strukturerte data: medlemmer, verv, kontingent, transaksjoner. Rad-nivå sikkerhet og revisjonslogg.                              |
| **SharePoint Online**            | Dokumentarkiv, intranett, sak/arkiv-funksjonalitet, lagring av vedlegg, retensjonsregler.                                        |
| **Entra ID**                     | Identitet, MFA, ekstern brukerinvitasjon (B2B/B2C) for medlemmer uten Microsoft-konto.                                           |
| **Power Platform**               | Power Apps for spesialfunksjoner, Power Automate for arbeidsflyt, Power BI for rapporter, Copilot Studio for AI-agenter.         |
| **Microsoft Teams**              | Møter, samhandling, kanaler per lokallag/utvalg. FriOrg-app i Teams gir oppgaver, godkjenninger og varsler uten å forlate Teams. |
| **Microsoft Copilot**            | AI-assistent i hele løsningen - saksoppsummering, tekstutkast, naturlig språk-søk på arkivet.                                    |
| **Azure Functions / Logic Apps** | Eksterne integrasjoner: Brreg, Altinn, Frifond, betalingstjenester, Vipps, Lovdata.                                              |

**Strategisk merknad: M365-avhengighet**

FriOrg krever at organisasjonen har et Microsoft 365-tenant - typisk Business Premium eller en Nonprofit-lisens. Organisasjoner på Google Workspace eller helt uten skybasert kontorpakke vil ikke kunne bruke FriOrg uten å migrere først.

Dette er bevisst valgt. Vi gir slipp på en mindre andel av markedet for å kunne levere en dypt integrert løsning med høy verdi for resten. Microsoft tilbyr Nonprofit-rabatter (opptil 10 gratis Business Premium-lisenser per organisasjon) som gjør terskelen lav for de fleste norske foreninger.

## **2.2 Datamodell - overordnet**

Sentralt i FriOrg står en utvidet kontaktmodell der personer kan ha flere parallelle relasjoner til organisasjonen samtidig: medlem, tillitsvalgt, ansatt, deltaker, giver, abonnent. Det er én kontakt - mange roller.

- **Kontakt** (person eller virksomhet) - grunnentitet.
- **Medlemskap** - tidsbegrenset relasjon mellom kontakt og organisasjonsenhet, med kategori, kontingent og status.
- **Verv** - tidsbegrenset rolle (leder, kasserer, varamedlem, likeperson) knyttet til en organisasjonsenhet, med arvtaker-pekere.
- **Organisasjonsenhet** - nasjonalt ledd, region, fylkeslag, lokallag, utvalg, gruppe - fleksibel hierarkimodell.
- **Husstand/familie** - samler kontakter for familiekontingent og felles utsendelser.
- **Hendelse** - arrangement, møte, kurs, oppdrag (likeperson, brukermedvirkning).
- **Transaksjon** - betaling, innbetaling, utbetaling, faktura, donasjon.
- **Frivillighetslogg** - registrert dugnadstid og frivillig innsats per kontakt, prosjekt og lokallag.
- **Sak** - arkivenhet, innkommende henvendelse eller styresak - med saksgang og habilitetskontroll.
- **Hendelse (avvik)** - uønsket hendelse, varsling, sikkerhetsbrudd - med audit-trail og eskaleringslogikk.

# **3\. Funksjonsmoduler**

Dette kapitlet beskriver hver modul i FriOrg, hva den løser, hvilken funksjonalitet den inneholder og hvordan den henger sammen med andre deler av systemet. Modulene merket med ★ er nye i versjon 1.0.

## **3.1 CRM - Kontakter, medlemmer og roller**

CRM-modulen er hjertet i FriOrg. Den samler all informasjon om personer og virksomheter organisasjonen har en relasjon til, og holder styr på hvilken rolle de har til enhver tid.

### **3.1.1 Medlemsregister**

- Innmelding via skjema, importeres fra fil, eller manuell registrering.
- Medlemskategorier (hovedmedlem, ungdom, student, pensjonist, æresmedlem, støttemedlem) med ulik kontingent og rettigheter.
- 15-årsregelen automatisert: husstandsmedlemmer konverteres til hovedmedlem ved 15-årsdag, med varsel og foreldresamtykke.
- Status (aktiv, venter på betaling, passiv, utmeldt) med automatiske overganger.
- Komplett historikk: når medlemmet meldte seg inn, hvilke verv hen har hatt, hvilke arrangementer og oppdrag, kommunikasjonshistorikk.
- Søk og segmentering på alle felter, lagrede segmenter for utsendelser.

### **3.1.2 Vervemodul**

- Vervekampanjer med trackbare lenker og QR-koder per kampanje og verver.
- Topp-ververe leaderboard med kvartals- og årsstatistikk.
- Belønningssystem (bonus, gaver, æresbevisninger) konfigurerbart per organisasjon.
- Onboarding-flyt for nye medlemmer: velkomst-e-post, fadderordning, første arrangement-anbefaling.

### **3.1.3 Digitalt medlemskort**

- Apple Wallet og Google Wallet-integrasjon.
- QR-kode for innsjekk på arrangement og rabatter hos partnere.
- Statusmerking (aktiv, æresmedlem, tillitsvalgt) på kortet.

### **3.1.4 Familie og husstand**

- Husstandsentitet samler 2+ kontakter med felles adresse og familiekontingent.
- Samtykker og kommunikasjon kan settes på husstandsnivå (én utsending per familie).
- Foreldresamtykke for medlemmer under 15 år, med automatisk varsel når barnet fyller 15.

### **3.1.5 Tillitsvalgte og ansatte**

- Verv-register koblet til organisasjonsenhet og periode.
- Habilitetsregister: bistillinger, familierelasjoner, økonomiske interesser. Varsel ved potensielt habilitetsproblem i saksbehandling.
- Valgperioder, varamedlemmer, valgkomitéens arbeidsverktøy.

### **3.1.6 Kompetansebase og sertifisering**

- Register over kurs, sertifikater og kompetansebevis per kontakt.
- Utløpsvarsel for kompetanse som må fornyes (likeperson, førstehjelp, beredskap).
- Kursadministrasjon: påmelding, gjennomføring, automatisk oppdatering av kompetanseregisteret.
- Eksport av kompetansebevis som digitale signerte dokumenter.

### **3.1.7 ★ Arvtaker- og overlappingsmodul**

Når en lokallagsleder, kasserer eller annen tillitsvalgt slutter, er kunnskapsoverdragelsen ofte katastrofal. Avgående bytter ut sin private e-post, papirer forsvinner, passord glemmes, og den nyvalgte starter på bar bakke. FriOrg skal løse dette.

- Per-verv sjekklister: «Hva skal du gjøre første uken som ny kasserer» - innebygd i systemet, ikke i en glemt Word-fil.
- Automatisk overføring av tilganger: når et verv overdras, flytter FriOrg over relevante SharePoint-tilganger, signaturrettigheter, abonnementer og innloggingsbruk i tilkoblede tjenester.
- Avgangs-pakke: avtroppende får en strukturert eksport-flyt der hen registrerer pågående saker, kontakter, kunnskap og praktisk informasjon før tilgangen lukkes.
- Onboarding-modul for nyvalgte: introvideoer, vedtekter for vervet, viktige kontakter, hvilke saker som er pågående, hvor finner jeg hva.
- Overlappingsperiode: avtroppende og påtroppende har felles tilgang i en konfigurerbar overgangsperiode (typisk 30 dager) for spørsmål og overdragelse.

**Hvorfor dette er en differensiator**

Frivillighetens største skjulte kostnad er kunnskap som forsvinner ved hver utskifting. En nyvalgt lokallagsleder bruker typisk 3-6 måneder bare på å forstå hva forrige leder drev med. Ingen av dagens systemer adresserer dette.

## **3.2 Økonomi**

### **3.2.1 Regnskapssystem**

Et innebygd, NRS-F-tilpasset regnskapssystem dekker behovene til de fleste små og mellomstore organisasjoner. Bilag, kontoplan, momshåndtering, periodisering, prosjektregnskap, avstemming.

- Norsk standard kontoplan med foreningstilpasninger.
- Prosjektregnskap kobler inntekter og kostnader til konkrete prosjekt og finansieringskilder (Frifond, Bufdir, gaver).
- Bankavstemming via PSD2/Open Banking mot DNB, Nordea, SpareBank 1 m.fl.
- SAF-T-eksport for revisor.
- Direkte integrasjoner mot Tripletex, Visma og Fiken for organisasjoner som vil beholde sitt eksisterende regnskapssystem.

Strategisk merknad: vi konkurrerer ikke mot 25 år gamle regnskaps-ISV-er på dybde. FriOrg dekker «godt nok» for små lag og integrerer dypt for større.

### **3.2.2 Fakturering og kontingentinnkreving**

- Kontingentkjøring én gang i året eller løpende, med automatiske purrerutiner (30/60/90 dager).
- AvtaleGiro og Vipps Faste betalinger som standard for medlemskontingent.
- KID-genererte fakturaer med EHF-utsending mot offentlige mottakere via Peppol.
- Inkassoflyt mot tredjeparts inkassoselskap, med automatisk overføring etter X dager.

### **3.2.3 Budsjett**

- Budsjett per organisasjonsenhet og prosjekt.
- Budsjett vs. faktisk-rapport i sanntid, drillbar fra prosjekt → kostnadssted → bilag.
- Excel-add-in lar økonomiansvarlig hente live-data og pushe budsjett tilbake.

### **3.2.4 Betalingsmodul**

- Vipps og kortbetaling for arrangement, kontingent og nettbutikk.
- Tilbakebetaling og kreditnota.
- Avstemming mot bank automatisk.

### **3.2.5 Nettbutikk og POS**

- Nettbutikk for medlemsartikler, bøker, billetter.
- POS-modul (kasse) for kiosk på arrangement og loppemarked.
- Lager- og produktstyring.
- Vipps-betaling og kortleser.

### **3.2.6 ★ Sponsor- og giverdatabase**

Givere og sponsorer er en egen kategori som krever annen behandling enn medlemmer. FriOrg tilbyr en dedikert giverdatabase med pipeline-funksjonalitet og automatisk skattefradrag.

- §6-50-rapportering automatisk til Skatteetaten: organisasjonen registreres som godkjent gavemottaker, givere får skattefradrag for gaver, FriOrg sender inn data årlig.
- Giverhistorikk per kontakt: når sist gitt, hva, til hvilket prosjekt, kommunikasjon.
- Pipeline for storgivere: lead → første samtale → forslag → avtale → oppfølging - på samme måte som en B2B-salgsprosess.
- Vipps Innsamling, fast donasjon, og engangsbidrag - alt samlet i én giverprofil.
- Anerkjennelse: takkebrev, gaveplaketter, æresplaketter automatisk generert fra giverhistorikk.
- Bedrifts-CRM: sponsoravtaler, motytelser, fakturering, rapportering tilbake til sponsor.

**Konkret ROI**

§6-50 gir privatpersoner inntil 25 000 kr i skattefradrag for gaver. Bedrifter får full fradragsrett. Organisasjoner som dokumenterer dette riktig henter typisk 15-30 % mer i donasjoner enn de som ikke gjør det. FriOrg automatiserer hele løypa.

## **3.3 Kommunikasjon (toveis)**

### **3.3.1 Kanaler**

- E-post (egen avsenderdomene, høy leveringskvalitet).
- SMS via norsk leverandør (Sveve, LINK Mobility).
- Digipost for digitale brev.
- Fysisk brev via Bring/Posten.
- Push-varsler i medlemsappen og Teams-app.
- Chat (Microsoft Teams og direktechat på nettsiden).

### **3.3.2 Ticketing/saksbehandling**

- Innkommende henvendelser fra alle kanaler samles i felles innboks.
- Tildeling, status, SLA og eskalering.
- Kanban-visning og prioriteringsmatrise.
- AI-kategorisering: innkommende henvendelser klassifiseres automatisk (klage/spørsmål/innspill/søknad).
- Forslag til svar basert på lignende tidligere saker (Copilot-drevet).

### **3.3.3 Segmentering og målgrupper**

- Segmenter basert på alle felter i CRM.
- Lagrede segmenter (alle ungdomsmedlemmer i Vestland, alle med utløpt likepersonkompetanse, etc.).
- A/B-testing av e-post.
- Detaljert leveringsrapport (åpning, klikk, svar).

## **3.4 Arrangement og påmelding**

### **3.4.1 Påmelding**

- Skjema med dynamiske spørsmål basert på arrangementtype.
- Betalingsmodul integrert (Vipps, kort, faktura).
- Bekreftelses-e-post, kalenderinnkalling (.ics).
- Venteliste med automatisk innkalling når plass ledig.
- Tilrettelegging-spørsmål (allergi, mobilitet, behov for tolk) håndteres skjermet.

### **3.4.2 Oppmøte og deltakelse**

- QR-innsjekk via medlemskort eller mobil.
- Manuell innsjekk for deltakere uten medlemskort.
- Deltakerstatistikk og no-show-rapport.
- Automatisk dugnadstime-registrering for frivillige (se 3.5.3).

### **3.4.3 Møter (Teams-integrasjon)**

- Saksliste med foredragsholdere, vedlegg, votering.
- Møtereferat med integrert skribent-rolle.
- Voterings-modul: enkelt flertall, kvalifisert flertall, hemmelig avstemning.
- AI-utkast til referat fra Teams-opptak (Copilot).
- Habilitetskontroll: når en sak meldes inn, sjekker FriOrg om noen i møtet er inhabile og varsler.

## **3.5 Loggføring og dokumentasjon**

### **3.5.1 Standardiserte logger**

- Likepersonoppdrag: dato, kanal, oppdragstype, kategori (anonymisert), oppfølging.
- Brukermedvirkningsoppdrag: oppdragsgiver, varighet, type oppdrag, honorar.
- Inhabilitetserklæringer for styresaker.
- Innsynskrav etter offentleglova/forvaltningsloven (for organisasjoner som mottar tilskudd).

### **3.5.2 Egendefinerte skjemaer**

- Skjemabygger med dra-og-slipp.
- Felles skjemabank med maler delt mellom organisasjoner.
- Innsendinger lagres som saker i saksarkivet.

### **3.5.3 ★ Frivillighetstimer og dugnadslogg**

Frivillig innsats er organisasjonenes viktigste ressurs, men de fleste fører ikke timene systematisk. Dette betyr tapt tilskudd, dårligere søknader og manglende anerkjennelse av enkeltmenneskers innsats.

- Mobilapp: medlemmer logger timer selv med dato, prosjekt og kategori.
- QR-kode på arrangement og dugnader: skann og start klokka, skann igjen for å stoppe.
- Automatisk tellig: deltakelse på arrangement, møter og oppdrag genererer timer uten manuell registrering.
- Akkumulering per person, lokallag, prosjekt - synlig på Min side og i lokallagets dashboard.
- Direkte kobling til Frifond-rapport, søknader til Sparebankstiftelsen, og årsrapport.
- Ledertavle (ledertavle / ledertabell): mest aktive lokallag og frivillige, anonymiserbart.
- Anerkjennelse: 100-timers-, 500-timers- og 1000-timers-merker, automatisk takkebrev og diplom.

**Strategisk verdi**

Tilskuddsgivere som Sparebankstiftelsen DNB og Stiftelsen Dam vekter dokumentert frivillig innsats tungt. En organisasjon som kan vise «4 218 dokumenterte frivillighetstimer i 2025» får systematisk høyere tildeling enn en som bare estimerer.

## **3.6 Rapportering og søknader**

### **3.6.1 Frifond**

- Automatisk generering av søknadsdata fra medlemsregister, lokallag og aktivitetsdata.
- Steg-for-steg-veiviser med automatisk validering mot Frifond-kravene.
- Direkte innsending via Altinn med BankID-signering.
- Sluttrapport per lokallag genereres automatisk fra aktivitets- og frivillighetsdata.

### **3.6.2 Momskompensasjon**

- Forenklet og dokumentert modell - automatisk valg av beste alternativ.
- Direkte uttrekk fra regnskapet.
- Innsending via Lottstift sin portal.

### **3.6.3 Årsrapportering**

- Automatisk rapport til Brønnøysund (Frivillighetsregisteret) og Skatteetaten.
- Årsmelding-mal med innfylling fra aktivitetsdata.
- Signering via BankID/Altinn.

### **3.6.4 Andre tilskudd**

- Bibliotek av tilskuddsordninger (Bufdir, Helsedirektoratet, Kulturrådet, lokale stiftelser) med frister og krav.
- Søknadskalender med automatiske påminnelser.
- Maler for søknader basert på tidligere innsending.

### **3.6.5 ★ Anonymisert benchmarking**

Hvor god er vi egentlig? FriOrg samler aggregerte, anonymiserte nøkkeltall på tvers av kunder og gir hver organisasjon en sammenligning mot relevante peers.

- Eksempel: «Foreningen din har 3,2 % medlemsfrafall i Q1 - gjennomsnittet for foreninger med 1 000-5 000 medlemmer er 4,8 %.»
- Aggregerte nøkkeltall per organisasjonsstørrelse, type (idrett, kultur, helse, interesse) og geografi.
- Bare deltakende organisasjoner får tilgang - opt-in for både datadeling og innsyn.
- All data anonymiseres etter k-anonymitetsprinsipper (minst 5 organisasjoner per peer-gruppe).

**Hvorfor dette skaper lock-in**

Når man har brukt benchmarking-funksjonen i ett år og ser sin egen utvikling mot peers, er det vanskelig å gå tilbake til å fly blindt. Verdien vokser med antallet kunder - en klassisk nettverkseffekt som de andre frivillighets-systemene ikke kan kopiere uten å starte fra null.

## **3.7 Fleksibel organisasjonsstruktur**

- Hierarkisk modell: nasjonalt → region → fylkeslag → lokallag → utvalg.
- Utvalg på tvers (ungdomsutvalg, fagutvalg) som ikke følger hierarkiet.
- Egendefinerte enhetstyper (menighet, klubb, gruppe - alt etter bransjespråk).
- Tilgangskontroll og rapportering følger strukturen automatisk.

### **3.7.1 ★ Multi-tenant for paraplyorganisasjoner**

Norges Idrettsforbund har 12 000 underforeninger. Trossamfunn har 200 menigheter. Studentsamskipnader, fagforbund og humanitære paraplyer har lignende strukturer - der hver underliggende enhet er juridisk selvstendig, men deler infrastruktur og rapportering.

- FriOrg kan kjøres som multi-tenant der hver underforening har egen datasilo, egen tilgang, eget regnskap.
- Paraplyorganisasjonen har konfigurerbar innsyn på tvers - typisk aggregerte tall, ikke personopplysninger.
- Felles maler, vedtekter og verktøy distribueres ovenfra; selvstendighet beholdes nedover.
- Hierarkiske databehandleravtaler bygges inn (paraply som behandlingsansvarlig på fellestjenester, underforening på egne data).
- Sentralisert lisensiering - paraply betaler en blokk, underforeninger får tilgang etter behov.

**Markedsåpning**

Multi-tenant åpner et helt annet marked enn enkelt-foreningskunden. Et idrettsforbund eller trossamfunn er en stor avtale i seg selv, og man får 12 000 underforeninger «på kjøpet». Krever betydelig arkitektur-arbeid, men det er en strategisk lås mot konkurrenter.

## **3.8 Sikkerhet og tilgangsstyring**

- MFA påkrevd for tillitsvalgte og ansatte.
- BankID som autentiseringsmetode for vanlige medlemmer.
- Rolle- og rad-nivå-sikkerhet i Dataverse.
- Detaljert audit-logg på alle endringer i sensitive felter.
- Eksternt revisor- og kontrollkomité-tilgang (se 3.16).
- Slettefrister og anonymisering automatisert.

## **3.9 Saks- og dokumentarkiv**

- Noark 5-inspirert struktur (uten full sertifisering, men med tilsvarende dataordning).
- SharePoint som lagringsmotor med retensjonsregler og versjonering.
- Saksgang med tildeling, status, frister, vedtak.
- Dokumenter, e-post og vedlegg knyttet til saker.
- Innsynsforespørsler etter offentleglova håndteres som egen sakstype.

### **3.9.1 ★ AI-assistent over saksarkivet**

Microsoft Copilot er bygget inn som en kjernedel av FriOrg, ikke som et tillegg. Dette er den mest synlige differensiatoren mot konkurrentene.

- **«Spør foreningen din»:** naturlig språk-søk på tvers av saksarkiv, vedtekter, tidligere protokoller og dokumenter. Eksempel: «Har styret vedtatt noe om habilitet siste 5 år?» - Copilot finner relevante vedtak, refererer til kildene og oppsummerer.
- **Automatisk saksoppsummering:** lange e-posttråder, saksdokumenter og møtereferat oppsummeres på 5-10 setninger med kilde-referanser.
- **Utkast til møtereferat:** fra Teams-opptak genereres et førsteutkast med sakslistereferanse, vedtak og handlinger. Skribenten kvalitetsikrer.
- **Utkast til svar:** innkommende henvendelser får forslag til svar basert på lignende tidligere saker, organisasjonens vedtekter og policy. Saksbehandler godkjenner eller redigerer.
- **Auto-kategorisering:** innkommende e-post og skjemaposter klassifiseres (klage / spørsmål / innspill / søknad / klage på enkeltvedtak) og rutes automatisk.
- **Vedtekts-fortolkning:** AI-en kan svare på spørsmål om organisasjonens egne vedtekter - alltid med direkte sitat og paragrafhenvisning.

**Personvern og kvalitet**

AI-en jobber kun innenfor organisasjonens egen tenant - ingen data brukes til å trene modeller eller deles med andre kunder. Alle AI-genererte tekster er merket og krever menneskelig godkjenning før de sendes utad. Copilot er en assistent, ikke en autopilot.

## **3.10 Skjemaløsning**

- Dra-og-slipp skjemabygger.
- Betinget logikk (vis felt X hvis svar Y).
- Flerstegs skjemaer for søknader.
- Innsendinger lagres som saker, kobles til kontakter, utløser arbeidsflyt.
- Anonyme skjemaer for varsling og innspill.

## **3.11 Publikasjoner**

- Medlemsblad-modul med abonnementshåndtering.
- Distribusjonsliste basert på medlemskap eller eksternt abonnement.
- Digitalt distribusjon (PDF, e-post, web) og fysisk utsending.
- Annonsestyring og fakturering.

## **3.12 Intranett**

- SharePoint-basert intranett for tillitsvalgte og ansatte.
- Nyheter, kunngjøringer, hurtiglenker.
- Wiki for vedtekter, retningslinjer, prosedyrer.
- Forum for diskusjon mellom tillitsvalgte.

## **3.13 Ekstranett (offentlig nettsted)**

- WordPress eller tilsvarende CMS for offentlig nettside.
- SSO mot Entra ID for redaktører.
- Skjema-poster fra nettsiden lagres direkte i FriOrg-saksarkivet.
- Medlemsinnmelding direkte fra nettsiden, integrert med CRM.

## **3.14 ★ Vedtektsmotor og regelvalidering**

Dette er den funksjonen som skiller FriOrg mest tydelig fra alle andre fagsystem for foreninger. Ingen konkurrent har noe i nærheten.

Organisasjonens egne vedtekter lastes opp og struktureres maskinlesbart. Etter første gangs oppsett - som FriOrg gjør sammen med kunden - fungerer vedtektene som regelmotor for hele systemet.

### **3.14.1 Hva motoren validerer**

- Innkalling: er årsmøtet innkalt med riktig frist (typisk 14 eller 30 dager)? Er sakslisten distribuert som vedtektene krever?
- Quorum: har styret nok oppmøtte til å fatte vedtak? Hvilke vedtak krever quorum og hvilke ikke?
- Stemmeregler: krever vedtaket simpelt flertall, kvalifisert flertall (2/3) eller absolutt flertall? Vedtektsendringer? Eksklusjon?
- Valgbarhet: hvem kan stilles til valg som leder? Må man være medlem i minst X år? Kan ansatte velges? Kan samme person ha verv A og B samtidig?
- Habilitet: er noen i forsamlingen inhabile i denne saken (familierelasjon, økonomisk interesse, tidligere arbeidsgiver)?
- Frister: protokoll skal signeres innen X dager, regnskap revideres innen Y, årsmelding distribueres senest Z.

### **3.14.2 Hvordan motoren brukes**

- I møtemodulen: når en sak meldes inn, sjekker FriOrg automatisk om vedtaket er gyldig basert på tilstede, vedtekter og habilitet. Varsel ved problem.
- I valgkomitémodulen: kandidater valideres mot valgbarhetskravene før de listes.
- I innkallinger: FriOrg påser at frister følges, og varsler hvis innkallingen er for sent ute.
- I vedtekts-fortolkning: medlemmer og tillitsvalgte kan stille spørsmål til AI-en om hva vedtektene sier - alltid med direkte sitat fra paragrafen.

**Smertepunkt nr. 1 for små foreninger**

Et lokallag i Vestland har akkurat hatt en kontroversiell eksklusjonssak. Var vedtaket gyldig? Hadde lokallaget quorum? Var innkallingen riktig? Trenger man jurist for å svare. Med vedtektsmotoren får man «Vedtaket oppfyller §7-3 (innkalling), §11 (quorum), men §14 (eksklusjon) krever 2/3 flertall - vedtaket fikk 58 % og er derfor ikke gyldig.»

## **3.15 ★ Krise- og hendelseshåndtering**

Organisasjoner som driver leirer, idrett, helserelatert arbeid eller arbeid med barn har lovkrav til å håndtere uønskede hendelser systematisk. I dag gjøres dette på Excel og e-post - som er en risiko.

- Innrapportering av avvik, uønskede hendelser, sikkerhetsbrudd og varslingssaker.
- Anonymitetsmodus for varslere - FriOrg lagrer rapporten kryptert, varsleridentitet er adskilt og kun tilgjengelig for et begrenset varslingsutvalg.
- Tidsstemplet hendelseslogg som ikke kan endres (audit-trail med kryptografisk signering).
- Automatisk eskalering til styre, daglig leder eller eksternt varslingsorgan etter konfigurerbare regler.
- Statistikk og trender: er det mønster? Samme person? Samme lokallag? Samme arrangement-type?
- Integrasjon mot Arbeidstilsynet for arbeidsplassrelaterte avvik, og mot Bufdir/barnevernlov-rapportering der relevant.
- Beredskapsplan og krisestab: i en akutt situasjon (alvorlig skade på arrangement, mediekrise, sikkerhetsbrudd) finnes ferdige sjekklister og kommunikasjonsmaler.

**Lov og praksis**

Arbeidsmiljøloven §2A-4 og barnevernloven §6-7 stiller krav til varslingsrutiner og hendelseslogg. De fleste små organisasjoner møter ikke kravene fullt ut. FriOrg løser dette uten at organisasjonen må kjøpe et eget HMS-system.

## **3.16 ★ Revisor- og kontrollkomitéportal**

Eksterne revisorer og interne kontrollkomitéer trenger jevnlig innsyn i organisasjonens data. I dag betyr dette at noen i sekretariatet bruker dager på å samle inn Excel-filer, dokumenter og pdf-er som sendes via e-post - med tilhørende risiko for feil og dataeksponering.

- Egne tilgangsroller for ekstern revisor og kontrollkomité med forhåndsdefinert lese-tilgang til relevante moduler.
- Selvbetjent tilgang til hovedbok, bilag, transaksjoner, styresaker og protokoller.
- Tidsbegrenset tilgang som automatisk utløper etter at oppdraget er fullført.
- Audit-spor: hver revisor-handling logges, slik at organisasjonen vet hvem som har sett hva.
- Direkte SAF-T-eksport til revisor.
- Ingen e-postutveksling av sensitive data.

**Konkret tidsbesparelse**

Sekretariatet bruker typisk 20-40 timer per år på revisor-forberedelser. Med portalen reduseres dette til under 5 timer. Risikoen for at sensitive data lekker via e-post eller blir værende i revisors innboks fjernes helt.

# **4\. M365-spesifikke supermakter**

M365-fundamentet er ikke bare et teknisk valg - det er en moat mot rene SaaS-konkurrenter. Dette kapitlet beskriver fire integrasjoner som utnytter M365-stacken aggressivt og gir brukeropplevelse konkurrentene ikke kan matche.

## **4.1 Teams som primær arbeidsflate**

Tillitsvalgte og ansatte bruker allerede Teams flere timer hver dag. FriOrg flytter inn dit i stedet for å trekke folk ut til en separat applikasjon.

- Teams-app som viser oppgaver, varsler, godkjenninger og frister i en personlig fane.
- «Adaptive Cards» dukker opp i kanaler: «Bjørn har sendt inn reiseregning på 1 240 kr - godkjenn?» med ja/nei-knapper og kommentarfelt.
- Meld inn medlem direkte i Teams via en chatbot.
- Sjekk medlemsstatus uten å forlate samtalen: «@FriOrg slå opp Anne Solberg».
- Slack-konkurrentene kan ikke matche dette på samme integrasjonsnivå.

## **4.2 Outlook-add-in for medlemskontekst**

Når en e-post fra et medlem åpnes i Outlook, vises et sidepanel med relevant kontekst - medlemstatus, verv, pågående saker, siste interaksjoner. Daglig leder eller kommunikasjonsansvarlig slipper å bytte mellom verktøy.

- Identifiserer avsender i medlemsregisteret automatisk.
- Viser status, verv, kontingent, siste 5 interaksjoner.
- Pågående saker hen er involvert i, med direkte lenke til saksarkivet.
- Ett-klikk-handling: «Logg denne samtalen som likepersonoppdrag», «Opprett sak», «Flagg som klage».
- Maler tilpasset organisasjonens kommunikasjonsstil for raske svar.

## **4.3 SharePoint som dokumentkjerne**

Vi bygger ikke et eget dokumenthåndteringssystem. Vi bruker SharePoint og brander det som FriOrg sin saksarkiv-modul - med ferdig oppsatte taksonomier, retensjonsregler, maler og automatiseringer.

- Organisasjonene får enterprise-grade DMS gratis i prisen.
- Brukerne får lavere læringsterskel - mange kjenner SharePoint allerede.
- Vi konsentrerer utviklingsarbeidet på frivillighetsspesifikke konfigurasjoner i stedet for grunnleggende DMS-funksjonalitet.

## **4.4 Excel som rapportverktøy for økonomer**

Mange kasserer-typer foretrekker Excel uansett hva systemet tilbyr. I stedet for å kjempe mot dette, omfavner FriOrg det.

- Excel-add-in henter live regnskapsdata med én knapp.
- Brukeren bygger egne pivottabeller, rapporter og analyser.
- Endringer i budsjett pushes tilbake til FriOrg.
- Filer kan deles på SharePoint og holdes synkronisert.

**Strategi**

Mange konkurrenter «låser» data i sitt eget grensesnitt for å skape avhengighet. Vi gjør motsatt: lar folk bruke verktøyet de allerede kan og foretrekker. Det skaper tillit og reduserer motstand mot å bytte fra dagens system.

# **5\. Integrasjoner**

## **5.1 Microsoft 365**

- Outlook (e-post, kalender, kontakter).
- Teams (møter, kanaler, chat, app).
- SharePoint (dokumentlagring, intranett).
- OneDrive (filsynk for tillitsvalgte).
- Power BI (rapporter).
- Power Automate (arbeidsflyt).
- Copilot (AI-assistanse).
- Excel (rapport-add-in).

## **5.2 Norske offentlige integrasjoner**

- Brønnøysundregistrene (Brreg, Frivillighetsregisteret) - automatisk validering og oppdatering.
- Altinn - innsending av rapporter og søknader, BankID-signering.
- Skatteetaten - §6-50-rapportering for skattefradrag på gaver.
- Folkeregisteret - adresse- og dødsfallsoppdateringer (krever konsesjon).
- Lotteritilsynet - momskompensasjon.
- KORG / Frifond / LNU - tilskuddsdata og rapportering.
- Lovdata Pro API - oppslag på lov, forskrift og dom for vedtekts-fortolkning.
- Bufdir og Helsedirektoratet - tilskudd og pliktrapportering.

## **5.3 Betalings- og kommunikasjonsleverandører**

- Vipps Mobilepay (betaling, faste betalinger, innsamling).
- Nets / Mastercard (kortbetaling).
- AvtaleGiro (BBS / NETS).
- DNB / Nordea / SpareBank 1 (PSD2 Open Banking for bankavstemming).
- Sveve / LINK Mobility (SMS).
- Posten / Bring (fysisk post, Digipost).
- EHF / Peppol (faktura til offentlige mottakere).

## **5.4 API og webhooks**

- REST API med OAuth 2.0-autentisering.
- Webhook-rammeverk for hendelser (medlem opprettet, betaling mottatt, sak avsluttet).
- OpenAPI 3.0-spesifikasjon med interaktiv dokumentasjon.
- Rate limits og brukskontroll.

## **5.5 ★ Integrasjons-marketplace**

Frivilligsentraler, fagforeninger, idrettslag, trossamfunn og humanitære organisasjoner har til dels svært ulike behov. I stedet for å bygge alt selv, åpner FriOrg en App Store-modell der tredjepartsutviklere kan publisere integrasjoner og spesialtilpasninger.

- Sertifiserte connectors med dokumentert sikkerhetsgjennomgang.
- Inntektsdeling med utviklere (70/30-modell, etter Salesforce AppExchange / Microsoft AppSource).
- Vurderinger, anmeldelser og brukstall.
- Kategorier: idrett, kultur, helse, religion, miljø, internasjonalt arbeid.
- Eksempler på connectors: idrettsforbund-spesifikke moduler, menighetsverktøy, fagforenings-tariffspørsmål, donor-management for bistandsorganisasjoner.

**Økosystem-effekt**

Når marketplace tar av, blir FriOrg ikke bare et system kunden bruker, men en plattform kunden bygger på. Bytte-kostnaden vokser eksponentielt - på samme måte som det er nesten umulig å forlate Salesforce eller Shopify når man har integrert med 15 third-party-løsninger.

# **6\. Brukerroller og typiske scenarier**

## **6.1 Bruker-personas**

Tre typiske brukere med ulike behov:

#### **Kari, daglig leder**

Kari leder et nasjonalt sekretariat med 4 ansatte. Hun bruker FriOrg til styring, rapportering, kommunikasjon med lokallag og tilskuddssøknader. Hun er på Outlook hele dagen og forventer at FriOrg snakker med Outlook og Teams sømløst.

#### **Bjørn, lokallagsleder (frivillig)**

Bjørn leder et lokallag i Vestland med 280 medlemmer. Han har vervet sitt på fritiden ved siden av en full jobb. Han bruker FriOrg sporadisk - typisk kvelder og helger - og har null tålmodighet for tunge opplæringsløp eller flere systemer. Det må bare virke.

#### **Anne, tillitsvalgt og likeperson**

Anne er pensjonert, valgt til lokallagsleder i Oslo, og sertifisert likeperson. Hun fører likepersonoppdrag, deltar i brukermedvirkning, og har tre verv parallelt. Hun trenger oversikt over sine egne aktiviteter og at systemet ikke gjør jobben mer komplisert.

## **6.2 Eksempel: Innmelding fra start til medlemskort**

La oss følge en innmelding fra ende til annen for å vise hvordan modulene henger sammen.

- **Steg 1:** Marit ser en annonse for organisasjonen og klikker «Bli medlem» på nettsiden. Hun fyller ut et kort skjema med navn, e-post, telefon og fylke.
- **Steg 2:** Skjemaet sendes til FriOrg via webhook. Adresse hentes fra Folkeregisteret basert på fødselsnummer (med samtykke). Lokallag tildeles automatisk basert på postnummer.
- **Steg 3:** Marit får velkomstbrev på e-post med Vipps-lenke for kontingent (450 kr). Hun betaler med ett klikk.
- **Steg 4:** Power Automate trigger: når betaling mottas, opprettes hovedmedlemskap aktivt. Lokallagsleder Bjørn får varsel i Teams om nytt medlem.
- **Steg 5:** Marit får digitalt medlemskort lagt til Apple Wallet. SMS bekrefter at hun er aktiv.
- **Steg 6:** Bjørn ringer henne velkommen - han ser i Outlook-add-in at hun nettopp meldte seg inn og at hun jobber innenfor et fagfelt relevant for lokallaget. Han inviterer henne til neste arrangement direkte fra Outlook.
- **Steg 7:** Marit melder seg på arrangementet, sjekker inn med QR-koden, og 3 timers frivillig innsats logges automatisk fordi hun stilte som vakt.

Hele prosessen: ingen manuell registrering for Bjørn, ingen Excel-import, ingen tapt kontakt mellom verktøy.

# **7\. Brukergrensesnitt - designprinsipper**

## **7.1 Designprinsipper**

- Microsoft Fluent Design som basis - kjent visuelt språk for M365-brukere.
- Norsk språk gjennomgående - alle felter, knapper, varsler og feilmeldinger på norsk bokmål, med nynorsk som valg.
- Tre nivåer av kompleksitet: enkel modus for medlemmer, standard for tillitsvalgte, avansert for administrasjon.
- Hurtighandlinger via kommandopalett (⌘K eller Ctrl+K) - søk og handling samme sted.
- Tilgjengelighet WCAG 2.2 AA som minimum, AAA der mulig.
- Mobiloptimalisert: alle medlemsvendte funksjoner fungerer like godt på telefon.
- Personlig preg: hver organisasjon kan tilpasse farger, logo og brand uten kode.

## **7.2 Hovedområder i administratorgrensesnittet**

- Hjem / Mine oppgaver - personlig oversikt og oppgavekø.
- CRM - Medlemmer, Verving, Kompetanse, Organisasjon, Tillitsvalgte.
- Økonomi - Oversikt, Fakturering, Regnskap, Budsjett, Nettbutikk, Givere.
- Drift - Arrangement, Møter, Kommunikasjon, Saksbehandling, Chat, Skjemaer, Loggføring.
- Innhold - Saksarkiv, Dokumenter, Publikasjoner, Intranett, Forum.
- Rapportering - Rapporter, Tilskudd, Benchmarking.
- System - Min side, Innstillinger, Integrasjoner, Marketplace.

## **7.3 Min side for medlemmer**

- Medlemsstatus, verv, kontingent.
- Kommende arrangementer hen er påmeldt.
- Personlig kompetanseoversikt med utløpsvarsler.
- Frivillighetstimer akkumulert med nivåmerker.
- Kvitteringer og fakturaer med skattefradragsoppsummering.
- Samtykker som kan oppdateres når som helst.
- GDPR-eksport av alle egne data med ett klikk.

# **8\. Implementeringsfaser**

FriOrg er et stort konsept. Det skal bygges i faser med konkrete leveranser i hver fase. Vi foreslår følgende rekkefølge:

## **8.1 Fase 1 - Fundament (måned 1-6)**

- Datamodell, kontakter, medlemskap, organisasjonsstruktur.
- Innmelding, kontingent, betaling (Vipps, AvtaleGiro).
- Min side med GDPR-eksport.
- Outlook-add-in for medlemskontekst.
- Power BI-rapporter på medlemstall.

Mål: 5 pilotorganisasjoner kan ta i bruk FriOrg som medlemsregister og kontingentinnkreving.

## **8.2 Fase 2 - Drift og kommunikasjon (måned 7-12)**

- Kommunikasjon (e-post, SMS, ticketing).
- Arrangement med påmelding og betaling.
- Saksarkiv og dokumenthåndtering.
- Frivillighetstimer (mobilapp og QR).
- Teams-app for tillitsvalgte.

Mål: pilotorganisasjonene driver løpende drift i FriOrg.

## **8.3 Fase 3 - Økonomi og rapportering (måned 13-18)**

- Innebygd regnskap eller dyp Tripletex/Visma/Fiken-integrasjon.
- Frifond, momskompensasjon, årsrapportering.
- Sponsor- og giverdatabase med §6-50-rapportering.
- Revisor- og kontrollkomitéportal.

Mål: organisasjonene kan gå et helt regnskapsår med FriOrg.

## **8.4 Fase 4 - AI og differensiatorer (måned 19-24)**

- Copilot-integrasjon for saksoppsummering, søk og utkast.
- Vedtektsmotor med regelvalidering.
- Arvtaker- og overlappingsmodul.
- Krise- og hendelseshåndtering.

Mål: FriOrg er tydelig differensiert mot konkurrentene og lanseres bredt i markedet.

## **8.5 Fase 5 - Plattform og økosystem (måned 25+)**

- Multi-tenant for paraplyorganisasjoner.
- Anonymisert benchmarking.
- Integrasjons-marketplace.
- Nordisk utvidelse: svensk Bolagsverket, dansk CVR, lokale tilskuddsordninger.

Mål: FriOrg er en plattform, ikke bare et produkt - med eget økosystem og internasjonalt potensial.

## **8.6 Avklaringer som bør tas tidlig**

- Hvor dypt skal regnskapsmotoren gå? Vår anbefaling: behold «godt nok» for små lag, integrer dypt mot Tripletex/Visma/Fiken for større. Konkurransen mot dedikerte regnskaps-ISV-er er tapt før den begynner.
- Hvordan håndteres organisasjoner uten M365-tenant? Anbefaling: hjelp dem med å sette opp Microsoft Nonprofit-lisenser (gratis for de fleste). Vi gir slipp på de som ikke vil - det er en bevisst markedsavgrensning.
- Skal FriOrg være SaaS eller kunde-tenant? Anbefaling: kunde-tenant. Hver organisasjon eier sine egne data, vi leverer applikasjon og oppdateringer.
- Prisemodell? Anbefaling: per-medlem-pris med grunnpris, slik at små lag betaler lite og store betaler mer. Marketplace-tjenester prises separat.
- AI og personvern: skal vi tilby Copilot-funksjonalitet uten at organisasjonen har sin egen Copilot-lisens? Anbefaling: gjør Copilot til en konfigurerbar kostnadsdrivende modul som kan slås av - men den blir nok det viktigste salgsargumentet for større kunder.

# **9\. Konkurransebildet og strategisk posisjon**

## **9.1 Norske konkurrenter i dag**

Markedet for fagsystemer til frivillige organisasjoner er fragmentert og preget av aldrende systemer. De viktigste aktørene:

- StyreWeb - bredt brukt, men teknologisk gammeldags og lite integrert med moderne kontorpakker.
- Hypersys - solid medlemsregister, svak på saksbehandling og kommunikasjon.
- Membit - moderne grensesnitt, men begrenset modulbredde.
- Egne Excel-baserte løsninger - overraskende vanlig blant små og mellomstore organisasjoner.
- Sammensatte SaaS-stacks (HubSpot for CRM, Mailchimp for kommunikasjon, Tripletex for regnskap, etc.) - fungerer, men tungt å vedlikeholde.

## **9.2 FriOrgs posisjonering**

FriOrg konkurrerer ikke på pris eller funksjonsbredde alene. Vi konkurrerer på integrasjon, intelligens og kontekstuell forståelse av frivillighetens behov.

| **Område**            | **Konkurrenter**                      | **FriOrg**                          |
| --------------------- | ------------------------------------- | ----------------------------------- |
| Plattform             | Lukket SaaS                           | M365-tenant, kunden eier data       |
| AI                    | Lite/ingen                            | Copilot dypt integrert              |
| Kommunikasjon         | Egen e-post, lite Outlook-integrasjon | Outlook-add-in, Teams-app           |
| Vedtekter             | Manuell tolkning                      | ★ Vedtektsmotor med regelvalidering |
| Kunnskapsoverdragelse | Ikke håndtert                         | ★ Arvtaker-modul                    |
| Frivillighetstimer    | Manuell Excel                         | ★ Mobilapp + QR + auto-tellig       |
| Givere                | Brevbasert eller eget verktøy         | ★ §6-50 + giver-CRM                 |
| Rapportering          | Statiske maler                        | Power BI + benchmarking             |
| Hendelser/varsling    | Excel + e-post                        | ★ Audit-trail + anonym varsling     |
| Økosystem             | Lukket                                | ★ App marketplace                   |

## **9.3 Hva vi velger å ikke konkurrere på**

- Egen videokonferanse - Teams er der allerede.
- Egen chat - Teams igjen.
- Egen filsynk - OneDrive.
- Dyp regnskapsmotor - Tripletex/Visma/Fiken har 25 års forsprang.
- Markedsføringsautomatisering på enterprise-nivå - HubSpot/Marketo er bedre.

Disse områdene tar vi via integrasjon, ikke duplikat. Det frigjør ressurser til områdene som faktisk skiller oss ut.

## **9.4 Nordisk utvidelse**

Norske systemer krysser sjelden landegrenser fordi de er bygget rundt Brreg, KID og norske tilskuddsordninger. FriOrg bør designes med dette i tankene fra dag én.

- Plug-in-arkitektur for landspesifikke registre: Brreg (NO), Bolagsverket (SE), CVR (DK).
- Plug-in for landspesifikke tilskuddsordninger.
- Lokal valutahåndtering, momslogikk og betalingsleverandører.
- Språkstøtte: norsk bokmål, nynorsk, svensk, dansk fra første versjon.

Skandinavisk marked er 4-5× det norske, og frivillighetssektoren har samme grunnstruktur i alle tre land.

# **10\. Avsluttende kommentarer**

Denne spesifikasjonen beskriver et ambisiøst, men gjennomførbart system. FriOrg er ikke «enda et medlemsregister». Det er en plattform som tar utgangspunkt i frivillighetens reelle behov - kunnskapsoverdragelse, vedtektsetterlevelse, dokumentasjon av frivillig innsats, kommunikasjon med givere - og bruker M365 som teknisk fundament for å levere noe ingen andre kan.

De ti viktigste differensierende funksjonene, oppsummert:

- Vedtektsmotor som validerer at vedtak, valg og innkallinger følger organisasjonens egne regler.
- AI-assistent over saksarkivet med Copilot - søk, oppsummering, utkast.
- Frivillighetstimer med mobilapp, QR og automatisk Frifond-kobling.
- Outlook-add-in som viser medlemskontekst sidestilt e-post.
- Arvtaker-modul som strukturerer overdragelse av verv.
- Sponsor- og giverdatabase med §6-50-rapportering.
- Krise- og hendelseshåndtering med anonym varsling.
- Revisor- og kontrollkomitéportal med tidsbegrenset tilgang.
- Multi-tenant for paraplyorganisasjoner.
- Anonymisert benchmarking på tvers av kunder.

Disse funksjonene posisjonerer FriOrg som «neste generasjon». De gir konkrete, målbare gevinster for kundene - sparte timer for sekretariatet, høyere tilskudd, færre habilitetsfeil, bedre kunnskapsoverdragelse, profesjonell givergjerning.

_Frivillighetens største skjulte kostnad er kunnskap som forsvinner. FriOrg er et system som husker det organisasjonen glemmer._

Vi er klare for å gå fra konsept til prototype. Neste steg er å definere pilotgruppe, prise utviklingsløpet og bestemme finansieringsmodell.

_- Slutt på spesifikasjon, versjon 1.0 -_
