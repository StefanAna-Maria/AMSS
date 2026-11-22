# Decizii de proiectare

Deciziile de mai jos răspund întrebărilor lăsate deschise pentru Faza 3 în
[../01-problema/04-ipoteze-si-intrebari.md](../01-problema/04-ipoteze-si-intrebari.md) și
[../02-domeniu/04-distinctii-si-alternative.md](../02-domeniu/04-distinctii-si-alternative.md):
`Q-01`, `Q-02`, `Q-03`, `Q-04`, `Q-05` și `Q-08`. Toate sunt marcate **`Propunere AI`** până le
discută și le validează echipa.

## Deciziile propuse (`DP-01`–`DP-05`)

| ID | Etichetă | Întrebare rezolvată | Decizia propusă | Alternativa respinsă | Justificare și consecințe |
|----|----------|---------------------|-----------------|----------------------|---------------------------|
| `DP-01` | `Propunere AI` | `Q-01` | Documentele scanate sunt păstrate pe server încă de la încărcare (`Încărcat`, `În procesare`, `De verificat`, `Eroare`), în componenta `C-02`, separat de evidența din `C-04`. | Păstrarea documentelor neconfirmate doar local pe telefon până la confirmare. | Susține `CN-03` (ce a încărcat sau corectat utilizatorul nu se pierde la o întrerupere), `CF-03` (reîncercare din `Eroare` fără reîncărcarea imaginii), `CN-04` (idempotență la încărcare, `OP-01`) și `D-10` (bonul neconfirmat din `EA-05` și `ED-08` există deja în contul firmei). Consecință: sistemul impune strict `INV-05`, ca nicio ciornă din `C-02` să nu intre în rapoarte sau export. |
| `DP-02` | `Propunere AI` | `Q-02` | Corectarea unui document `Confirmat` (`OP-03`, `TR-08`) este validată atomic în `C-04`; dacă strică potrivirea totalului (`INV-03`) sau validitatea liniilor/datei (`INV-04`), modificarea este respinsă și documentul rămâne `Confirmat` cu valorile vechi. | Întoarcerea documentului în `De verificat` la o diferență de sumă, sau recalcularea automată a totalului din linii fără acord explicit. | Evită ieșirea accidentală a unui document confirmat din evidență și oscilațiile din totalurile lunii (`INV-05`, exemplul din [04-stari-si-tranzitii.md](04-stari-si-tranzitii.md)). Spre deosebire de recalcularea automată a totalului, păstrează rolul de control al totalului de pe document (`P-03`, `RD-04`). Consecință: când se modifică o sumă de linie pe un document confirmat, utilizatorul actualizează în aceeași operație și totalul documentului. |
| `DP-03` | `Propunere AI` | `Q-03` | Documentele incluse într-un export primesc marcajul `exportat în {lună}` (`P-01`). La o corectare sau ștergere ulterioară, editarea nu este blocată și exportul deja generat rămâne imuabil (`D-09`, `INV-06`), dar sistemul semnalează diferența (`modificat după export`). | Blocarea definitivă a corectării/ștergerii după export, sau modificarea retroactivă a fișierului de export vechi. | Blocarea ar contrazice `CF-08`/`CF-09` și ar împiedica remedierea unei erori observate după export; alterarea exportului vechi ar încălca `D-09` (`INV-06`), deoarece contabilul are deja fișierul inițial în SAGA (`I-01`). Consecință: firma vede clar ce documente s-au schimbat după export și poate genera un export nou (`ED-08`). |
| `DP-04` | `Propunere AI` | `Q-04`, `Q-05` | Exportul contabil B2B (`OP-06`) se generează la cerere de către orice membru al contului de firmă (aliniat cu `I-04`), în format text structurat CSV/XML pentru import manual în SAGA. | Export automat la final de lună și/sau permis doar administratorului; integrare directă cu SAGA. | Generarea la cerere permite firmei să exporte exact după ce a confirmat bonurile întârziate (`ED-06`, `ED-08`) și să regenereze la nevoie; accesul pentru orice membru nu introduce roluri noi și rămâne consecvent cu `I-04`; fișierul CSV/XML respectă granița unidirecțională `I-01`. Consecință: structura exactă de coloane/câmpuri depinde de documentația SAGA (`Q-04`), iar dacă echipa introduce roluri (căderea `I-04`), `C-01` și precondiția lui `OP-06` se restrâng la administrator. |
| `DP-05` | `Propunere AI` | `Q-08` | La confirmare (`OP-04`), `C-04` verifică existența altui document `Confirmat` în același cont cu același `magazin`, aceeași `data documentului` și același `total`; dacă găsește unul, semnalează un posibil duplicat prin avertisment, fără a bloca confirmarea (`P-02`). | Blocarea automată a confirmării la aceeași combinație `(magazin, dată, total)` sau lipsa oricărei verificări de duplicate. | Blocarea ar respinge achiziții reale identice făcute în aceeași zi (ex. două cafele în aceeași zi, `D-02`), iar lipsa verificării ar lăsa neobservat bonul încărcat de doi colegi (`ED-01`). Consecință: decizia finală rămâne la utilizator, iar identitatea dată de sistem (`D-02`) rămâne neschimbată. |

