# Predarea Fazei 3 către revizuire și verificare

De la Luisa Frincu (Faza 3, proiectarea), către evaluatorul proiectării și către Cristina Simion,
care face verificarea în Faza 4.

## 1. Rolul, întrebarea, ce așteptăm și unde se oprește

- Rolul: evaluator al proiectării sistemului, nu autor.
- Întrebarea: sunt componentele logice (`C-01`–`C-06`), granițele cu sistemele externe, invarianții
  (`INV-01`–`INV-06`), contractele (`OP-01`–`OP-06`), tranzițiile (`TR-01`–`TR-10`) și deciziile
  (`DP-01`–`DP-05`) din `03-proiectare/` coerente cu `01-problema/` și `02-domeniu/` și destul de
  precise ca să poată fi verificate în Faza 4?
- Ce așteptăm: o listă de constatări. Fiecare are fișierul, ID-ul și o propunere de decizie
  (acceptată, respinsă cu motiv sau deschisă, cu pasul următor). Constatările intră în jurnalul din
  `revizuiri/`.
- Unde se oprește: evaluatorul nu rescrie fișierele și nu începe verificarea din Faza 4.

## 2. Fișierele și versiunea

| Fișier | Versiunea |
|--------|-----------|
| `03-proiectare/*.md` | același commit cu acest rezumat (commit-ul `03-proiectare`) |
| `02-domeniu/*.md` | commit-ul `ef9515e` |
| `01-problema/*.md` | commit-ul `2bda01e` |

Evaluatorul primește acest rezumat, fișierele din `03-proiectare/` și sursele din `01-problema/` și
`02-domeniu/`.

## 3. Ce e decis, ce e ipoteză și ce e deschis

- Preluat din Faza 1 și Faza 2, fără modificarea fișierelor sursă: cerințele `CF-01`–`CF-16`,
  `CN-01`–`CN-06`, regulile `R-01`–`R-09`, `RD-01`–`RD-13`, relațiile `REL-01`–`REL-08`, deciziile
  de modelare `D-01`–`D-11` și ipotezele `I-01`–`I-10`.
- Propuneri AI din Faza 3, de discutat în echipă: împărțirea în componente logice (`C-02` și `C-03`
  ca separare de proiectare) și deciziile `DP-01`–`DP-05`, care propun răspunsuri pentru `Q-01`,
  `Q-02`, `Q-03`, `Q-04`, `Q-05` și `Q-08`.
- Ipoteze păstrate ca ipoteze: exportul B2B prin fișier static către SAGA (`I-01`–`I-03`, `C-06`),
  drepturile egale ale membrilor firmei (`I-04`), excluderea neconfirmatelor din evidență (`I-05`),
  prima pagină din PDF (`I-06`), moneda unică lei (`I-07`), pragul fix `0,8` (`I-08`), timeout OCR
  (`I-09`), potrivirea la ban fără toleranță (`I-10`) și idempotența la documente scanate (`CN-04`).
- Rămase deschise pentru echipă și Faza 4:
  - întrebările de domeniu `QD-01`–`QD-04` (cu impact potențial direct asupra `INV-03`, `INV-04`,
    `OP-03`, `OP-04`), plus `QD-05`–`QD-07`;
  - schema exactă de coloane/taguri din documentația SAGA (`Q-04`);
  - analiza detaliată a impactului schimbării `S-01` asupra `INV-03`, `INV-05`, `OP-03`, `OP-04` și
    `OP-06`.

## 4. Constrângeri, scenarii, invarianți și criterii

- Constrângeri: proiectarea rămâne la nivel de componente logice, granițe, contracte, invarianți și
  stări; nu alege tehnologii, baze de date, framework-uri sau clase de implementare.
- Scenarii de referință: `EA-01`–`EA-05` din `01-problema/05-exemple-de-acceptare.md`, `ED-01`–`ED-08`
  din `02-domeniu/04-distinctii-si-alternative.md` și schimbările `S-01`, `S-02` din
  `01-problema/06-schimbarea-unei-cerinte.md`.
- Invarianți formulați: `INV-01`–`INV-06` în `03-proiectare/03-contracte-si-invarianti.md`, păziți
  prin contractele `OP-01`–`OP-06` și prin tranzițiile `TR-01`–`TR-10` (plus tranzițiile interzise)
  din `03-proiectare/04-stari-si-tranzitii.md`.
- Criterii de revizuire:
  1. Graful de dependențe dintre `C-01`–`C-06` nu are cicluri, iar granițele izolează sistemele
     externe (`C-03`, `C-06`, `C-01`) și separă ciorna (`C-02`) de evidență (`C-04`).
  2. Cele trei sisteme externe (Motorul OCR, SAGA, Serviciul de email) au contracte clare și
     acoperă explicit cazurile de eșec fără a corupe evidența.
  3. Fiecare invariant (`INV-01`–`INV-06`) și fiecare contract (`OP-01`–`OP-06`) se leagă trasabil
     de cerințe (`CF`/`CN`), reguli (`RD`) sau decizii marcate `Propunere AI`, fără cerințe inventate.
  4. Diagrama de stări, tabelul `TR-01`–`TR-10`, tranzițiile interzise și contractele `OP-01`–`OP-06`
     nu se contrazic între ele (inclusiv pentru cheltuiala manuală și ștergerea în `În procesare`).
  5. Fiecare decizie `DP-01`–`DP-05` este marcată `Propunere AI`, prezintă o alternativă respinsă și
     explică consecințele fără a tranșa pe tăcute întrebările `QD-01`–`QD-07`.
  6. Nu apar tehnologii, baze de date, framework-uri sau clase de implementare, iar fișierele din
     `01-problema/` și `02-domeniu/` nu au fost modificate.

## 5. Ce am verificat și ce mai e de făcut

- Am verificat: lipsa ciclurilor în graful de dependențe `C-01`–`C-06`, existența tuturor
  identificatorilor referiți din Faza 1 și Faza 2, coerența dintre `OP-01`–`OP-06`, `INV-01`–`INV-06`
  și `TR-01`–`TR-10`, precum și integritatea linkurilor relative dintre fișiere.
- Nu s-a rulat niciun cod sau prototip; exemplele și scenariile sunt propuse pe hârtie.
- Mai e de făcut: revizuirea într-o conversație nouă, decizia echipei pe `DP-01`–`DP-05`, închiderea
  `QD-01`–`QD-04` și `Q-04`, apoi predarea către Cristina Simion pentru verificarea din Faza 4
  (`04-verificare/`).

## Cererea de revizuire

Se lipește într-o conversație AI nouă, împreună cu fișierele.

> Lucrezi ca evaluator (agent de revizuire) pentru partea „Proiectarea sistemului” a unui dosar de
> analiză și proiectare AMSS despre OCRInvoice. Nu rescrie nimic. Primești fișierele din
> `01-problema/`, `02-domeniu/`, `03-proiectare/` și acest rezumat. Verifică cele 6 criterii de mai
> sus. Pentru fiecare constatare scrie fișierul și ID-ul, textul în cauză, problema, un scenariu sau
> un contraexemplu concret și ce propui: acceptare, respingere cu motiv sau o întrebare deschisă cu
> pasul următor. Deosebește un defect de o regulă de funcționare nerezolvată și de o îmbunătățire
> opțională. Nu inventa erori și nu spune că ai verificat ceva ce n-ai putut verifica.

