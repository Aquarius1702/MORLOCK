# Upute za Codex

## Svrha ovih uputa

Ovaj repozitorij je izvor istine za MORLOCK i radi se na više računala. Kod, trajne upute i status rada moraju ostati u Git-u kako bi novi Codex chat mogao nastaviti rad bez prethodnog razgovora.

`docs/PRODUCT_CONTEXT.md` je glavni poslovni i funkcionalni kontekst proizvoda. Razlikuj njegove oznake **DEFINIRANO**, **PREDLOŽENO** i **OTVORENO**. Ne tretiraj prijedlog kao prihvaćenu odluku i ne proširuj opseg bez potvrde.

Projekt je u inicijalnoj fazi. Prije predlaganja arhitekture, ovisnosti ili naredbi za pokretanje najprije pregledaj repozitorij i zatraži odluke koje bitno utječu na smjer projekta.

## Početak svakog novog chata

1. Pročitaj ovaj `AGENTS.md`, zatim `README.md`, `docs/PRODUCT_CONTEXT.md`, `docs/STATUS.md` i `docs/WORKFLOW.md`.
2. Pregledaj trenutačno stanje repozitorija i Git povijest relevantnu za zadatak.
3. Sažmi što razumiješ kao trenutačno stanje i predloži sljedeći korak prije većih izmjena.

## Način rada

- Prije izmjena sažmi što namjeravaš promijeniti.
- Ne uvodi novu ovisnost, vanjski servis ili trajnu promjenu konfiguracije bez izričitog zahtjeva ili odobrenja.
- Ne dodaj tajne, lozinke, pristupne tokene ni privatne konfiguracijske vrijednosti u Git.
- Nakon izmjena pokreni odgovarajuće provjere kada postoje te jasno navedi što je provjereno.
- Ne predstavljaj pretpostavke kao činjenice.

## Dokumentacija i predaja rada

- `README.md` je opis projekta i upute za ljude: svrha, pokretanje i osnovna uporaba.
- `docs/PRODUCT_CONTEXT.md` je autoritativna specifikacija proizvoda i opsega.
- `docs/STATUS.md` je kratka predaja rada: što je napravljeno, što slijedi, poznati problemi i način provjere.
- `docs/WORKFLOW.md` opisuje dogovoreni rad između dva računala.

Prije predlaganja commita pregledaj sve promjene i ažuriraj navedenu dokumentaciju samo ondje gdje se stvarno promijenilo stanje. Potom pokaži `git diff` i pričekaj potvrdu prije commita i pusha.
