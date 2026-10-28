# MORLOCK
## Projektni kontekst, funkcionalna specifikacija i smjernice za razvoj

**Naziv proizvoda:** Morlock  
**Radni slogan:** Rental Time Machine  
**Alternativni slogan:** Time is our business  
**Kategorija:** SaaS aplikacija za upravljanje vremenski ograničenim najmom rekvizita  
**Primarno tržište:** Globalno tržište, s početnim fokusom na manje iznajmljivače  
**Status:** Definiranje proizvoda i priprema za razvoj

---

# 1. SVRHA OVOG DOKUMENTA

Ovaj dokument služi kao početni kontekst za razvoj aplikacije Morlock u Codexu.

Sadrži poslovnu ideju, dosad donesene odluke, funkcionalne zahtjeve, predloženu arhitekturu i otvorena pitanja.

**Važna uputa za Codex:**

Nemoj pretpostaviti da su svi tehnički prijedlozi u ovom dokumentu konačne odluke.

Razlikuj:

- **DEFINIRANO** – zahtjev koji je vlasnik projekta izričito prihvatio.
- **PREDLOŽENO** – preporuka koju tek treba potvrditi.
- **OTVORENO** – pitanje koje još nije riješeno.

Nemoj samostalno proširivati opseg aplikacije bez prethodnog dogovora.

Osnovna filozofija projekta je jednostavnost, brzina rada i minimalan broj operacija koje zaposlenik mora izvršiti.

---

# 2. OSNOVNA POSLOVNA IDEJA

Morlock je aplikacija za upravljanje najmom rekvizita na određeno vrijeme.

Za razliku od većine postojećih aplikacija za najam, Morlock **nije sustav za rezervacije (booking)**.

Aplikacija je namijenjena situacijama u kojima gost fizički dolazi na lokaciju, odabire dostupni rekvizit i plaća njegovo korištenje tijekom određenog razdoblja.

Primjer:

Na plaži se nalazi nekoliko trampolina.

Roditelj dolazi sa svojim djetetom i želi unajmiti trampolin na 30 minuta.

Zaposlenik:

1. Otvara Morlock.
2. Odabire odgovarajući trampolin.
3. Odabire trajanje najma iz unaprijed definiranog cjenika.
4. Vidi cijenu koju treba naplatiti.
5. Pokreće najam.

Aplikacija automatski prati vrijeme.

Nakon isteka plaćenog trajanja upozorava zaposlenika da treba pozvati roditelja po dijete.

Nakon isteka dodatnog dopuštenog vremena zaposlenik može dobiti još izraženije upozorenje.

Kada je trampolin stvarno slobodan, zaposlenik završava najam.

Rekvizit ponovno postaje dostupan.

## 2.1. Što Morlock jest

- Sustav za praćenje vremenski ograničenih najmova.
- Sustav za upravljanje raspoloživošću rekvizita.
- Sustav za upravljanje zaposlenicima i njihovim pristupom.
- Sustav za evidentiranje najmova i očekivanog prometa.
- Sustav za centralizirano upravljanje više lokacija.
- SaaS proizvod s licenciranjem prema broju zaposlenika.

## 2.2. Što Morlock nije

Morlock u početnoj verziji nije:

- Booking sustav.
- Online trgovina.
- Sustav za online naplatu.
- Kartični procesor.
- Fiskalna blagajna.
- Računovodstveni program.
- Sustav za registraciju gostiju.
- Aplikacija koju gost mora instalirati.
- Kompleksni ERP za iznajmljivače.

Ne treba uvoditi te funkcionalnosti samo zato što ih imaju drugi sustavi za najam.

---

# 3. CILJANI KORISNICI

Morlock je namijenjen malim i srednjim iznajmljivačima koji iznajmljuju opremu ili rekvizite na određeno vrijeme.

Početni primjeri:

- Trampolini.
- Pedaline.
- SUP daske.
- Kajaci.
- Vodeni parkovi.
- Bicikli.
- Različiti sportski rekviziti.
- Druga oprema koja se iznajmljuje na vremenski ograničene intervale.

Primjer s plažom služi za objašnjenje koncepta, ali arhitektura ne smije ograničiti aplikaciju samo na plaže ili turističke djelatnosti.

Morlock treba biti dovoljno generički da podržava različite djelatnosti bez izmjene osnovne poslovne logike.

---

# 4. ORGANIZACIJSKA HIJERARHIJA

**DEFINIRANO**

Osnovna struktura:

```text
MORLOCK
│
├── Vlasnički račun / Organizacija A
│   │
│   ├── Lokacija A1
│   │   ├── Grupa: Trampolini
│   │   │   ├── Trampolin 1
│   │   │   ├── Trampolin 2
│   │   │   └── Trampolin 3
│   │   │
│   │   ├── Grupa: Pedaline
│   │   │   ├── Pedalina 1
│   │   │   └── Pedalina 2
│   │   │
│   │   └── Grupa: Vodeni park
│   │
│   ├── Lokacija A2
│   │   ├── Grupa: Kajaci
│   │   └── Grupa: SUP
│   │
│   ├── Zaposlenici
│   ├── Licence
│   └── Administracija
│
└── Vlasnički račun / Organizacija B
    └── ...
```

## 4.1. Vlasnički račun

Vlasnički račun predstavlja poslovni subjekt koji koristi Morlock.

Jedan vlasnik može imati:

- Više lokacija.
- Više zaposlenika.
- Više kupljenih licenci.
- Više grupa rekvizita.
- Više pojedinačnih rekvizita.

Podaci različitih vlasničkih računa moraju biti međusobno izolirani.

