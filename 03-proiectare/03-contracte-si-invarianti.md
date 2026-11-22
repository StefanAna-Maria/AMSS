# Contracte de operații și invarianți

Invarianții definesc condițiile care trebuie să rămână adevărate înainte și după orice operație
finalizată a sistemului. Contractele stabilesc, pentru fiecare operație principală, cine o poate
apela, ce trebuie să fie adevărat înainte (precondiții), ce se garantează după (postcondiții) și cum
se tratează eșecurile.

## Invarianții sistemului (`INV-01`–`INV-06`)

| ID | Invariant | Surse și etichetă | Componente care îl păzesc |
|----|-----------|-------------------|---------------------------|
| `INV-01` | Un document aparține exact unui cont (personal sau de firmă), stabilit la creare și nemodificabil. | `RD-01`, `REL-03`, `D-01` (`Stabilit`; „nemodificabil” este `Propunere AI`) | `C-02`, `C-04` |
| `INV-02` | **Izolarea între conturi:** nicio operație nu citește, modifică sau șterge documente ori exporturi din alt cont decât contul personal al utilizatorului sau contul firmei în care acesta este membru. Un document din alt cont se comportă ca și cum nu ar exista. | `RD-02`, `CN-01`, `I-04` (`Stabilit` pentru personal, `Ipoteză` pentru firmă) | `C-01` (verificare), `C-02`, `C-04`, `C-05`, `C-06` (aplicare) |
| `INV-03` | Orice document în starea `Confirmat` are zero câmpuri cu marcajul `de verificat` și respectă `totalul documentului == suma liniilor` la ban, fără toleranță. | `RD-04`, `RD-05`, `I-10` (`Stabilit`; „la ban” este `Ipoteză`) | `C-04` |
| `INV-04` | Fiecare linie a unui document confirmat (și orice sumă introdusă manual) are sumă `> 0` cu cel mult 2 zecimale și exact una dintre cele 9 categorii; `data documentului <= azi` (după fusul orar al utilizatorului). | `RD-06`, `RD-10`, `I-07`, `CN-02` (`Stabilit`; `> 0` pentru toate liniile depinde de `QD-02`) | `C-04`, `C-03` (implicit `Altele`) |
| `INV-05` | Evidența unui cont conține exclusiv documente în starea `Confirmat`. Pentru orice cont și orice lună calendaristică (după `data documentului`), suma totalurilor documentelor din evidență este egală la ban cu suma totalurilor pe cele 9 categorii. | `RD-07`, `RD-08`, `RD-09`, `I-05` (`Ipoteză` pentru evidență, `Stabilit` pentru egalitatea sumelor) | `C-04`, `C-05` |
| `INV-06` | `Imaginea-sursă` a unui document scanat și conținutul unui `Export` deja generat sunt imuabile: odată create, nu se mai modifică (decât prin ștergerea definitivă a documentului, în cazul imaginii-sursă). | `D-03`, `D-09`, `RD-11` (`Propunere AI`) | `C-02` (`imaginea-sursă`), `C-06` (`Export`) |

> **Observație privind `INV-05`:** Așa cum arată analiza domeniului
> ([../02-domeniu/03-regulile-domeniului.md](../02-domeniu/03-regulile-domeniului.md)), egalitatea
> dintre totalul lunii și suma totalurilor pe cele 9 categorii decurge direct din `INV-03` și
> `INV-04`. O formulăm separat ca invariant de verificat în Faza 4, inclusiv pentru a măsura impactul
> schimbării `S-01`.

## Contractele operațiilor (`OP-01`–`OP-06`)

### `OP-01`: Încărcarea unui document scanat

- **Componentă responsabilă:** `C-02: Preluare și Flux Document` (folosește `C-01`).
- **Cine apelează:** Utilizator autentificat (B2C pentru contul personal sau membru B2B pentru contul
  firmei).
- **Date de intrare:** `cont_id`, `tip_document` (`bon`, `factură` sau `chitanță`, `D-11`),
  `fișier` (poză sau PDF, `CF-01`), `cheie_idempotenta` (`CN-04`).
- **Precondiții:**
  1. Utilizatorul are adresa de email confirmată (`RD-13`) și drept de acces în `cont_id` verificat
     prin `C-01` (`INV-02`).
  2. Fișierul este într-un format acceptat (imagine sau PDF, `CF-01`).
