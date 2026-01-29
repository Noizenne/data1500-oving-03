# Besvarelse av refleksjonsspørsmål - DATA1500 Oppgavesett 1.3

Skriv dine svar på refleksjonsspørsmålene fra hver oppgave her.

---

## Oppgave 1: Docker-oppsett og PostgreSQL-tilkobling

### Spørsmål 1: Hva er fordelen med å bruke Docker i stedet for å installere PostgreSQL direkte på maskinen?

**Ditt svar:**

***Enkel installasjon -*** kan starte postgres med bare en kommando, trenger ingen konfigurasjon eller noe andre bakgrunnsprosesser som krever ekstra tid og dypere tekniske kunnskaper(docker.com, 2022).
***Isolasjon -*** Databasen er i sin egen isolert container, uavhengig av os-en, dermed blir det ingen forstyrrelser med andre programvarer selv når de kjører på samme server og kan kjøre flere versjoner samtidig uten konflikt(rd-datarespons.no).
***"Kjører på samme server" -*** Fjerner problemet "men det fungerer på min PC", da når man er i en container så jobber man i prinsippet på "den samme maskinen"(rd-datarespons.no).
***Av/På -*** Like lett å avslutte postgres som å starte.

- 
---

### Spørsmål 2: Hva betyr "persistent volum" i docker-compose.yml? Hvorfor er det viktig?

**Ditt svar:**

`Volumes` er det som blir brukt for å lagre data på harddisken. Det er der Docker lagrer data permanent utenfor containerenes levetid. For selv da om man avslutter containeren, sletter eller omstarter så vil data overleve(docs.docker.com).

---

### Spørsmål 3: Hva skjer når du kjører `docker-compose down`? Mister du dataene?

**Ditt svar:**

Det vil stoppe og fjerne containere som er lagd med up. Data vil ikke bli mistet med mindre man tvinger det med "-V"(docs.docker.com).

---

### Spørsmål 4: Forklar hva som skjer når du kjører `docker-compose up -d` første gang vs. andre gang.

**Ditt svar:**

Første kjøring så opprettet det et statndard nettverk for å la tjenestene kommunisere med hverandre, så oppretter og starter Docker nye containere basert på de byggede bildene, fordi `-d` flagget blir brukt så startes tjenestene i bakgrunnen og evt spesifiserte volumer opprettes for å lagre data.

På andre kjøring så bruker Docker allerede eksisterne ressurser/funksjoner og unngår unødvendig opprettelser og bygging med minre man spesifiserer det.

- Å bygge bilder for tjenester i Docker betyr å opprette en selvstendig og portabel passe av applikasjonen som kan kjøres i containere. Dette gir konsistens og isolasjon for applikasjoner uavhengig av hvor de kjører.
---

### Spørsmål 5: Hvordan ville du delt docker-compose.yml-filen med en annen student? Hvilke sikkerhetshensyn må du ta?

**Ditt svar:**

Forskjellige måter å dele på:
1. Git og Github
2. Som vedlegg i en epost
3. Komprimere og sende over via chat applikasjoner som Discord.

Man burde passe på at man ikke deler sensitive data(f.eks passord), og da bruke miljøvariabler eller .env-filer som ikke deles.

- `Miljøvariabler` er dynamisk navngitte verdier som kan påvirke oppførselen til programvare og prosesser i et operativsystem. De fungerer som innstillinger som kan brukes av programmer for å tilpasse oppførselen deres uten at man må endre koden og brukes ofte til å lagre konfigurasjonsinformasjon, som databasenavn, brukernavn, passord og API-nøkler.Fordelene er at sensitive data kan holdes utenfor kildekoden og endringer kan gjøres uten å endre koden, noe som gjør det lettere å tilpasse applikasjonen til forskjellige miljøer.
---

## Oppgave 2: SQL-spørringer og databaseskjema

### Spørsmål 1: Hva er forskjellen mellom INNER JOIN og LEFT JOIN? Når bruker du hver av dem?

**Ditt svar:**

`INNER JOIN`: Bruker dette for å velge data fra to eller flere relaterte tabeller og den returnerer rader som har marchende verdiere i alle tabeller. Altså brukes det til når bare data fra begge tabeller eksisterer. F.eks kunder som har plassert ordre.

`LEFT JOIN(LEFT OUTER JOIN)`: Bruker dette for å velge rader fra en tabell som har eller ikke har tilsvarende rader i andre tabeller. Kan altså også være NULL. Brukes npr man trenger alle data fra en hovedtabell for så å se om det eksisterer i en sekundær tabell. F.eks alle studenter, uavhengig om de er registrert i et emne eller ikke.

Forskjellen er altså at INNER JOIN returnerer bare matchende verdier i begge tabeller, mens LEFT JOIN alle rader fra venstre tabell og de matchende verdiene fra høyre tabell, verdiene på høyre side vil få en NULL verdi.

---

### Spørsmål 2: Hvorfor bruker vi fremmednøkler? Hva skjer hvis du prøver å slette et program som har studenter?

**Ditt svar:**