## 4.2. Lokacija

Lokacija je fizičko mjesto na kojem se obavlja najam.

Primjeri:

- Plaža Zrće.
- Plaža Bačvice.
- Kamp A.
- Sportski centar B.

Jedna organizacija može imati neograničen ili tarifnim paketom ograničen broj lokacija. Konačna komercijalna ograničenja još nisu definirana.

## 4.3. Grupa rekvizita

Grupa okuplja rekvizite iste ili slične vrste na određenoj lokaciji.

Primjeri:

- Trampolini.
- Pedaline.
- Kajaci.
- SUP.

Na razini grupe definiraju se:

- Naziv.
- Dostupni vremenski paketi.
- Cijene.
- Grace In.
- Grace Out.

## 4.4. Rekvizit

Rekvizit je pojedinačna jedinica koja se iznajmljuje.

Primjeri:

- Trampolin 1.
- Trampolin 2.
- Pedalina 3.

Svaki rekvizit ima vlastito stanje raspoloživosti.

Ne smije istodobno imati dva aktivna najma.

---

# 5. KORISNIČKE ULOGE

## 5.1. Vlasnik / Administrator

**DEFINIRANO**

Vlasnik ima administracijsko sučelje.

Može:

- Upravljati lokacijama.
- Upravljati grupama rekvizita.
- Upravljati pojedinačnim rekvizitima.
- Definirati cjenike.
- Definirati Grace In i Grace Out.
- Dodavati i deaktivirati zaposlenike.
- Upravljati kupljenim licencama.
- Dodjeljivati i oduzimati licence.
- Određivati na kojim lokacijama zaposlenik smije raditi.
- Vidjeti trenutačno aktivne najmove.
- Vidjeti evidentirani promet.
- Pregledavati povijest najmova.

Vlasnik može pregledavati stanje više lokacija iz jednog računa.

**PREDLOŽENO:** Administrativni pregled ne zahtijeva dodatnu zaposleničku licencu. Ako vlasnik osobno želi pokretati i završavati najmove, tada koristi jednu zaposleničku licencu.

## 5.2. Zaposlenik

**DEFINIRANO**

Zaposlenik koristi operativno sučelje.

Može:

- Prijaviti se u sustav ako ima aktivnu licencu.
- Odabrati jednu od lokacija za koje ima dopuštenje.
- Pregledavati rekvizite i njihovu raspoloživost.
- Pokretati najmove.
- Vidjeti cijenu prema cjeniku.
- Pratiti preostalo vrijeme.
- Primati upozorenja o isteku.
- Završavati najmove.

Zaposlenik ne uređuje cjenike niti administrira licence.

**OTVORENO:** Treba definirati može li zaposlenik ispravljati pogrešno evidentirani najam i pod kojim uvjetima.

## 5.3. Voditelj lokacije

**PREDLOŽENO**

Moguća dodatna uloga između vlasnika i zaposlenika.

Nije obvezna za MVP.

Ne uvoditi je bez potrebe.

---

# 6. LICENCIRANJE

Ovo je jedan od važnih dijelova poslovnog modela Morlocka.

**DEFINIRANO**

Morlock se naplaćuje prema broju zaposleničkih licenci.

Licenca nije trajno vezana uz pojedinu osobu.

Licenca pripada vlasničkom računu, a vlasnik je dodjeljuje zaposleniku.

## 6.1. Primjer

Vlasnik kupuje pet licenci.

Ima šest zaposlenika.

Pet zaposlenika može imati aktivnu licencu, a šesti ne može pristupiti operativnom sustavu dok ne dobije licencu.

Ako zaposlenik napusti tvrtku:

1. Vlasnik mu oduzima licencu.
2. Licenca se vraća među raspoložive licence organizacije.
3. Vlasnik je dodjeljuje drugom zaposleniku.
4. Licenca zadržava postojeći datum isteka.

Vlasnik ne mora ponovno kupovati licencu samo zato što se zaposlenik promijenio.

## 6.2. Pravila

- Licenca ima vremensku valjanost.
- Jedna licenca može biti dodijeljena samo jednom zaposleniku u istom trenutku.
- Zaposlenik bez aktivne licence ne može pristupiti operativnom sučelju.
- Oduzimanje licence treba onemogućiti daljnje operacije.
- Povijest najmova mora ostati povezana s izvornim zaposlenikom.
- Brisanje ili deaktiviranje zaposlenika ne smije uništiti povijesne podatke.

## 6.3. Trajanje licenci

**PREDLOŽENO**

Podržati mjesečne i sezonske licence, primjerice:

- 1 mjesec.
- 3 mjeseca.
- 6 mjeseci.
- 12 mjeseci.

Točne cijene i trajanja nisu definirani.

## 6.4. Tehnička preporuka

Razdvojiti:

- Korisnički identitet.
- Kupljenu licencu.
- Dodjelu licence zaposleniku.

Nemoj koristiti isti podatkovni entitet za sve tri stvari.

---

# 7. PRISTUP LOKACIJAMA

**DEFINIRANO**

Jedan zaposlenik može imati pravo rada na više lokacija istog vlasnika.

Vlasnik u administracijskom sučelju određuje dopuštene lokacije.

Primjeri:

- Sve lokacije.
- Samo jedna lokacija.
- Dvije od četiri lokacije.
- Bilo koja druga kombinacija.

Zaposlenik se u jednom trenutku može operativno prijaviti samo na jednu lokaciju.

## 7.1. Postupak prijave

1. Zaposlenik se autentificira.
2. Morlock provjerava aktivnu licencu.
3. Dohvaća popis dopuštenih lokacija.
4. Zaposlenik odabire lokaciju.
5. Otvara se operativno sučelje te lokacije.