- **Postcondiții:**
  1. Dacă `cheie_idempotenta` a mai produs deja un document în același `cont_id`, operația întoarce
     documentul existent fără a crea un al doilea document (`CN-04`).
  2. Altfel, se creează un document cu identificator nou (`D-02`), asociat definitiv cu `cont_id`
     (`INV-01`) și cu utilizatorul care l-a încărcat (`REL-08`), cu `imaginea-sursă` atașată imuabil
     (`D-03`, `INV-06`), în starea `Încărcat` (`TR-01`), în afara evidenței (`INV-05`, `DP-01`).
- **Caz de eșec:**
  - Lipsă acces în `cont_id`: cererea este respinsă fără a dezvălui existența contului (`INV-02`).
  - Format de fișier neacceptat sau corupt: nu se creează niciun document; utilizatorul primește un
    mesaj clar despre ce formate poate încărca (`CN-06`).
  - Indisponibilitate temporară a serverului: nu se modifică evidența, iar utilizatorul poate
    retrimite cu aceeași `cheie_idempotenta` (`CN-03`, `CN-04`).

### `OP-02`: Procesarea răspunsului OCR

- **Componentă responsabilă:** `C-02: Preluare și Flux Document` + `C-03: Adaptor OCR`.
- **Cine apelează:** Fluxul intern al `C-02`, după trimiterea `imaginii-sursă` către `C-03`
  (`TR-02` sau reîncercarea `TR-05`).
- **Date de intrare:** `document_id`, rezultatul normalizat din `C-03` (valorile extrase, siguranțele
  în `[0, 1]`, cele 4 etape de progres `CF-03`) sau semnalul de eșec/timeout (`I-09`).
- **Precondiții:**
  1. Documentul există și se află în starea `În procesare`.
  2. Documentul are `imaginea-sursă` atașată (`REL-04`).
- **Postcondiții:**
  - **La succes:**
    1. Pentru fiecare valoare citită (antet și linii) se păstrează `valoarea citită` și `siguranta`,
       iar `valoarea curentă` este inițializată cu `valoarea citită` (`D-04`).
    2. Valorile cu `siguranta < 0,8` primesc marcajul `de verificat`; valorile cu `siguranta >= 0,8`
       nu primesc marcaj (`RD-03`, `I-08`, `ED-04`).
    3. Orice linie fără categorie validă primește categoria implicită `Altele` (`RD-06`).
    4. Se calculează `suma liniilor` și `diferența = totalul documentului - suma liniilor` (`CF-05`).
    5. Documentul trece în starea `De verificat` (`TR-03`) și rămâne în afara evidenței (`INV-05`).
  - **La eșec (timeout `I-09`, serviciu indisponibil sau document ilizibil):**
    1. Documentul trece în starea `Eroare` (`TR-04`).
    2. `Imaginea-sursă` rămâne păstrată imuabil (`INV-06`) pentru reîncercare ulterioară (`CN-03`,
       `EA-04`).
    3. Evidența și totalurile contului rămân neschimbate (`INV-05`).
- **Caz de eșec:**
  - Documentul nu se mai află în `În procesare` (de ex. răspuns sosit după timeout): rezultatul
    întârziat este ignorat, fără a altera starea curentă a documentului.
  - Răspuns malformat din Motorul OCR: `C-03` îl transformă în eșec, iar documentul trece în `Eroare`
    cu `imaginea-sursă` păstrată.

### `OP-03`: Corectarea unui document

- **Componentă responsabilă:** `C-02` (când documentul este în `De verificat`) sau `C-04` (când
  documentul este în `Confirmat`), cu verificare de acces prin `C-01`.
- **Cine apelează:** Utilizator autentificat cu acces în contul documentului (`INV-02`).
- **Date de intrare:** `document_id`, modificările propuse asupra valorilor curente (magazin, dată,
  oră, total, plată, notă, tip document, linii — modificare, adăugare sau eliminare de linii) și/sau
  lista câmpurilor marcate `de verificat` pe care utilizatorul le acceptă fără schimbare (`P-04`).
- **Precondiții:**
  1. Utilizatorul are acces în contul documentului (`C-01`, `INV-02`).
  2. Documentul se află în starea `De verificat` sau `Confirmat`.
  3. Fiecare sumă modificată sau adăugată respectă `RD-10` (`> 0`, cel mult 2 zecimale), categoria
     este una dintre cele 9 (`RD-06`), iar `data documentului <= azi` (`RD-10`, `INV-04`).
