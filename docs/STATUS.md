# Status projekta

## Trenutačno stanje

- Projekt je inicijaliziran.
- Lokalni Git repozitorij ima početni commit i konfiguriran `origin` udaljeni repozitorij; pristup i sinkronizacija još nisu provjereni u ovom radu.
- Poslovna ideja, funkcionalni zahtjevi, MVP granice, otvorena pitanja i predložena arhitektura zapisani su u `docs/PRODUCT_CONTEXT.md`.
- Potvrđena je osnovna platforma: PHP backend na postojećem web hostingu i MySQL/MariaDB baza.
- Potvrđena je jedna frontend aplikacija s rutama `/employee` za zaposlenika i `/owner` za vlasnika.
- Za objavu je predviđena zasebna MORLOCK domena ili poddomena s vlastitim javnim document rootom; privatni PHP kod mora ostati izvan njega.
- Implementacija još nije započela.

## Zadnje dovršeno

- Dodane su početne datoteke za trajni kontekst: `AGENTS.md`, `README.md` i ovaj statusni zapis.
- Dodana je autoritativna specifikacija proizvoda: `docs/PRODUCT_CONTEXT.md`.
- Definiran je početni postupak za rad na više računala i nastavak rada u novom Codex chatu.

## Sljedeći korak

- Analizirati `docs/PRODUCT_CONTEXT.md`, jasno izdvojiti MVP i otvorena pitanja koja blokiraju početak implementacije.
- Potvrditi minimalnu PHP/MySQL/MariaDB arhitekturu, podatkovni model i podržanu verziju PHP-a prije pisanja programskog koda.
- Odrediti MORLOCK domenu/podomenu, njezin document root i provjeriti može li PHP učitati kod iz privatne susjedne mape.
- Provjeriti pristup i sinkronizaciju s konfiguriranim udaljenim Git repozitorijem prije rada na više računala.

## Otvorene odluke

- Podržana verzija PHP-a i dostupne mogućnosti postojećeg hostinga.
- Minimalna struktura PHP aplikacije i API-ja.
- Konkretni MySQL/MariaDB podatkovni model i pravila transakcija za sprječavanje dvostrukog najma.
- Konačna MORLOCK domena/poddomena i stvarna putanja njezina document roota.

## Poznati problemi

- Nema — projekt još nema implementaciju.