Ako zaposlenik ima pristup samo jednoj lokaciji, može se razmotriti njezin automatski odabir.

## 7.2. Promjena lokacije

Zaposlenik može prijeći na drugu dopuštenu lokaciju.

Pri tome se prethodna aktivna radna sesija zatvara ili zamjenjuje.

Ne smiju postojati dvije istodobne aktivne radne sesije istog zaposlenika na različitim lokacijama.

## 7.3. Autorizacija

Backend mora provjeravati:

- Identitet zaposlenika.
- Valjanost licence.
- Dopuštenje za lokaciju.
- Pravo izvršavanja konkretne operacije.

Provjera samo prilikom prijave nije dovoljna ako je vlasnik u međuvremenu oduzeo licencu ili pristup.

---

# 8. CJENICI

**DEFINIRANO**

Vlasnik definira cjenik za pojedinu grupu rekvizita na pojedinoj lokaciji.

Cjenik se temelji na unaprijed definiranim vremenskim paketima.

Primjer:

Grupa: Trampolini

| Trajanje | Cijena |
|---|---:|
| 15 minuta | 5 € |
| 30 minuta | 8 € |
| 60 minuta | 14 € |

Grupa: Pedaline

| Trajanje | Cijena |
|---|---:|
| 30 minuta | 12 € |
| 60 minuta | 20 € |

Zaposlenik odabire ponuđeni paket.

Morlock automatski prikazuje iznos koji treba naplatiti.

Time se smanjuje mogućnost pogreške zaposlenika.

## 8.1. Naplata

**DEFINIRANO**

Morlock ne obrađuje plaćanje.

Novac se naplaćuje izvan aplikacije.

Ne uvoditi:

- Kartične procesore.
- Online checkout.
- Integracije s POS terminalima.
- Fiskalizaciju.

Morlock evidentira vrijednost najma prema internom cjeniku.

## 8.2. Povijesne cijene

**PREDLOŽENO – važan zahtjev za integritet podataka**

Kada se najam pokrene, potrebno je spremiti cijenu primijenjenu na taj najam.

Kasnija promjena cjenika ne smije promijeniti povijesni promet.

## 8.3. Cijena po minuti

**DEFINIRANO**

U početnoj verziji ne uvoditi obračun cijene po minuti.

Vlasnik definira konkretna trajanja i cijene.

Obračun po minuti može se razmotriti u budućnosti ako korisnici pokažu stvarnu potrebu.

---

# 9. VREMENSKA LOGIKA NAJMA

Ovo je središnja funkcionalnost Morlocka.

**DEFINIRANO**

Svaka grupa rekvizita ima:

- `grace_in`
- `grace_out`

Svaki vremenski paket ima:

- `duration`
- `price`

## 9.1. Grace In

Grace In predstavlja vrijeme između evidentiranja/prodaje najma i početka obračunatog trajanja korištenja.

Primjer:

- Najam evidentiran u 10:00.
- Grace In = 3 minute.
- Plaćeno trajanje = 30 minuta.

Početak obračunatog vremena je u 10:03.

Čak i ako gost fizički počne koristiti rekvizit u 10:01, za potrebe Morlocka početak ostaje 10:03.

Ne traži se dodatna potvrda stvarnog početka korištenja.

To je namjerno pojednostavljenje.

## 9.2. Trajanje najma

Trajanje je unaprijed definirano u cjeniku.

Primjer:

- 15 minuta.
- 30 minuta.
- 60 minuta.

Zaposlenik bira paket, a ne proizvoljno trajanje.

## 9.3. Grace Out

Grace Out predstavlja dopušteno dodatno vrijeme nakon isteka plaćenog trajanja.

Primjer s trampolinom:

Nakon isteka 30 minuta zaposlenik poziva roditelja da preuzme dijete.

Grace Out daje roditelju kratko vrijeme da dođe i preuzme dijete.

Ne radi se o dodatnom komercijalnom najmu, nego o praktičnom tolerancijskom razdoblju.

Kod drugih rekvizita Grace Out može služiti za povrat opreme.

## 9.4. Primjer kompletne vremenske linije

Postavke:

- Grace In = 3 minute.
- Trajanje = 30 minuta.
- Grace Out = 1 minuta.

| Vrijeme | Događaj |
|---|---|
| 10:00 | Evidentiran najam |
| 10:03 | Početak obračunatog trajanja |
| 10:33 | Istek plaćenog najma |
| 10:34 | Istek Grace Out razdoblja |

Formula:

```text
start_at = created_at + grace_in

expires_at = start_at + duration

grace_expires_at = expires_at + grace_out
```

## 9.5. Konfiguracija

Grace In i Grace Out:

- Definiraju se po grupi rekvizita.
- Izražavaju se u minutama.
- Mogu imati vrijednost 0.
- Vlasnik ih može promijeniti kad god želi.

Primjer:

```json
{
  "group": "Trampolini",
  "grace_in": 3,
  "grace_out": 1,
  "packages": [
    { "duration": 15, "price": 5.00 },
    { "duration": 30, "price": 8.00 },
    { "duration": 60, "price": 14.00 }
  ]
}
```

Ako se tijekom rada pokaže da su intervali prekratki ili predugi, vlasnik ih jednostavno prilagodi.

Ne treba komplicirati ovu logiku.

## 9.6. Promjena konfiguracije

**PREDLOŽENO**

Prilikom pokretanja najma spremiti tadašnje vrijednosti:

- Trajanje.
- Cijenu.
- Grace In.
- Grace Out.