- **Postcondiții:**
  1. Pentru fiecare câmp scanat modificat: `valoarea citită` și `siguranta` rămân neschimbate
     (`D-04`), `valoarea curentă` devine noua valoare, iar marcajul devine `corectat` (`CF-04`,
     `ED-03`).
  2. Pentru fiecare câmp `de verificat` acceptat fără modificare: `valoarea curentă` rămâne egală cu
     `valoarea citită`, iar marcajul devine `confirmat` (`P-04`, `Q-07`).
  3. `Imaginea-sursă` rămâne nemodificată (`INV-06`).
  4. **Dacă documentul era `De verificat`:** rămâne în `De verificat` (`TR-06`), iar `suma liniilor`
     și `diferența` sunt recalculate (`CF-05`).
  5. **Dacă documentul era `Confirmat`:** modificările sunt acceptate atomic doar dacă `INV-03`
     (zero marcaje `de verificat` și `totalul documentului == suma liniilor` la ban) și `INV-04`
     (inclusiv cel puțin o linie, `QD-04`) rămân adevărate (`DP-02`, `TR-08`). Totalurile lunii
     (eventual ale ambelor luni, dacă s-a schimbat `data documentului`, `RD-08`) și sumele pe
     categorii se actualizează păstrând `INV-05` (`ED-05`). Dacă documentul avea marcajul
     `exportat în {lună}`, primește marcajul `modificat după export` (`P-01`, `DP-03`), fără a
     schimba conținutul exportului deja generat (`INV-06`).
- **Caz de eșec:**
  - Lipsă acces în cont: documentul se comportă ca și cum nu ar exista (`INV-02`).
  - Document aflat în `Încărcat`, `În procesare` sau `Eroare`: corectarea este respinsă.
  - Valori invalide (sumă `<= 0`, mai mult de 2 zecimale, dată din viitor, categorie invalidă):
    respinse conform `INV-04`, fără modificarea documentului.
  - Pentru un document `Confirmat`, modificarea încalcă `INV-03` (ex. lasă o diferență între total și
    suma liniilor): întreaga operație este respinsă atomic (`DP-02`), documentul rămâne `Confirmat`
    cu valorile vechi, iar utilizatorul vede diferența de corectat (`CN-06`).

### `OP-04`: Confirmarea unui document

- **Componentă responsabilă:** `C-02` → `C-04` (cu verificare de acces prin `C-01`).
- **Cine apelează:** Utilizator autentificat cu acces în contul documentului (`INV-02`).
- **Date de intrare:** `document_id`.
- **Precondiții:**
  1. Utilizatorul are acces în contul documentului (`C-01`, `INV-02`).
  2. Documentul se află în starea `De verificat`.
  3. Documentul are zero câmpuri cu marcajul `de verificat` (`RD-05`, `EA-02`).
  4. Documentul are cel puțin o linie (ipoteza de lucru `QD-04`), iar toate liniile și
     `data documentului` respectă `INV-04`.
  5. `totalul documentului == suma liniilor` la ban (`RD-04`, `I-10`, `EA-03`, `INV-03`).
- **Postcondiții:**
  1. Documentul trece din `De verificat` în `Confirmat` (`TR-07`) și intră în evidența contului în
     `C-04` (`INV-05`, `EA-01`).
  2. Totalul lunii corespunzătoare `datei documentului` și sumele pe categorii includ documentul
     (`RD-08`, `RD-09`, `ED-06`).
  3. `C-04` verifică dacă există deja în același cont un alt document `Confirmat` cu același
     `magazin`, aceeași `data documentului` și același `total`; dacă există, întoarce un avertisment
     de posibil duplicat fără a bloca confirmarea (`P-02`, `DP-05`, `ED-01`).
- **Caz de eșec:**
  - Lipsă acces în cont (`INV-02`) sau stare diferită de `De verificat` (ex. `Încărcat`,
    `În procesare`, `Eroare`): confirmarea este respinsă.
  - Există cel puțin un câmp cu marcajul `de verificat`: confirmarea este blocată și se indică
    câmpurile rămase de verificat (`EA-02`).
  - `totalul documentului != suma liniilor`: confirmarea este blocată și se afișează diferența exactă
    (`CF-05`, `EA-03`).
  - Lipsă linii sau valori care încalcă `INV-04`: confirmarea este respinsă cu mesaj explicativ
    (`CN-06`).

