# Besvarelse av refleksjonsspørsmål - DATA1500 Oppgavesett 1.3

Skriv dine svar på refleksjonsspørsmålene fra hver oppgave her.

---

## Oppgave 1: Docker-oppsett og PostgreSQL-tilkobling

### Spørsmål 1: Hva er fordelen med å bruke Docker i stedet for å installere PostgreSQL direkte på maskinen?

**Ditt svar:**

***Enkel installasjon -*** kan starte postres med bare en kommando, trenger ingen konfigurasjon eller noe andre bakgrunnsprosesser som krever ekstra tid og dypere tekniske kunnskaper(docker.com, 2022).
***Isolasjon -*** Databasen er i sin egen isolert container, uavhengig av os-en, dermed blir det ingen forstyrrelser med andre programvarer selv når de kjører på samme server og kan kjøre flere versjoner samtidig uten konflikt(rd-datarespons.no).
***"Kjører på samme server" -*** Fjerner problemet "men det fungerer på min PC", da når man er i en container så jobber man i prinsippet på "den samme maskinen"(rd-datarespons.no).
***Av/På -*** Like lett å avslutte postgres som å starte.

- 
---

### Spørsmål 2: Hva betyr "persistent volum" i docker-compose.yml? Hvorfor er det viktig?

**Ditt svar:**

Volumes er det som blir brukt for å lagre data på harddisken. Det er der Docker lagrer data permanent utenfor containerenes levetid. For selv da om man avslutter containeren, sletter eller omstarter så vil data overleve(docs.docker.com).

---

### Spørsmål 3: Hva skjer når du kjører `docker-compose down`? Mister du dataene?

**Ditt svar:**

Det vil stoppe og fjerne containere som er lagd med up. Data vil ikke bli mistet med mindre man tvinger det med "-V"(docs.docker.com).

---

### Spørsmål 4: Forklar hva som skjer når du kjører `docker-compose up -d` første gang vs. andre gang.

**Ditt svar:**

Første kjøring så opprettet det et statndard nettverk for å la tjenestene kommunisere med hverandre, så oppretter og starter Docker nye containere basert på de byggede bildene, fordi -d flagget blir brukt så startes tjenestene i bakgrunnen og evt spesifiserte volumer opprettes for å lagre data.

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

- Miljøvariabler er dynamisk navngitte verdier som kan påvirke oppførselen til programvare og prosesser i et operativsystem. De fungerer som innstillinger som kan brukes av programmer for å tilpasse oppførselen deres uten at man må endre koden og brukes ofte til å lagre konfigurasjonsinformasjon, som databasenavn, brukernavn, passord og API-nøkler.Fordelene er at sensitive data kan holdes utenfor kildekoden og endringer kan gjøres uten å endre koden, noe som gjør det lettere å tilpasse applikasjonen til forskjellige miljøer.
---

## Oppgave 2: SQL-spørringer og databaseskjema

### Spørsmål 1: Hva er forskjellen mellom INNER JOIN og LEFT JOIN? Når bruker du hver av dem?

**Ditt svar:**

INNER JOIN: 

LEFT JOIN:
---

### Spørsmål 2: Hvorfor bruker vi fremmednøkler? Hva skjer hvis du prøver å slette et program som har studenter?

**Ditt svar:**

[Skriv ditt svar her]

---

### Spørsmål 3: Forklar hva `GROUP BY` gjør og hvorfor det er nødvendig når du bruker aggregatfunksjoner.

**Ditt svar:**

[Skriv ditt svar her]

---

### Spørsmål 4: Hva er en indeks og hvorfor er den viktig for ytelse?

**Ditt svar:**

[Skriv ditt svar her]

---

### Spørsmål 5: Hvordan ville du optimalisert en spørring som er veldig treg?

**Ditt svar:**

[Skriv ditt svar her]

---

## Oppgave 3: Brukeradministrasjon og GRANT

### Spørsmål 1: Hva er prinsippet om minste rettighet? Hvorfor er det viktig?

**Ditt svar:**

[Skriv ditt svar her]

---

### Spørsmål 2: Hva er forskjellen mellom en bruker og en rolle i PostgreSQL?

**Ditt svar:**

[Skriv ditt svar her]

---

### Spørsmål 3: Hvorfor er det bedre å bruke roller enn å gi rettigheter direkte til brukere?

**Ditt svar:**

[Skriv ditt svar her]

---

### Spørsmål 4: Hva skjer hvis du gir en bruker `DROP` rettighet? Hvilke sikkerhetsproblemer kan det skape?

**Ditt svar:**

[Skriv ditt svar her]

---

### Spørsmål 5: Hvordan ville du implementert at en student bare kan se sine egne karakterer, ikke andres?

**Ditt svar:**

[Skriv ditt svar her]

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