Promjene konfiguracije trebaju vrijediti za buduće najmove, a ne retroaktivno mijenjati postojeće.

---

# 10. ŽIVOTNI CIKLUS NAJMA

**DEFINIRANO U OSNOVI; NAZIVI STATUSA SU PREDLOŽENI**

Najam prolazi kroz nekoliko logičkih faza.

```text
EVIDENTIRAN
    |
    v
GRACE IN
    |
    v
AKTIVNO PLAĆENO VRIJEME
    |
    v
GRACE OUT
    |
    v
PREKORAČENJE
    |
    v
ZAVRŠEN
```

Ako je Grace In ili Grace Out jednak nuli, odgovarajuća faza može trajati nula sekundi.

## 10.1. Važna razlika: status najma i status rekvizita

**DEFINIRANO**

Istek vremena ne oslobađa automatski rekvizit.

Primjer:

Pedalina je iznajmljena do 11:00.

Grace Out završava u 11:05.

Ako se gost nije vratio, pedalina je i dalje zauzeta.

Morlock može prikazivati da je vrijeme prekoračeno, ali ne smije omogućiti novi najam iste pedaline dok zaposlenik ne potvrdi da je stvarno slobodna.

To pravilo vrijedi za sve rekvizite.

## 10.2. Završetak najma

Zaposlenik izričito završava najam.

Tada se:

- Bilježi stvarno vrijeme završetka.
- Najam označava završenim.
- Rekvizit oslobađa.
- Zapis zadržava u povijesti.

---

# 11. TIMERI I TRAJNA POHRANA

**DEFINIRANO**

Svi podaci o najmovima, tekućim i završenim, moraju se spremati u bazu podataka.

Gašenje aplikacije ne smije prekinuti ili poništiti najam.

Ako zaposlenik zatvori preglednik ili aplikaciju i ponovno je otvori, mora vidjeti isto stanje najmova, ažurirano prema stvarno proteklom vremenu.

## 11.1. Arhitekturno načelo

**Baza podataka i backend predstavljaju izvor istine.**

Timeri se prikazuju i izračunavaju na strani klijentske aplikacije.

Backend ne mora imati zaseban timer koji svake sekunde odbrojava svaki najam.

Umjesto toga, spremaju se apsolutne vremenske oznake.

Primjer:

```json
{
  "rental_id": 123456,
  "resource_id": 3,
  "employee_id": 12,
  "price": 8.00,
  "duration_min": 30,
  "grace_in_min": 3,
  "grace_out_min": 1,
  "created_at": "2026-07-15T10:00:00+02:00",
  "start_at": "2026-07-15T10:03:00+02:00",
  "expires_at": "2026-07-15T10:33:00+02:00",
  "grace_expires_at": "2026-07-15T10:34:00+02:00",
  "closed_at": null
}
```

Primjer je ilustrativan, nije konačna shema.

## 11.2. Izračun preostalog vremena

Frontend izračunava razliku između vremena isteka i trenutačnog vremena.

Primjer:

```javascript
const remainingMs =
    new Date(rental.expires_at).getTime() - Date.now();
```

Prikaz se može osvježavati svake sekunde.

Ne treba smanjivati brojač po principu:

```javascript
remaining--;
```

Takav brojač može postati netočan zbog:

- Pauziranja JavaScript timera u pozadini.
- Zaključavanja telefona.
- Usporavanja preglednika.
- Ponovnog otvaranja aplikacije.

Umjesto toga, pri svakom osvježavanju treba ponovno izračunati razliku iz apsolutnog vremena.

## 11.3. Ponovno pokretanje aplikacije

Pri otvaranju operativnog sučelja:

1. Backend identificira zaposlenika i njegovu lokaciju.
2. Provjerava licencu i prava.
3. Dohvaća sve nezavršene najmove te lokacije.
4. Vraća njihove vremenske oznake.
5. Frontend izračunava trenutačno stanje.
6. Prikazuje odgovarajuće timere i upozorenja.

Ako je najam istekao dok je aplikacija bila zatvorena, odmah se prikazuje kao istekao ili prekoračen.

Ne smije se ponovno pokretati od početka.

## 11.4. Sinkronizacija vremena

**PREDLOŽENO**

Voditi računa o razlici između sata mobilnog uređaja i sata servera.

Moguće rješenje je da backend uz podatke vraća i serversko vrijeme, a frontend računa korekciju.

---

# 12. RAD VIŠE ZAPOSLENIKA

**DEFINIRANO**

Na istoj lokaciji može raditi više zaposlenika.

Svi trebaju vidjeti aktualno stanje rekvizita.

Ako jedan zaposlenik pokrene najam, drugi zaposlenici moraju vidjeti da je rekvizit zauzet.

## 12.1. Sinkronizacija

**PREDLOŽENO**

Koristiti WebSocket za distribuciju promjena stanja.

Primjeri događaja:

- Pokrenut najam.
- Završen najam.
- Produžen najam, ako se ta funkcija uvede.
- Promijenjena raspoloživost rekvizita.
- Promijenjena prava zaposlenika.

Za početni prototip može se koristiti i periodičko dohvaćanje stanja.

## 12.2. Sprječavanje dvostrukog najma

**OBVEZNO TEHNIČKO PRAVILO**

Ako dva zaposlenika gotovo istodobno pokušaju iznajmiti isti rekvizit, backend mora dopustiti samo jednu operaciju.

To treba riješiti na razini baze i transakcija.

Nije dovoljno da frontend provjerava prikazuje li se rekvizit kao slobodan.

---

