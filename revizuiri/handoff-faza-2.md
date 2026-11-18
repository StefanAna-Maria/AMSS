# Predarea Fazei 2 către revizuire și proiectare

De la Andreea Dima (Faza 2, domeniul), către evaluatorul domeniului și către Luisa Frincu, care
face proiectarea în Faza 3.

## 1. Rolul, întrebarea, ce așteptăm și unde se oprește

- Rolul: evaluator al modelului de domeniu, nu autor.
- Întrebarea: sunt conceptele, identitățile, relațiile și regulile din `02-domeniu/` coerente cu
  `01-problema/` și destul de clare ca să putem scrie contracte, invarianți și stări pe ele?
- Ce așteptăm: o listă de constatări. Fiecare are fișierul, ID-ul și o propunere de decizie
  (acceptată, respinsă cu motiv sau deschisă, cu pasul următor). Constatările intră în
  jurnalul din `revizuiri/`.
- Unde se oprește: evaluatorul nu rescrie fișierele și nu începe proiectarea.

## 2. Fișierele și versiunea

| Fișier | Versiunea |
|--------|-----------|
| `02-domeniu/*.md` | același commit cu acest rezumat (commit-ul `02-domeniu`) |
| `01-problema/*.md` | commit-ul `2bda01e` |

Evaluatorul primește acest rezumat, fișierele din `02-domeniu/` și sursele din `01-problema/`.

## 3. Ce e decis, ce e ipoteză și ce e deschis

- Preluat din Faza 1, fără schimbări de fond: regulile R-01 la R-09, reformulate ca RD-01 la RD-13.
- Propuneri AI, de discutat în echipă: deciziile D-01 la D-11 și răspunsurile la Q-06, Q-07 și
  Q-09. Cele care schimbă cel mai mult proiectarea sunt D-01 (cont separat de utilizator), D-07
  (cheltuiala manuală ca document cu o linie), D-09 (exportul cu moment al generării) și D-10
  (documentul există de la încărcare).
- Ipoteze de lucru: o linie are sumă mai mare decât 0, un document are cel puțin o linie, un
  utilizator e membru în cel mult o firmă, categoria nu are siguranță.
- Întrebări deschise noi: QD-01 la QD-07. QD-01 (RP01-RP04 și lista celor 9 categorii) trebuie
  închisă înainte de revizuire. QD-02, QD-03 și QD-04 trebuie închise înainte de contracte.
- Rămase din Faza 1 pentru Faza 3: Q-01, Q-02, Q-03, Q-04, Q-05 și Q-08.

## 4. Constrângeri, scenarii, invarianți și criterii

- Constrângeri: domeniul nu alege clase, tabele sau structuri de date. Vocabularul din Faza 1 se
  păstrează, cu o singură schimbare: „produs” devine „linie”.
- Scenarii: ED-01 la ED-08 în `02-domeniu/04-distinctii-si-alternative.md`.
- Invarianți propuși pentru Faza 3: RD-01 (un document, un cont), RD-05 (un document confirmat nu
  are valori „de verificat”, iar totalul se potrivește), RD-07 (doar documentele confirmate sunt
  în evidență). RD-09 rezultă din RD-05 și RD-06, deci e o proprietate de verificat.
- Criterii de revizuire:
  1. Fiecare concept are o definiție, o identitate sau motivul pentru care e doar o valoare.
  2. Fiecare regulă RD trimite la o regulă sau cerință din Faza 1, ori e marcată ca propunere.
  3. Nicio regulă din Faza 1 nu s-a pierdut și nu și-a schimbat sensul la reformulare.
  4. Fiecare decizie D are o alternativă plauzibilă și un exemplu care le deosebește.
  5. Cifrele din exemplele ED sunt corecte și se potrivesc cu EA-01 la EA-05.
  6. Nicăieri nu apar clase, tabele sau alte alegeri de implementare.
  7. Întrebările deschise nu sunt tranșate pe tăcute.

## 5. Ce am verificat și ce mai e de făcut

- Am verificat: calculele din ED-01 la ED-08, faptul că fiecare R-01 la R-09 apare în cel puțin o
  regulă RD și faptul că fiecare ID folosit în `02-domeniu/` e definit.
- Exemplele ED-01 la ED-08 sunt propuse, nu le-am rulat.
- Mai e de făcut: revizuirea într-o conversație nouă, decizia echipei pe D-01 la D-11 și pe
  răspunsurile la Q-06, Q-07 și Q-09, apoi închiderea QD-01.

## Cererea de revizuire

Se lipește într-o conversație AI nouă, împreună cu fișierele.

> Lucrezi ca evaluator (agent de revizuire) pentru partea „Modelarea domeniului” a unui dosar de
> analiză AMSS despre OCRInvoice. Nu rescrie nimic. Primești fișierele din `01-problema/`, cele din
> `02-domeniu/` și acest rezumat. Verifică cele 7 criterii de mai sus. Pentru fiecare constatare
> scrie fișierul și ID-ul, textul în cauză, problema, un scenariu sau un contraexemplu concret și ce
> propui: acceptare, respingere cu motiv sau o întrebare deschisă cu pasul următor. Deosebește un
> defect de o regulă de funcționare nerezolvată și de o îmbunătățire opțională. Nu inventa erori și
> nu spune că ai verificat ceva ce n-ai putut verifica.
