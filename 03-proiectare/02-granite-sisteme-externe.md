# Granițele cu sistemele externe

Sistemul interacționează cu trei sisteme externe, identificate în
[../01-problema/02-limitele-sistemului.md](../01-problema/02-limitele-sistemului.md): Motorul OCR,
SAGA și Serviciul de email. Nu controlăm funcționarea lor internă; stabilim exact ce schimbăm cu
fiecare și cum se comportă sistemul nostru când granița eșuează.

## Sinteză

| Sistem extern | Componentă responsabilă | Direcția schimbului | Etichetă |
|---------------|-------------------------|---------------------|----------|
| Motorul OCR | `C-03: Adaptor OCR` | Cerere + răspuns cu progres | `Stabilit` (`Ipoteză` pentru `I-06`, `I-08`, `I-09`) |
| SAGA | `C-06: Export Contabil (B2B)` | Unidirecțional, fișier static prin contabil | `Ipoteză` (`I-01`–`I-03`, `CF-10`) |
| Serviciul de email | `C-01: Acces și Conturi` (în afara nucleului) | Unidirecțional, livrare coduri | `Stabilit` (`CF-11`, `CN-05`, `CN-06`) |

## 1. Motorul OCR (prin `C-03`)

### Contractul de schimb

- **Ce trimitem:** `imaginea-sursă` a documentului — o poză sau prima pagină a unui fișier PDF
  (`CF-01`, `I-06`, `D-03`). Nu trimitem alte documente ale contului și nu trimitem date personale
  inutile.
- **Ce primim:**
  - valorile extrase ale antetului: `magazin`, `data`, `ora`, `total`, `plata`;
  - lista `linii`, fiecare cu `denumire`, `suma` și `categorie_propusa`;
  - pentru fiecare valoare citită, `siguranta` în intervalul `[0, 1]` (`CF-02`);
  - stadiul de avansare pe cele 4 etape fixe, în ordine (`CF-03`):
    1. încărcarea;
    2. citirea;
    3. găsirea magazinului, a datei și a totalului;
    4. extragerea produselor (liniilor).
- **Normalizarea la graniță (în `C-03`):**
  - orice valoare citită cu `siguranta < 0,8` primește marcajul `de verificat`; la `siguranta >= 0,8`
    nu primește marcaj (`RD-03`, `I-08`, `ED-04`);
  - `valoarea curentă` pornește egală cu `valoarea citită`, iar ambele sunt păstrate separat (`D-04`);
  - dacă `categorie_propusa` lipsește sau nu face parte din cele 9 categorii, `C-03` atribuie
    categoria implicită `Altele` (`RD-06`). Până la închiderea întrebării `QD-07`, categoria propusă
    nu primește marcajul `de verificat`.
  - siguranța mare nu este tratată ca o garanție de corectitudine (`P-03`); potrivirea dintre
    `totalul documentului` și `suma liniilor` rămâne verificată ulterior de `C-04` (`RD-04`).

### Tratarea eșecurilor

| Situație de eșec | Cum o detectăm | Cum reacționează sistemul |
|------------------|----------------|---------------------------|
| Timpul de citire depășește limita stabilită (`I-09`) | `C-03` oprește așteptarea la timeout | Documentul trece din `În procesare` în `Eroare` (`TR-04`). `Imaginea-sursă` rămâne păstrată (`D-03`, `INV-06`). Utilizatorul vede un mesaj clar și butonul de reîncercare (`CF-03`, `CN-03`, `CN-06`). |
| Motorul OCR este oprit sau întoarce eroare tehnică (`EA-04`) | `C-03` primește eroare sau lipsă de răspuns | Același comportament: trecere în `Eroare`, fără afectarea evidenței (`INV-05`), cu posibilitate de reîncercare (`TR-05`) fără a reîncărca poza. |
| Document ilizibil sau răspuns gol / malformat | `C-03` nu poate extrage structura minimă | Documentul trece în `Eroare` (`TR-04`). Utilizatorul află că documentul nu a putut fi citit și poate reîncerca sau încărca altă poză (`EA-04`, `CN-06`). |
| Răspuns tardiv după trecerea în `Eroare` sau ștergere | `C-02` verifică starea curentă a documentului | Răspunsul sosit când documentul nu mai este în `În procesare` este ignorat, pentru a nu suprascrie starea curentă (`OP-02`). |