# 13. POVIJEST I EVIDENCIJA PROMETA

**DEFINIRANO**

Svi najmovi moraju ostati u bazi.

Vlasnik mora moći vidjeti:

- Aktivne najmove.
- Zauzete i slobodne rekvizite.
- Evidentirani promet.
- Povijest najmova.
- Koji je zaposlenik evidentirao najam.
- Na kojoj se lokaciji najam dogodio.
- Koji je rekvizit korišten.
- Koji je vremenski paket odabran.
- Koja je cijena primijenjena.

## 13.1. Promet nije potvrđena naplata

Morlock ne obrađuje novac.

Zato evidentirani promet predstavlja vrijednost najmova prema cjeniku, a ne nužno potvrđenu gotovinsku ili kartičnu naplatu.

Tu razliku treba zadržati u terminologiji i izvještajima.

## 13.2. Dnevni promet

Za dnevne izvještaje treba koristiti lokalni kalendarski dan lokacije.

Konačni SQL upit mora biti prilagođen MySQL/MariaDB-u i odabranoj strategiji spremanja vremenskih oznaka. Mora grupirati najmove prema lokalnom datumu, od ponoći do ponoći.

**PREDLOŽENO:** Svaka lokacija može imati vlastitu vremensku zonu, što je korisno za globalni proizvod.

## 13.3. Povijest zaposlenika

Ako zaposlenik ode iz organizacije ili izgubi licencu, njegovi raniji najmovi moraju ostati sačuvani.

Nemoj brisati povijesne podatke zbog promjena zaposleničkih računa.

---

# 14. VREMENSKI TIPOVI PODATAKA

Razmatrane su tri mogućnosti:

1. MySQL/MariaDB `DATETIME` vrijednosti spremljene u UTC-u.
2. MySQL/MariaDB `TIMESTAMP` vrijednosti.
3. Unix epoch u sekundama ili milisekundama.

## 14.1. Preporuka

**OTVORENO**

Konačni vremenski tipovi odredit će se pri projektiranju MySQL/MariaDB sheme. Bez obzira na odabrani tip, apsolutni trenutci moraju se spremati jednoznačno, a lokalna vremenska zona ne smije ovisiti o trenutačnoj postavci poslužitelja.

Ne koristiti 32-bitni `INTEGER` za epoch sekunde zbog ograničenja 2038. godine.

## 14.2. Frontend

U JavaScriptu koristiti epoch milisekunde za izračun timera.

Backend može slati ISO 8601 datume ili epoch vrijednosti, ali format API-ja treba biti dosljedan.

## 14.3. Vremenske zone

Sve apsolutne vremenske oznake trebaju predstavljati jednoznačne trenutke.

Lokalna vremenska zona koristi se za:

- Prikaz korisniku.
- Grupiranje po danima.
- Izvještaje.
- Lokalno poslovno vrijeme.

---

# 15. PREDLOŽENI MODEL BAZE PODATAKA

Ovo nije konačna shema, nego početni prijedlog entiteta.

| Entitet | Namjena |
|---|---|
| `organization` | Vlasnički računi |
| `user` | Identiteti korisnika |
| `organization_user` | Članstvo i uloge korisnika |
| `location` | Lokacije |
| `resource_group` | Grupe rekvizita |
| `resource` | Pojedinačni rekviziti |
| `rental_package` | Trajanje i cijena paketa |
| `license` | Kupljene licence |
| `license_assignment` | Dodjele licenci zaposlenicima |
| `employee_location` | Prava pristupa lokacijama |
| `work_session` | Aktivna lokacija zaposlenika |
| `rental` | Evidencija najmova |
| `audit_log` | Evidencija administrativnih promjena |

## 15.1. Osnovna polja tablice rental

Predložena polja:

```text
rental_id
organization_id
location_id
resource_id
employee_id

price
currency

duration_min
grace_in_min
grace_out_min

created_at
start_at
expires_at
grace_expires_at
closed_at

status
```

Napomene:

- `price` treba biti decimalni tip (`NUMERIC`), a ne floating-point.
- `currency` je koristan za međunarodno tržište.
- Statusi se mogu dijelom izvoditi iz vremenskih oznaka.
- `closed_at` označava stvarni završetak.
- Potrebno je spriječiti više nezavršenih najmova istog rekvizita.
- Konačne primarne ključeve i indekse treba projektirati prije implementacije.

## 15.2. Integritet podataka

Treba osigurati:

- Referencijalni integritet.
- Transakcijsko pokretanje najma.
- Transakcijsko završavanje najma.
- Sprječavanje dvostrukog zauzimanja rekvizita.
- Izolaciju podataka različitih organizacija.
- Povijesnu točnost cijena i vremenskih postavki.
- Dosljedno upravljanje licencama.

---

# 16. TEHNOLOŠKA ARHITEKTURA

**DJELOMIČNO DEFINIRANO**

MORLOCK će koristiti postojeći web hosting s PHP-om i MySQL/MariaDB bazom. PHP verziju, strukturu aplikacije i način objave još treba potvrditi.

### Frontend

- HTML.
- CSS.
- JavaScript.
- Responsive web aplikacija.
- Moguća PWA izvedba.

**DEFINIRANO:** Postoji jedna frontend aplikacija s odvojenim funkcionalnim dijelovima prema ulozi:

- `/employee` je operativno sučelje zaposlenika za rad s najmovima.
- `/owner` je administracijsko sučelje vlasnika.

Pristup rutama i svim pripadajućim API operacijama mora provjeravati PHP backend prema ulozi i ovlastima korisnika. Samo skrivanje dijelova sučelja nije dovoljna zaštita.

