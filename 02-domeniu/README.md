# Domeniul

Autor: Andreea Dima. Faza 2, 09.11-15.11.2026. Ciornă, înainte de revizuire.

Aici stabilim despre ce lucruri vorbește OCRInvoice, ce le identifică, cum se leagă între ele și ce
reguli respectă. Pornim de la [../01-problema/](../01-problema/). Nu alegem clase, tabele sau
structuri de date: un concept de aici poate ajunge în proiectare o componentă, o parte dintr-una sau
doar o valoare.

## Fișierele

| Fișier | Ce găsești acolo |
|--------|------------------|
| [01-glosar.md](01-glosar.md) | Termenii, fiecare cu o definiție scurtă |
| [02-concepte-si-relatii.md](02-concepte-si-relatii.md) | Ce identifică fiecare concept și în ce relații stă cu celelalte |
| [03-regulile-domeniului.md](03-regulile-domeniului.md) | Regulile R-01 la R-09 reformulate pe concepte, plus ce rămâne deschis |
| [04-distinctii-si-alternative.md](04-distinctii-si-alternative.md) | Deciziile de modelare, alternativa respinsă și exemplele care verifică distincțiile |

## Pe scurt

- Un document aparține unui cont, nu unui utilizator. Contul e personal sau de firmă (D-01).
- Documentul e identificat de sistem, nu de ce scrie pe el. Același bon încărcat de două ori
  înseamnă două documente (D-02).
- Imaginea-sursă nu se schimbă niciodată. Corecturile schimbă valorile documentului (D-03).
- O valoare ține minte ce a citit motorul OCR, cu ce siguranță, și ce valoare are acum (D-04).
- Linia (produsul) există doar în documentul ei. Magazinul și categoria sunt valori, nu lucruri cu
  identitate proprie (D-05, D-06).
- Cheltuiala manuală e un document cu o singură linie, scrisă de utilizator (D-07).
- Documentul ține de luna datei de pe el, nu de luna în care a fost încărcat (D-08).
- Exportul are un moment al generării și un conținut care nu se mai schimbă după aceea (D-09).

## Etichete

Folosim etichetele din [../01-problema/README.md](../01-problema/README.md): Stabilit, Ipoteză,
Întrebare și Propunere AI. Ce vine direct din Faza 1 își păstrează eticheta de acolo. Deciziile noi
din această etapă sunt marcate Propunere AI până le discută echipa.

Identificatorii noi:

- D-xx: decizie de modelare, în [04-distinctii-si-alternative.md](04-distinctii-si-alternative.md);
- RD-xx: regulă a domeniului, în [03-regulile-domeniului.md](03-regulile-domeniului.md);
- ED-xx: exemplu care verifică o distincție, în
  [04-distinctii-si-alternative.md](04-distinctii-si-alternative.md);
- QD-xx: întrebare deschisă apărută în această etapă, în
  [03-regulile-domeniului.md](03-regulile-domeniului.md).

Exemplele ED-01 la ED-08 sunt pregătite de noi și propuse. Nu le-am rulat.

> Am lucrat la ciornă cu un asistent AI, în rol de analist. Revizuirea se face separat, într-o
> conversație nouă (vezi [../revizuiri/handoff-faza-2.md](../revizuiri/handoff-faza-2.md)).