## Exemple concrete ale impactului deciziilor

- **Pentru `DP-03` (document corectat după export):** În situația din `EA-05` și `ED-08`, firma
  Exemplu SRL a generat exportul pe noiembrie 2026 pe 1 decembrie (`376,18 lei`, 3 documente, toate
  marcate `exportat în 2026-11`). Dacă pe 4 decembrie Ioana corectează categoria sau suma unei linii
  (împreună cu totalul, conform `DP-02`) pe factura de `310,50 lei`, factura rămâne `Confirmat`,
  primește marcajul `modificat după export`, exportul din 1 decembrie rămâne neschimbat la
  `376,18 lei`, iar Ioana știe că trebuie să transmită contabilului un nou export.
- **Pentru `DP-05` (posibil duplicat între colegi):** În scenariul `ED-01`, după ce Radu confirmă în
  contul firmei bonul de `25,68 lei` de la `MINIMARKET LUNA SRL` din `10.11.2026`, când Ioana apasă
  confirmarea pentru același bon (`OP-04`), `C-04` îi afișează avertismentul de posibil duplicat.
  Ioana poate renunța și șterge documentul (`OP-05`) pentru a nu dubla suma la `51,36 lei`, sau poate
  continua dacă au fost cu adevărat două cumpărături identice.

## Ce rămâne deschis pentru Faza 4 (`04-verificare/`)

Următoarele puncte nu sunt închise în Faza 3 și trebuie analizate sau verificate explicit în etapa
următoare:

1. **Verificarea tranzițiilor interzise și a scenariilor de eșec:** construcția de scenarii și
   contraexemple care testează păstrarea `INV-01`–`INV-06` pe cazuri-limită: timeout OCR (`I-09`,
   `TR-04`), răspuns OCR tardiv după `Eroare` (`OP-02`), încercare de ștergere în `În procesare`
   (`OP-05`), retrimitere cu `cheie_idempotenta` (`CN-04`, `OP-01`), acces încrucișat între conturi
   (`INV-02`) și corectare care strică totalul unui document `Confirmat` (`DP-02`).
2. **Impactul schimbării `S-01` asupra proiectării:** dacă se acceptă confirmarea unui document cu
   diferență de total acceptată explicit (`S-01`), se rup `INV-03` și, fără o regulă nouă de alocare
   a diferenței (ex. la `Altele`), și `INV-05` (`RD-09`); se modifică precondițiile lui `OP-04` și
   `OP-03`, structura datelor din `C-04` și conținutul fișierului de export din `C-06` (`OP-06`).
   Comparativ, schimbarea `S-02` (prag `0,9`) rămâne izolată în `C-03`.
3. **Întrebările de domeniu rămase deschise (`QD-01`–`QD-04`, plus `QD-05`–`QD-07`) și formatul SAGA
   (`Q-04`):**
   - `QD-01`: introducerea listei exacte a celor 9 categorii și verificarea corespondenței cu regulile
     RP01–RP04 din documentul de la Scrum;
   - `QD-02`: dacă liniile de reducere cu sumă negativă devin permise, `INV-04` (`sumă > 0`) și
     validarea din `OP-03`/`OP-04` trebuie relaxate pentru liniile de reducere;
   - `QD-03`: dacă la facturi liniile sunt fără TVA și totalul cu TVA, formula din `INV-03` (`RD-04`)
     necesită un caz distinct pentru TVA;
   - `QD-04`: dacă o chitanță poate fi confirmată fără linii, condiția „cel puțin o linie” din `OP-04`
     și `TR-07` trebuie nuanțată pe tipul documentului;
   - `QD-05`–`QD-07` și schema exactă a fișierului SAGA (`Q-04`), de confirmat înainte de orice
     prototip de export.