Det bruker for å sikre referensiell integritet, slik at referanser mellom tabeller peker på gyldige rader. Det kan også hindre i å legge til verdier som ikke har noe tilsvarende verdier i den refererte tabellen. `Fremmednøkler` opprettholder også konsistens ved å automatisk oppdatere eller slette relaterte rader i den refererte tabellen når forandringer skjer i hovedtabellen. 

Hvis man prøver å slette et program som har studenter, så vil databasen nekte slettigen(som er standard) med mindre er spesifisert `ON DELETE CASCADE` eller tilsvarende regel som sier ellers.

---

### Spørsmål 3: Forklar hva `GROUP BY` gjør og hvorfor det er nødvendig når du bruker aggregatfunksjoner.

**Ditt svar:**

Aggregatfunksjoner er som "oppsummeringsverktøy". Istedet for å på hver enkelt rad for seg selv, tar de en hel bunt med rader og regner dem om til en enkelt verdi.
De 5 vanligste funksjonene:
- `COUNT()` : Teller antall rader
- `SUM()` : Legger sammen alle verdiene i en kolonne
- `AVG()` : Regner ut gjennomsnittet
- `MIN()` : Finner den laveste verdien
- `MAX()` : Finner den høyeste verdien

`GROUP BY` er en metode som splitter rader til grupper og bruker aggregatfunksjoner til hvert gruppe. Det er altså en funksjon som beregner en enkelt verdi basert på flere rader.

---

### Spørsmål 4: Hva er en indeks og hvorfor er den viktig for ytelse?

**Ditt svar:**

`Indeks` er som et stikkord, dette kan databasen bruke til å hoppe rett til riktig sted. 
Uten indeks ville databasen lest rader en etter en, og det krever enorme mengder med disklesing og tid. 
Med indeks så finner den seg rett til raden vi faktisk leter etter og bruker dermed en mer effektiv søkealgoritme som ofte er kalt for `B-Tree` for å finne frem. 

---

### Spørsmål 5: Hvordan ville du optimalisert en spørring som er veldig treg?

**Ditt svar:**

- Ikke bruke `SELECT *` som henter alle kolonner, det blir dyrt for det øker mengden data som må sendes over nettverket. Spesifiser nøyaktig kolonnene man trenger `SELECT navnm epost FROM..`.
- Bruke indekser, og dekke to kolonner som en indeks.
- Bruke INNER JOIN hvis man vet det finnes treff i begge tabeller.

---
1. **Hent alle studenter som ikke har noen emneregistreringer**
select s.fornavn, s.student_id 
from studenter s
left join emneregistreringer er on s.student_id = er.student_id 
where s.student_id is null; !!!Hjelp, ingen res
2. **Hent alle emner som ingen studenter er registrert på**
select e.emne_navn from emner e
left join studenter s on e.emne_id = s.student_id
where e.emne_navn is null; !!!Hjelp, ingen res
3. **Hent studentene med høyeste karakter per emne**
select e.emne_navn, s.fornavn, s.etternavn, er.karakter
from emneregistreringer er join studenter s on s.student_id = er.student_id
join emner e on er.emne_id = e.emne_id
where er.karakter = (select max(karakter) from emneregistreringer where emne_id = er.emne_id);
4. **Lag en rapport som viser hver student, deres program, og antall emner de er registrert på**
select s.fornavn, s.etternavn, p.program_navn, count(er.registrering_id) as antall_emner
from studenter s left join programmer p on s.program_id = p.program_id
left join emneregistreringer er on s.student_id = er.student_id group by s.student_id, s.fornavn, s.etternavn, p.program_navn;
5. **Hent alle studenter som er registrert på både DATA1500 og DATA1100**
select s.fornavn, s.etternavn from studenter s
join emneregistreringer er on s.student_id = er.student_id
join emner e on er.emne_id = e.emne_id
where e.emne_kode in ('DATA1500', 'DATA1100') group by s.student_id, s.fornavn, s.etternavn
having count(distinct e.emne_kode) = 2;
---

## Oppgave 3: Brukeradministrasjon og GRANT

### Spørsmål 1: Hva er prinsippet om minste rettighet? Hvorfor er det viktig?

**Ditt svar:**

Principle of Least Privilege - en av grunnpilarene i IT-sikkerhet.
Det betyr at en bruker, program eller prossess kun skal ha de rettighetene som er **strengt nødvendige** for å utføre en spesifikk oppgave og ingenting mer.

Det gjelder både:
- Omfang(Hvilke data man kan se(f.eks. kun egne rader i en tabell)).
- Funksjon(Hva man kan gjøre(f.eks. kun, lese og ikke endre eller slette noe)).
- Tid(Hvor lenge man har tilgang(f.eks. midlertidig tilgang til et prosjekt)).

Grunner til hvorfor det er viktig:

- Beskyttelse av skade ved angrep: Si hvis en studentbruker blir angrepet, og den brukeren har admin-rettigheter, så kan angriperen slette hele databasen. Hadde studentbrukeren derimot bare hatt tilgang til sitt eget view, så ville skadepotensialet blitt begrenset til kun studenten sin data.