### Backend

- PHP na postojećem web hostingu.
- REST API.

**OTVORENO:** Treba odrediti treba li MVP-u sinkronizacija promjena stanja u stvarnom vremenu i kako je ostvariti u ograničenjima hostinga. Ne pretpostavljati WebSocket podršku.

### Baza podataka

- MySQL ili MariaDB na postojećem web hostingu.

### Autentifikacija

Sigurna autentifikacija s provjerom korisničkih ovlasti, organizacije, licence i lokacije.

Točan mehanizam autentifikacije nije definiran.

### Smještaj na postojećem hostingu

**PREDLOŽENO:** MORLOCK treba objaviti na vlastitoj domeni ili poddomeni s vlastitim document rootom, odvojeno od glavne domene hostinga i drugih postojećih web-stranica.

Javno dostupni document root treba sadržavati samo `index.php` i statičke datoteke. PHP poslovna logika, konfiguracija, migracije i logovi trebaju biti izvan njega. Javni `index.php` učitava aplikaciju iz privatne mape istog hosting računa.

Prije implementacije treba potvrditi stvarni document root nove domene i provjeriti dopušta li hosting učitavanje privatnog PHP koda iz susjedne mape (`open_basedir`).

### Dijagnostika i zapisivanje poruka

**DEFINIRANO U NAČELU:** Aplikacija treba prepoznati izvršava li se PHP iz konzole ili kroz web-poslužitelj te poruke zapisivati primjerenom kanalu.

- Pri izvršavanju iz konzole razvojne poruke mogu se ispisati u terminal.
- Kod web zahtjeva poruke se zapisuju u PHP/server error log; tehnički detalji ne smiju se prikazati korisniku.
- Okruženje mora biti izričito određeno postavkom, primjerice razvojno ili produkcijsko, a ne samo automatskim prepoznavanjem hostinga.
- `phpinfo()` smije služiti samo za privremenu dijagnostiku i ne smije ostati javno dostupno niti biti dio produkcijskog bootstrap koda.

## 16.1. Mobilni uređaji

Primarni uređaj zaposlenika vjerojatno će biti mobilni telefon.

Sučelje mora biti prilagođeno:

- Radu na otvorenom.
- Brzom odabiru rekvizita.
- Velikim dodirnim površinama.
- Minimalnom unosu teksta.
- Jasnom prikazu zauzetosti.
- Vidljivim timerima.
- Jednostavnom završavanju najma.

## 16.2. Offline rad

**OTVORENO**

Na plažama i sličnim lokacijama internetska veza može biti nepouzdana.

Potrebno je odlučiti hoće li MVP zahtijevati stalnu internetsku vezu ili podržavati ograničeni offline rad.

Offline pokretanje najmova s više zaposlenika uvodi problem sinkronizacije i mogućeg dvostrukog najma.

Ne uvoditi punu offline funkcionalnost bez posebne odluke.

## 16.3. Obavijesti

**OTVORENO – VAŽNO**

Morlock mora upozoriti zaposlenika kada najam istekne.

Treba odrediti kako se upozorenja ponašaju:

- Dok je aplikacija otvorena.
- Dok je preglednik u pozadini.
- Dok je telefon zaključan.
- Kada je aplikacija potpuno zatvorena.

Obični JavaScript timer ne jamči pouzdanu obavijest u svim tim stanjima.

Potrebno je odvojeno projektirati mehanizam obavještavanja.

Za početak su moguća vizualna i zvučna upozorenja unutar otvorene aplikacije, uz jasno definirana ograničenja.

---

# 17. KORISNIČKO SUČELJE

## 17.1. Operativni ekran zaposlenika

Glavni ekran prikazuje:

- Naziv trenutačne lokacije.
- Grupe rekvizita.
- Rekvizite unutar odabrane grupe.
- Status svakog rekvizita.
- Preostalo vrijeme aktivnih najmova.
- Jasne oznake isteka i prekoračenja.

Poželjno je da se najam može pokrenuti u dva ili tri jednostavna koraka.

Primjer:

```text
MORLOCK
Lokacija: Plaža A

[ TRAMPOLINI ] [ PEDALINE ] [ SUP ]

Trampolin 1    SLOBODAN
Trampolin 2    12:34 preostalo
Trampolin 3    SLOBODAN
Trampolin 4    ISTEKLO

Odabir: Trampolin 3

15 min      5 €
30 min      8 €
60 min     14 €

[ POKRENI NAJAM ]
```

Ovo je konceptualni prikaz, a ne konačni dizajn.

## 17.2. Administracijski ekran vlasnika

Treba omogućiti:

- Pregled svih lokacija.
- Pregled trenutačnih najmova.
- Pregled evidentiranog prometa.
- Upravljanje zaposlenicima.
- Upravljanje licencama.
- Dodjelu lokacija zaposlenicima.
- Upravljanje grupama i rekvizitima.
- Upravljanje cjenicima.
- Postavljanje Grace In i Grace Out.

---

# 18. MONETIZACIJA

**DEFINIRANO**

Morlock se monetizira prodajom vremenski ograničenih zaposleničkih licenci.

Licence su u vlasništvu organizacije i prenosive su između zaposlenika.

## 18.1. Poslovne prednosti

- Jednostavno razumljiv model naplate.
- Vlasnik plaća za operativne korisnike.
- Sezonski zaposlenici mogu se mijenjati bez gubitka licence.
- Licenca nije vezana za pojedinu lokaciju.
- Jedan zaposlenik može raditi na više dopuštenih lokacija.
- Broj lokacija ne mora automatski povećavati broj licenci.

