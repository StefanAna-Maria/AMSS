# Predarea Fazei 1 către revizuire și domeniu

De la Florențiu Mihai (Faza 1, problema), către Ana-Maria Ștefan, care revizuiește problema, și
Andreea Dima, care face domeniul în Faza 2.

## 1. Rolul, întrebarea, ce așteptăm și unde se oprește

- Rolul: evaluator al problemei și al cerințelor, nu autor.
- Întrebarea: sunt limitele și ipotezele din `01-problema/` clare, coerente și destul de complete ca
  să putem începe domeniul și proiectarea?
- Ce așteptăm: o listă de constatări. Fiecare are fișierul, ID-ul și o propunere de decizie
  (acceptată, respinsă cu motiv sau deschisă, cu pasul următor). Constatările intră în jurnalul din
  `revizuiri/`.
- Unde se oprește: evaluatorul nu rescrie fișierele și nu începe domeniul sau proiectarea.

## 2. Fișierele și versiunea

| Fișier | Versiunea |
|--------|-----------|
| `01-problema/*.md` | același commit cu acest rezumat (commit-ul `01-problema`) |

Evaluatorul primește și acest rezumat, și fișierele originale.

## 3. Ce e decis, ce e ipoteză și ce e deschis

- Decis: nucleul (încărcare → extragere → verificare și corecție → confirmare → categorisire sau
  export), sistemele externe (motorul OCR, SAGA, serviciul de email) și regulile R-01 la R-09.
- Ipoteze: I-01 la I-10, în `04-ipoteze-si-intrebari.md`. Cele mai importante sunt I-01, I-02, I-05
  și I-10.
- Întrebări deschise: Q-01 la Q-09. Q-06, Q-07 și Q-09 trebuie lămurite înainte de Faza 2, iar
  Q-01, Q-02 și Q-03 înainte de Faza 3.
- Pentru glosar, în Faza 2: lista completă a celor 9 categorii (CF-07) și termenii din
  `01-problema/README.md`.

## 4. Constrângeri, scenarii, invarianți și criterii

- Constrângeri: motorul OCR e extern și poate fi lent sau oprit. SAGA e extern și nu ne răspunde.
- Scenarii: EA-01 la EA-05 în `05-exemple-de-acceptare.md` și schimbările S-01 și S-02 în
  `06-schimbarea-unei-cerinte.md`.
- Invarianți propuși pentru Faza 3: un document e al unui singur cont (R-01, CF-12); un document
  confirmat nu are valori de verificat, iar produsele adunate dau totalul (R-03, I-10); sumele pe
  categorii adunate dau totalul lunii (R-09).
- Criterii de revizuire:
  1. Fiecare cerință are eticheta „stabilit” sau „ipoteză”.
  2. Nicio cerință nu intră în detalii de implementare.
  3. Granița nucleului e clară: pentru orice funcție se poate spune dacă e înăuntru sau nu.
  4. Fiecare ipoteză spune ce se schimbă dacă nu e adevărată.
  5. Exemplele au rezultate pe care le putem verifica, cu cifre.
  6. Efectul schimbărilor S-01 și S-02 e urmărit până la cerințele, regulile și exemplele pe care le
     atinge.

## 5. Ce am verificat și ce mai e de făcut

- Am verificat calculele din EA-01 la EA-05 și din S-02 și faptul că fiecare ID folosit în
  `01-problema/` e definit.
- Exemplele EA-01 la EA-05 sunt propuse, nu le-am rulat.
- Mai e de făcut: revizuirea într-o conversație nouă, decizia echipei pe I-01 la I-05 și I-10 și
  răspunsurile la întrebările care blochează Faza 2.

## Cererea de revizuire

Se lipește într-o conversație AI nouă, împreună cu fișierele.

> Lucrezi ca evaluator (agent de revizuire) pentru partea „Problemă și cerințe” a unui dosar de
> analiză AMSS despre OCRInvoice. Nu rescrie nimic. Primești fișierele din `01-problema/` și acest
> rezumat. Verifică cele 6 criterii de mai sus. Pentru fiecare constatare scrie fișierul și ID-ul,
> textul în cauză, problema, o consecință concretă și ce propui: acceptare, respingere cu motiv sau o
> întrebare deschisă cu pasul următor. Deosebește un defect de o întrebare pentru beneficiar și de o
> îmbunătățire opțională. Nu inventa erori și nu spune că ai verificat ceva ce n-ai putut verifica.
