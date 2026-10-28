# Rad na dva računala

## Osnovno pravilo

Git repozitorij je zajednički izvor istine za MORLOCK. Codexov lokalni projekt i njegovi chatovi nisu zamjena za Git: vezani su uz konkretno računalo i lokalnu mapu.

Za rad na oba računala svako računalo treba imati vlastiti klon istog odobrenog udaljenog repozitorija. U Codexu se na svakom računalu lokalno doda projekt koji pokazuje na taj klon.

## Rutina rada

## Brzi podsjetnik pri završetku rada

1. Reci Codexu: “Pripremi projekt za predaju rada prema `AGENTS.md`.”
2. Pregledaj prikazani `git diff`.
3. Ako je sve u redu, reci: “Commitaj promjene i pushaj ih.”
4. Na drugom računalu pokreni `git pull`.
5. Otvori MORLOCK i upotrijebi početni prompt iz odjeljka niže.

### Početak rada

1. Pokreni `git pull` u pravilnom klonu.
2. Otvori MORLOCK projekt u Codexu na tom računalu.
3. U novom chatu zatraži da Codex pročita `AGENTS.md`, `README.md`, `docs/STATUS.md` i ovu datoteku te provjeri stanje repozitorija.

### Završetak rada

1. Neka Codex pregleda promjene i ažurira dokumentaciju koja stvarno treba promjenu.
2. Pregledaj `git diff`.
3. Pokreni dogovorene provjere.
4. Nakon potvrde napravi commit i `git push`.

### Prijelaz na drugo računalo

1. Na prvom računalu dovrši commit i push.
2. Na drugom računalu napravi `git pull`.
3. Otvori novi Codex chat i upotrijebi početni prompt iz sljedećeg odjeljka.

## Početni prompt za novi Codex chat

> Pročitaj `AGENTS.md`, `README.md`, `docs/STATUS.md` i `docs/WORKFLOW.md`. Zatim pregledaj trenutačno stanje repozitorija i relevantnu Git povijest. Sažmi gdje je projekt stao, navedi sljedeći konkretni korak i ne mijenjaj datoteke dok ne potvrdim plan.

## Uloga razgovora i dokumentacije

Prethodni Codex chat je koristan za detalje trenutačnog razgovora, ali nije jedino mjesto za trajno znanje. Bitne odluke, upute za pokretanje, ograničenja, sljedeći koraci i poznati problemi moraju biti zapisani u repozitoriju.

## Sigurnost i poslovni podaci

Koristi samo udaljeni repozitorij i kućno računalo koje su dopušteni pravilima organizacije. Ne spremaj tajne, tokene, lozinke ili osjetljive poslovne podatke u repozitorij ili dokumentaciju.