## 18.2. Cijene

**OTVORENO**

Razmatrane su ilustrativne cijene od nekoliko eura mjesečno po zaposleniku.

Nijedna cijena nije konačno prihvaćena.

Prije određivanja cijene potrebno je provjeriti:

- Spremnost korisnika na plaćanje.
- Troškove hostinga.
- Troškove korisničke podrške.
- Sezonalnost.
- Konkurentske proizvode.
- Troškove distribucije i prodaje.

---

# 19. BREND I MARKETING

## 19.1. Naziv

**DEFINIRANO**

Naziv aplikacije je:

**MORLOCK**

Inspiracija dolazi iz romana *Vremenski stroj* H. G. Wellsa.

Morlocki su bića koja u romanu žive pod zemljom i upravljaju strojevima.

Naziv je odabran kao prepoznatljiv brend, a ne kao doslovni opis aplikacije.

## 19.2. Slogani

Razmatrani su:

- **Time is our business.**
- **Rental Time Machine.**

Radna preporuka:

**MORLOCK — Rental Time Machine**

Dodatni opis:

**Smart Timers for Equipment Rentals.**

Marketinška poruka:

**No bookings. Just rentals.**

Slogani nisu konačno potvrđeni.

## 19.3. SEO i ASO

Slogan sam po sebi nije dovoljan za dobro rangiranje.

Za web i trgovine aplikacijama treba koristiti opisne izraze povezane s namjenom proizvoda.

Potencijalne ključne riječi za istraživanje:

- rental timer app
- equipment rental management software
- timed rental software
- beach rental management
- water sports rental software
- rental tracking app
- rental staff management

Predloženi naslov web stranice:

**Morlock – Rental Timer & Equipment Rental Management Software**

Primjer opisa:

*Manage timed rentals, equipment availability, staff access and revenue across multiple locations. No booking system required.*

Prije lansiranja treba provjeriti dostupnost domene, naziva i žigova.

---

# 20. KONKURENCIJA I POZICIONIRANJE

Morlock ne treba predstavljati kao proizvod koji nema nikakvu konkurenciju.

Postoje sustavi za upravljanje najmom opreme, plažama i rekreacijskim sadržajima.

Razlika koju Morlock želi naglasiti jest:

**Jednostavno upravljanje neposrednim vremenskim najmom bez rezervacijskog sustava.**

Glavne vrijednosti:

1. Brz početak najma.
2. Jednostavno praćenje vremena.
3. Jasna raspoloživost rekvizita.
4. Centralizirano upravljanje lokacijama.
5. Interni cjenici.
6. Evidencija prometa.
7. Fleksibilno licenciranje zaposlenika.

Ne treba kopirati kompleksnost velikih booking platformi.

---

# 21. ŠTO NE ULAZI U POČETNI MVP

Bez dodatnog odobrenja ne implementirati:

- Online rezervacije.
- Registraciju gostiju.
- Aplikaciju za goste.
- Online plaćanja.
- Fiskalizaciju.
- Automatsko izdavanje računa.
- Kompleksne promocije i popuste.
- Dinamičko određivanje cijena.
- Obračun po minuti.
- AI asistente.
- Automatsku analizu potražnje.
- Sustav ocjenjivanja.
- Marketplace iznajmljivača.
- Napredne integracije s vanjskim servisima.

Također ne uvoditi nove funkcionalnosti samo zato što se čine korisnima.

Prvo treba napraviti kvalitetan osnovni sustav.

---

# 22. FUNKCIONALNOSTI ZA KASNIJE RAZMATRANJE

**PREDLOŽENO, NIJE DOGOVORENO**

Moguće buduće funkcionalnosti:

- Produženje aktivnog najma.
- Evidencija razloga prijevremenog završetka.
- Privremena nedostupnost rekvizita zbog održavanja.
- Napredni izvještaji.
- Pregled iskorištenosti pojedinih rekvizita.
- Dodatne zaposleničke uloge.
- Offline rad.
- Push obavijesti.
- Višejezičnost.
- Više valuta.
- Izvoz izvještaja.
- Povezivanje s vanjskim sustavima.

Svaku funkcionalnost treba uvoditi tek kada postoji opravdana potreba.

---

# 23. KRITIČNI SCENARIJI ZA TESTIRANJE

Prije lansiranja treba provjeriti najmanje sljedeće scenarije.

### Scenarij 1 – Normalan najam

Zaposlenik pokreće najam, vrijeme prolazi, aplikacija upozorava na istek i zaposlenik završava najam.

### Scenarij 2 – Zatvaranje aplikacije

Zaposlenik pokreće najam i zatvara aplikaciju.

Nakon ponovnog otvaranja mora vidjeti točno preostalo vrijeme ili odgovarajući status isteka.

### Scenarij 3 – Istek dok je aplikacija zatvorena

Najam istječe dok aplikacija nije otvorena.

Nakon povratka zaposlenika sustav mora prikazati stvarno stanje.

### Scenarij 4 – Dva zaposlenika

Dva zaposlenika istodobno pokušavaju pokrenuti najam istog rekvizita.

Samo jedan pokušaj smije uspjeti.

### Scenarij 5 – Promjena cjenika

Vlasnik promijeni cijenu paketa.

Povijesni najmovi moraju zadržati stare cijene.

### Scenarij 6 – Promjena Grace intervala

Vlasnik promijeni Grace In ili Grace Out.

Novi najmovi koriste nove vrijednosti, a postojeći zadržavaju stare.

### Scenarij 7 – Oduzimanje licence

Vlasnik oduzima licencu zaposleniku.

Zaposlenik više ne smije izvršavati operativne radnje.