## 2. SAGA (prin `C-06`, B2B, `Ipoteză` `I-01`)

### Contractul de schimb

- **Modul de integrare:** graniță prin fișier static, descărcat din sistem și importat manual de
  contabil în SAGA (`I-01`). Sistemul nu apelează SAGA și nu primește confirmare automată de import.
- **Ce conține fișierul:**
  - exact documentele în starea `Confirmat` ale contului de firmă care au `data documentului` în
    luna calendaristică cerută, după fusul orar al utilizatorului (`RD-08`, `RD-12`, `EA-05`);
  - niciun document personal, niciun document neconfirmat și niciun document din altă lună (`INV-02`,
    `INV-05`);
  - toate sumele exprimate în lei, cu cel mult 2 zecimale (`I-07`, `RD-10`);
  - structură de fișier text (CSV/XML, `Propunere AI`: `DP-04`), schema exactă urmând să fie validată
    față de documentația SAGA (`Q-04`).
- **Imuabilitate și trasabilitate:**
  - fiecare generare creează un `Export` identificat prin contul de firmă, lună și momentul
    generării, al cărui conținut nu se mai schimbă după generare (`D-09`, `INV-06`, `ED-08`);
  - documentele incluse primesc marcajul `exportat în {lună}` (`P-01`, `DP-03`).

### Tratarea eșecurilor și a situațiilor limită

| Situație | Cum reacționează sistemul |
|----------|---------------------------|
| Nu există niciun document `Confirmat` al firmei în luna cerută | `C-06` nu generează un fișier gol (`OP-06`) și informează clar utilizatorul că luna nu are documente confirmate de exportat (`CN-06`). |
| Un document deja exportat este corectat ulterior (`Q-03`) | Fișierul de export vechi rămâne neschimbat (`INV-06`), iar documentul primește marcajul `modificat după export` (`P-01`, `DP-03`) pentru ca diferența să fie vizibilă și contabilul să poată primi un export actualizat. |
| Un document deja exportat este șters sau apare un document nou cu data în luna deja exportată (`ED-06`, `ED-08`) | Exportul anterior nu se modifică (`INV-06`); un export generat ulterior pentru aceeași lună este un `Export` nou, cu un moment al generării mai recent, care reflectă evidența curentă (`D-09`). |
| SAGA respinge fișierul sau contabilul importă același fișier de două ori | Deoarece SAGA nu ne răspunde (`I-01`), sistemul nu poate detecta automat importul. Riscul de format se reduce prin verificarea schemei SAGA (`Q-04`), iar riscul de dublare prin identificarea clară a fiecărui export cu luna și momentul generării (`D-09`). |

## 3. Serviciul de email (prin `C-01`, în afara nucleului)

### Contractul de schimb

- **Ce trimitem:** cereri de expediere email pentru două situații (`CF-11`):
  1. cod de unică folosință pentru confirmarea adresei de email la crearea contului (`RD-13`);
  2. cod de unică folosință pentru resetarea parolei.
- **Ce controlăm la graniță (în `C-01`):**
  - textul mesajului în limba aplicației (`CN-06`) și durata de valabilitate a codului;
  - stocarea ireversibilă a codurilor și a parolelor (`CN-05`);
  - răspuns neutru la cererea de resetare a parolei, astfel încât nimeni să nu poată afla dacă o
    adresă de email are sau nu cont (`CN-05`);
  - limitarea încercărilor repetate de autentificare sau introducere de cod (`CN-05`).

### Tratarea eșecurilor

| Situație de eșec | Cum reacționează sistemul |
|------------------|---------------------------|
| Serviciul de email este indisponibil sau mesajul întârzie | `C-01` afișează un mesaj clar în limba aplicației și oferă posibilitatea de retrimitere a unui cod nou (`CN-06`). Codul anterior este invalidat la emiterea unuia nou. |
| Codul a expirat sau a fost introdus greșit | Accesul rămâne blocat (`RD-13`, `CN-05`), iar utilizatorul este ghidat să ceară un cod nou (`CN-06`). |
| Eroare la livrarea emailului în timp ce alți utilizatori lucrează în nucleu | Eșecul rămâne izolat în `C-01` și nu afectează încărcarea, verificarea, evidența sau raportarea utilizatorilor deja autentificați. |

