# OCRInvoice

Dosarul de analiză și proiectare al echipei pentru *Analiza și Modelarea Sistemelor Software*
(AMSS), anul 2026/2027.

> Sinteza se completează pe parcurs. La final ar trebui să aibă cam două pagini și să trimită la
> fișierele din fiecare etapă.

## Echipa

| Membru | GitHub |
|--------|--------|
| Florențiu Mihai | [florentiu](https://github.com/florentiu) |
| Andreea Dima | [DimaAndreea](https://github.com/DimaAndreea) |
| Luisa Frincu | [Lizu2003](https://github.com/Lizu2003) |
| Cristina Simion | [SimionC](https://github.com/SimionC) |
| Ana-Maria Ștefan | [StefanAna-Maria](https://github.com/StefanAna-Maria) |

## Problema

Bonurile, chitanțele și facturile se pierd ușor. Cine vrea să știe cât a cheltuit trebuie să le
adune și să le treacă de mână, așa că de cele mai multe ori nu știe cât a cheltuit într-o lună și pe
ce. La o firmă mică e la fel: documentele ajung la contabil la final de lună, strânse pe hârtie.

În OCRInvoice utilizatorul fotografiază sau încarcă documentul. Un motor OCR citește datele de pe el
și spune, pentru fiecare valoare, cât de sigur e pe ea. Utilizatorul se uită doar la valorile
nesigure. Dacă produsele nu dau totalul, documentul nu poate fi salvat. Documentele salvate sunt
împărțite pe categorii, iar o firmă le poate exporta pentru contabil. Avem două tipuri de
utilizatori: persoana fizică (B2C) și firma (B2B).

## Limitele proiectului

Ne concentrăm pe drumul unui document:

încărcare → extragere → verificare și corecție → confirmare → categorisire sau export

Motorul OCR și programul de contabilitate SAGA sunt sisteme externe. Nu le analizăm pe dinăuntru, ne
interesează doar ce schimbăm cu ele. Predăm un dosar de analiză și proiectare, nu o aplicație.
Detaliile sunt în [01-problema/](01-problema/).

## Structura dosarului

| Folder | Ce conține | Cine se ocupă | Când |
|--------|------------|---------------|------|
| [01-problema/](01-problema/) | Beneficiari, obiective, limite, cerințe, ipoteze, întrebări deschise, exemple de acceptare | Florențiu Mihai | 01.11-08.11 |
| [02-domeniu/](02-domeniu/) | Glosar, concepte, identitate, relații, regulile domeniului | Andreea Dima | 09.11-15.11 |
| [03-proiectare/](03-proiectare/) | Responsabilități, granița cu sistemele externe, contracte, invarianți, stări și tranziții | Luisa Frincu | 15.11-22.11 |
| [04-verificare/](04-verificare/) | Scenarii, verificarea proprietăților, o alternativă de proiectare, efectul unei schimbări de cerință | Cristina Simion | 23.11-29.11 |
| [revizuiri/](revizuiri/) | Jurnalul revizuirilor, rezumatele de predare, decizia la care am lucrat cu AI | Ana-Maria Ștefan (revizuirea finală) | 30.11-06.12 |

## Deciziile principale

*De completat.*

## Verificările

*De completat.*

## Incertitudini rămase

*De completat.*

## Lucrul cu AI

Instrucțiunile cursului pentru asistenții AI sunt în [AGENTS.md](AGENTS.md). Revizuirile le facem
într-o conversație nouă, nu în cea în care s-a scris materialul, iar constatările și ce am decis le
notăm în [revizuiri/](revizuiri/).

## Contribuții

Florențiu Mihai a pornit dosarul (structura de foldere, instrucțiunile cursului pentru AI, sinteza de față) și a scris problema și cerințele, în [01-problema/](01-problema/).
