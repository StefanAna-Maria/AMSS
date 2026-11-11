# Exemple de acceptare

Exemplele sunt propuse, nu le-am rulat. Magazinele, firmele și sumele sunt inventate pentru exemplu.

Primele trei exemple folosesc bonul acesta. La produse, prima siguranță e pentru denumire, a doua
pentru sumă.

| Câmp | Valoare citită | Siguranță |
|------|----------------|-----------|
| Magazin | MINIMARKET LUNA SRL | 0,97 |
| Data | 10.11.2026 | 0,91 |
| Ora | 12:40 | 0,93 |
| Plata | Card | 0,88 |
| Produsul 1 | LAPTE 1,5%, 14,98 lei, Alimente | 0,90 și 0,93 |
| Produsul 2 | PÂINE, 4,50 lei, Alimente | 0,92 și 0,95 |
| Produsul 3 | DETERGENT, 6,20 lei, Altele | 0,89 și 0,91 |
| Total | 25,68 lei | 0,95 |

## EA-01. Bon citit clar (B2C)

Dat fiind că e 10 noiembrie 2026, Andrei e în contul lui și a cheltuit 400,00 lei în noiembrie,
când fotografiază bonul și motorul OCR întoarce valorile din tabel,
atunci:

- nicio valoare nu e marcată „de verificat”;
- sistemul arată că produsele fac 25,68 lei, exact cât totalul de pe bon;
- confirmarea e permisă;
- după confirmare, bonul apare la 10 noiembrie, cu poza atașată. Totalul lunii ajunge la 425,68
  lei, Alimente crește cu 19,48 lei, iar Altele cu 6,20 lei. Cele două creșteri adunate (25,68 lei)
  sunt egale cu creșterea totalului lunii.

Verifică: CF-01, CF-02, CF-05, CF-06, CF-07, CF-14, CF-15, R-09. Stare: propus.

## EA-02. O valoare nesigură

Dat fiind același bon, dar cu ora citită cu siguranță 0,62,
când se termină citirea,
atunci:

- doar ora e marcată „de verificat”;
- confirmarea e blocată, deși totalul se potrivește;
- după ce Andrei schimbă ora în 12:45, ora apare ca „corectat”, iar documentul se poate confirma cu
  ora 12:45.

Nu știm încă ce se întâmplă dacă ora 12:40 era corectă (Q-07).

Verifică: CF-04, CF-06, R-02, R-03. Stare: propus.

## EA-03. Totalul nu se potrivește

Dat fiind același bon, dar cu totalul citit 28,68 lei (siguranță 0,95), adică cu 3 lei mai mult
decât fac produsele (25,68 lei),
când se termină citirea,
atunci:

- sistemul arată „Diferență de 3,00 lei față de total”;
- confirmarea e blocată, deși nicio valoare nu e marcată;
- Andrei corectează DETERGENT la 9,20 lei. Produsele fac acum 28,68 lei, cât totalul, și
  confirmarea e permisă.

Verifică: CF-05, CF-06, R-03, I-10. Stare: propus.

## EA-04. Motorul OCR nu răspunde

Dat fiind că motorul OCR e oprit și Andrei a cheltuit 425,68 lei în noiembrie,
când fotografiază un bon,
atunci:

- sistemul spune „Documentul nu a putut fi citit.” și îi dă butonul „Încearcă din nou”;
- niciun document nu e confirmat;
- totalul lunii rămâne 425,68 lei.

La fel se întâmplă și cu o poză ilizibilă.

Verifică: CF-03, CN-03, I-05. Stare: propus.

## EA-05. Exportul lunii pentru contabil (B2B)

Exemplul depinde de ipotezele I-01 la I-05. Dacă una dintre ele cade, îl rescriem.

Dat fiind firma Exemplu SRL, cu Ioana (administrator) și Radu (angajat), și că în noiembrie 2026:

- Radu a confirmat în contul firmei două bonuri, de 25,68 lei și de 40,00 lei;
- Ioana a confirmat o factură de 310,50 lei;
- Radu a mai încărcat un bon, care a rămas cu valori de verificat;
- Radu a confirmat un bon de 12,00 lei în contul lui personal;

când se face exportul firmei pe noiembrie 2026,
atunci:

- fișierul are exact 3 documente, în total 376,18 lei;
- bonul neconfirmat și bonul personal al lui Radu nu apar;
- nu apar documente din octombrie sau din decembrie.

Verifică: CF-10, CF-12, CN-01, I-01 la I-05. Stare: propus.