### `OP-05`: Ștergerea unui document

- **Componentă responsabilă:** `C-02` (pentru documente neconfirmate) sau `C-04` (pentru documente
  confirmate), cu verificare de acces prin `C-01`.
- **Cine apelează:** Utilizator autentificat cu acces în contul documentului (`INV-02`).
- **Date de intrare:** `document_id`, `confirmare_explicita = da` (`RD-11`, `CF-09`).
- **Precondiții:**
  1. Utilizatorul are acces în contul documentului (`C-01`, `INV-02`).
  2. Utilizatorul a confirmat explicit ștergerea (`RD-11`).
  3. Documentul se află în una dintre stările `Încărcat`, `De verificat`, `Confirmat` sau `Eroare`
     (nu este în `În procesare`).
- **Postcondiții:**
  1. Documentul, toate liniile lui și `imaginea-sursă` asociată sunt șterse definitiv (`TR-10`,
     `RD-11`).
  2. Dacă documentul era în starea `Confirmat`, el dispare din evidență, iar totalurile lunii și
     sumele pe categorii se recalculează păstrând `INV-05` (`CF-09`).
  3. Dacă documentul fusese inclus într-un `Export` anterior, conținutul exportului deja generat
     rămâne nemodificat (`INV-06`), iar lipsa documentului față de exportul anterior este semnalată
     (`DP-03`).
- **Caz de eșec:**
  - Lipsă acces în cont (`INV-02`) sau lipsa confirmării explicite (`RD-11`): ștergerea este respinsă.
  - Documentul se află în `În procesare`: ștergerea este respinsă pentru a evita conflicte cu
    răspunsul OCR aflat în curs; utilizatorul este informat să aștepte finalizarea sau eșecul citirii
    (`CN-06`).

### `OP-06`: Generarea exportului contabil B2B

- **Componentă responsabilă:** `C-06: Export Contabil (B2B)` (folosește `C-01` și `C-04`).
- **Cine apelează:** Orice membru autentificat al contului de firmă (`I-04`, `DP-04`, răspuns propus
  la `Q-05`).
- **Date de intrare:** `cont_firma_id`, `luna` (an și lună calendaristică).
- **Precondiții:**
  1. Utilizatorul are emailul confirmat (`RD-13`) și este membru în `cont_firma_id` (`C-01`,
     `INV-02`).
  2. Contul este de tip firmă (`I-03`).
  3. Există cel puțin un document în starea `Confirmat` al firmei cu `data documentului` în `luna`
     cerută (`RD-08`, `RD-12`).
- **Postcondiții:**
  1. Se creează un nou `Export` cu `cont_firma_id`, `luna` și `momentul generării` curent (`D-09`),
     cuprinzând exact documentele `Confirmat` ale firmei din acea lună (`EA-05`), în format text
     structurat CSV/XML pentru import în SAGA (`DP-04`, `I-01`), cu sume în lei cu cel mult 2
     zecimale (`I-07`).
  2. Conținutul exportului generat este imuabil (`INV-06`, `ED-08`).
  3. Fiecare document inclus primește marcajul `exportat în {lună}` (`P-01`, `DP-03`).
- **Caz de eșec:**
  - Lipsă acces în cont (`INV-02`): contul se comportă ca inexistent.
  - Cont personal (B2C): operația este respinsă (`I-03`).
  - Zero documente `Confirmat` ale firmei în luna cerută: nu se generează un fișier gol; utilizatorul
    primește un mesaj clar (`CN-06`).

> **Notă privind cheltuiala manuală (`CF-13`, `D-07`, `TR-09`):** Adăugarea unei cheltuieli manuale
> intră direct în `C-04` (fără a trece prin `C-02` sau `C-03`), cu verificare de acces prin `C-01`,
> suport pentru `cheie_idempotenta` (`CN-04`) și validare conform `INV-04` (o singură linie cu sumă
> `> 0`, cel mult 2 zecimale, categorie din cele 9, `data documentului <= azi`, fără oră și fără
> `imagine-sursă`, `ED-07`). Deoarece `totalul documentului` este egal cu suma singurei linii și nu
> există marcaje OCR, `INV-03` este îndeplinit automat la intrarea în evidență.