### Scenarij 8 – Prijenos licence

Licenca se oduzima jednom zaposleniku i dodjeljuje drugom.

Datum isteka ostaje nepromijenjen.

### Scenarij 9 – Promjena lokacije

Zaposlenik napušta jednu lokaciju i prijavljuje se na drugu dopuštenu lokaciju.

Ne smiju ostati dvije aktivne radne sesije.

### Scenarij 10 – Istek Grace Out

Rekvizit ostaje zauzet i nakon isteka Grace Out sve dok zaposlenik ne potvrdi završetak najma.

### Scenarij 11 – Netočan sat uređaja

Mobilni uređaj ima netočno postavljen sat.

Prikaz timera mora ostati dovoljno pouzdan zahvaljujući usklađivanju sa serverskim vremenom.

### Scenarij 12 – Izolacija organizacija

Korisnik jedne organizacije ne smije moći dohvatiti ili mijenjati podatke druge organizacije.

---

# 24. OTVORENA PITANJA

Sljedeće odluke još nisu donesene:

1. Točan sustav registracije i autentifikacije.
2. Način kupnje i obnove Morlock licenci.
3. Konačne cijene licenci.
4. Precizna pravila istodobnih prijava i uređaja.
5. Pravila za ispravljanje pogrešno pokrenutih najmova.
6. Hoće li se u MVP-u podržavati produženje najma.
7. Hoće li se moći privremeno blokirati neispravan rekvizit.
8. Hoće li se evidentirati potvrda da je gost platio.
9. Mehanizam pouzdanih obavijesti na zaključanom telefonu.
10. Podrška za offline rad.
11. Konačna shema baze.
12. Hosting i produkcijska infrastruktura.
13. Konačan vizualni identitet.
14. Pravila arhiviranja i zadržavanja podataka.
15. Točne funkcionalnosti administracijskih izvještaja.

Ove odluke treba donositi postupno, tijekom projektiranja.

---

# 25. PREPORUČENI REDOSLIJED RAZVOJA

## Faza 1 – Osnovni podatkovni model

Projektirati:

- Organizacije.
- Korisnike.
- Lokacije.
- Grupe rekvizita.
- Rekvizite.
- Cjenike.
- Najmove.

## Faza 2 – Operativni prototip

Omogućiti:

- Prikaz rekvizita.
- Odabir paketa.
- Pokretanje najma.
- Frontend timere.
- Završetak najma.
- Ponovno učitavanje aktivnih najmova iz baze.

## Faza 3 – Višekorisnički rad

Dodati:

- Autentifikaciju.
- Prava pristupa lokacijama.
- Sinkronizaciju između zaposlenika.
- Sprječavanje dvostrukih najmova.

## Faza 4 – Licenciranje

Dodati:

- Evidenciju kupljenih licenci.
- Dodjelu licenci.
- Prijenos licenci.
- Kontrolu isteka.
- Onemogućavanje pristupa bez licence.

## Faza 5 – Administracija

Dodati:

- Upravljanje zaposlenicima.
- Upravljanje lokacijama i rekvizitima.
- Cjenike.
- Grace intervale.
- Pregled aktivnih najmova.
- Pregled evidentiranog prometa.

## Faza 6 – Produkcijska priprema

Provjeriti:

- Sigurnost.
- Performanse.
- Mobilnu upotrebljivost.
- Pouzdanost obavijesti.
- Ponašanje pri prekidu veze.
- Integritet podataka.
- Backup i oporavak.
- Licenciranje i naplatu pretplate.

Ovo je predloženi redoslijed, a ne obvezujući plan.

---

# 26. GLAVNA RAZVOJNA FILOZOFIJA

Morlock treba biti:

**Jednostavan za razumjeti.**

Zaposlenik mora znati koristiti aplikaciju bez opsežne edukacije.

**Brz u svakodnevnom radu.**

Pokretanje najma mora zahtijevati minimalan broj dodira.

**Pouzdan.**

Najmovi i vremenske oznake ne smiju se izgubiti zatvaranjem aplikacije.

**Precizan.**

Svi timeri moraju biti izvedeni iz trajno spremljenih vremenskih oznaka.

**Fleksibilan.**

Vlasnik može mijenjati cjenike, Grace intervale, zaposlenike i njihove lokacije.

**Komercijalno jednostavan.**

Licence pripadaju vlasniku i mogu se prenositi među zaposlenicima.

**Generički.**

Aplikacija ne smije biti vezana samo za jednu vrstu rekvizita ili djelatnosti.

**Minimalistički.**

Ne dodavati nepotrebne mogućnosti koje otežavaju razvoj i korištenje.

---

# 27. ZAVRŠNA UPUTA ZA CODEX

Morlock je samostalan komercijalni softverski proizvod.

Nemoj ga automatski povezivati s drugim razvojnim projektima ili platformama autora.

Prije početka implementacije:

1. Analiziraj ovaj dokument.
2. Izdvoji definirane zahtjeve.
3. Izdvoji otvorena pitanja koja stvarno blokiraju implementaciju.
4. Predloži minimalnu arhitekturu.
5. Predloži model MySQL/MariaDB baze podataka.
6. Predloži strukturu PHP backenda i frontend aplikacije.
7. Razdvoji MVP od budućih mogućnosti.
8. Nemoj pisati programski kod dok arhitektura i opseg nisu potvrđeni.

**Glavni cilj nije izraditi najveći mogući sustav za najam, nego najjednostavniji pouzdan sustav za upravljanje vremenskim najmom koji će vlasnici stvarno željeti koristiti i plaćati.**