- Beskyttelse mot menneskelige feil: Brukere kan gjøre feil. 

- GDPR: Prinsippet er lovpålagt i mange sammenhenger. F.eks krever GDPR at personopplysninger ikke skal være tilgjengelige for flere enn de som faktsik trenger dem for å gjøre jobben sin.
---

### Spørsmål 2: Hva er forskjellen mellom en bruker og en rolle i PostgreSQL?

**Ditt svar:**

Brukeren er definert som hvem som gjør det(innlogging) og rollen er definert som hva som kan gjøres(rettigheter).

---

### Spørsmål 3: Hvorfor er det bedre å bruke roller enn å gi rettigheter direkte til brukere?

**Ditt svar:**

- **Skalerbarhet**: Med f.eks 500 studenter, uten roller så måtte man kjøre 500 `GRANT`-spørringer hver gang man oppretter en ny tabell som studente skal se, men med roller så kjører du en `GRANT`-spørring til en f.eks student_self_view og alle 500 studenter får tilgang fordi de er medlemmer av rollen.

- **Sikkerhet**: Ved å bruke roller så er det enkelt å se hva en bruker kan og ikke kan gjøre. Det gjør det altså oversiktlig og man får god kontroll på det istedet for hvis rettighetene var spredt over mange tabeller og funksjoner.

- **Konsistens**: En rolle behandles likt og det gjør risikoen for at en bruker får tilgang til noe, mens en annen ikke får det fordi begge ligger i samme rolle. Det er lett å glemme hvem som har hvilke rettigheter hvis man manuelt skulle gitt de til enkeltpersoner.

- **Endring**: Enkelt å fjerne eller bytte rolle enn å fjerne hundrevis av enkeltrettigheter manuelt fra en enkeltperson.
---

### Spørsmål 4: Hva skjer hvis du gir en bruker `DROP` rettighet? Hvilke sikkerhetsproblemer kan det skape?

**Ditt svar:**

Det brukes for å slette objekter permanent, slik som tabeller, views, indekser eller hele databaser. 

Sikkerhetsproblemer som kan oppstå:
- Den mest åpenbare risikoen er permanent tap av data. For i motsetning til `DELETE`(som sletter rader i en tabell), fjerner f.eks `DROP TABLE` selve beholderen og alt av innhold. 
- DoS(Denial of Service) fordi selv om man har en backup, så tar det tid å gjenopprette. Appen i bruk vil krasje da tabellen ikke lenger blir funnet som forventet og skaper nedetid for alle brukere.
- Det vil også ødelegge dataintegritet da tabellene henger sammen via relasjoner(fk) og kan skape kaos i databasestrukturen og logikken.

---

### Spørsmål 5: Hvordan ville du implementert at en student bare kan se sine egne karakterer, ikke andres?

**Ditt svar:**

Lage en view-tabell for å se på sine egne karakterer med studenten sine andre informasjon og gi rollen tilgang til view-tabellen med bare select.

---
1. **Opprett en rolle `program_ansvarlig` som kan lese og oppdatere programmer-tabellen, men ikke slette**
* I admin:

- create role program_ansvarlig login password 'program_ansvarlig';

- grant select, update on programmer to program_ansvarlig ;

* I program_ansvarlig:
- select * from programmer;

- update programmer set beskrivelse = 'Bachelor i Informatikk(I)' where program_id = 1;

2. **Opprett en rolle `student_self_view` som bare kan se sitt eget studentdata (hint: bruk en VIEW)**
* I admin:

- create role student_self_view login password 'student_self_view';
- create view self_view as select * from studenter where epost = SESSION_USER;
- grant select on self_view to student_self_view;

* I student_self_view:

- select * from self_view;
3. **Gi `foreleser_role` tilgang til å lese fra `student_view` (som allerede er opprettet)**

- grant select on self_view to foreleser_role;

4. **Opprett en rolle `backup_bruker` som bare har SELECT-rettighet på alle tabeller**

- grant select on programmer,studenter, emneregistreringer, emner to backup_bruker;

5. **Lag en oversikt over alle roller og deres rettigheter**

- select grantee, privilege_type from  information_schema.role_table_grants;

---

## Notater og observasjoner

Bruk denne delen til å dokumentere interessante funn, problemer du møtte, eller andre observasjoner:

[Skriv dine notater her]


## Oppgave 4: Brukeradministrasjon og GRANT

1. **Hva er Row-Level Security og hvorfor er det viktig?**
   - Svar her...

2. **Hva er forskjellen mellom RLS og kolonnebegrenset tilgang?**
   - Svar her...

3. **Hvordan ville du implementert at en student bare kan se karakterer for sitt eget program?**
   - Svar her...

4. **Hva er sikkerhetsproblemene ved å bruke views i stedet for RLS?**
   - Svar her...

5. **Hvordan ville du testet at RLS-policyer fungerer korrekt?**
   - Svar her...

---

## Referanser

- PostgreSQL dokumentasjon: https://www.postgresql.org/docs/
- Docker dokumentasjon: https://docs.docker.com/

