# Decizii de modelare, alternative și exemple

Prima parte arată ce am ales pentru fiecare concept și ce alternativă am respins. A doua parte are
exemplele care verifică distincțiile.

Deciziile sunt Propuneri AI până le discută echipa. Exemplele sunt pregătite de noi și propuse. Nu
le-am rulat. Numele, firmele și sumele sunt inventate și le continuă pe cele din
[../01-problema/05-exemple-de-acceptare.md](../01-problema/05-exemple-de-acceptare.md).

## Deciziile

| ID | Ce am ales | Alternativa | De ce am respins alternativa | Exemplu |
|----|------------|-------------|------------------------------|---------|
| D-01 | Documentul aparține unui cont. Contul e personal sau de firmă, iar utilizatorul e altceva decât contul. | Documentul aparține utilizatorului care l-a încărcat, iar firma e doar o etichetă pe document. | CF-12 spune că documentele firmei nu sunt ale angajatului. Dacă ar fi ale lui, ar pleca odată cu el. | ED-02 |
| D-02 | Documentul e identificat de sistem, din momentul în care apare. | Documentul e identificat de magazin, dată și total. | Două bonuri diferite pot avea același magazin, aceeași dată și același total, de exemplu două cafele în aceeași zi. În plus, o corectare a totalului ar schimba identitatea documentului. | ED-01 |
| D-03 | Imaginea-sursă e separată de document și nu se schimbă. | Imaginea e documentul, iar valorile sunt doar o citire a ei. | Utilizatorul corectează valori, nu poza. După o corectare, documentul și imaginea spun lucruri diferite, deci nu pot fi același lucru. | ED-03 |
| D-04 | O valoare ține minte valoarea citită, siguranța, valoarea curentă și marcajul. | Se păstrează doar valoarea curentă și marcajul. | CF-04 cere să se vadă ce a fost „corectat”, deci trebuie știut ce s-a citit la început. Fără valoarea citită, nu putem spune nici dacă o corectare a adus valoarea înapoi la cea inițială. | ED-03, ED-04 |
| D-05 | Linia există doar în documentul ei și e identificată de poziție. | Produsul e un articol de catalog, comun tuturor documentelor. | Nicio cerință nu urmărește același produs pe mai multe documente. Un catalog ar cere să hotărâm dacă „LAPTE 1,5%” și „LAPTE 1.5% 1L” sunt același articol. | ED-05 |
| D-06 | Magazinul e un text de pe document. | Magazinul e un lucru cu identitate, cu o listă proprie. | Nicio cerință nu grupează sau nu filtrează după magazin. Dacă apare o astfel de cerință, decizia se revizuiește. | ED-05 |
| D-07 | Cheltuiala manuală e un document cu exact o linie, scrisă de utilizator. | Cheltuiala manuală e un concept separat de document. | CF-13 cere pentru ea exact ce are o linie: pentru ce s-a plătit, suma și categoria. Ca document cu o linie, respectă aceleași reguli de apartenență, totaluri, corectare și ștergere (RD-01, RD-09, RD-11), fără să le scriem de două ori. | ED-07 |
| D-08 | Documentul ține de luna datei de pe el. | Documentul ține de luna în care a fost încărcat. | O-03 vrea ca utilizatorul să știe cât a cheltuit într-o lună. Un bon din 31 octombrie încărcat pe 2 noiembrie e o cheltuială din octombrie. | ED-06 |
| D-09 | Exportul are un moment al generării, iar conținutul lui rămâne cel de atunci. | Exportul e doar o privire asupra evidenței, recalculată la fiecare cerere. | Contabilul primește un fișier la un moment dat. Întrebarea Q-03, ce facem cu un document corectat după export, are sens doar dacă știm ce conținea fișierul trimis. | ED-08 |
| D-10 | În domeniu, documentul există de la încărcare, în orice stare. | Documentul există doar după confirmare. Până atunci e doar o citire în curs. | EA-05 vorbește despre „un bon al firmei rămas cu valori de verificat”. Ca să putem spune că e al firmei și că nu intră în export, trebuie să fie un document. | ED-08 |
| D-11 | Tipul documentului îl alege utilizatorul. | Tipul îl propune motorul OCR. | CF-02 nu trece tipul printre valorile întoarse de motorul OCR. Vezi Q-09. | - |

La D-07 am cântărit serios și alternativa, pentru că o cheltuială manuală nu trece prin extragere
și verificare. Am ales varianta cu o linie pentru că păstrează vocabularul din Faza 1, unde
cheltuiala manuală e un document, și face RD-09 valabilă la fel pentru toate documentele.

## Ce nu am decis aici

| Subiect | De ce rămâne deschis | Unde se decide |
|---------|----------------------|----------------|
| Dacă un document neconfirmat e păstrat de sistem sau doar pe telefon | Ține de proiectare, nu de domeniu (Q-01) | Faza 3 |
| Ce se întâmplă cu un document confirmat când o corectare strică potrivirea totalului | Ține de stări și tranziții (Q-02) | Faza 3 |
| Ce facem cu un document corectat sau șters după export | D-09 face întrebarea posibilă, dar nu îi răspunde (Q-03, P-01) | Faza 3 |
| Dacă un posibil duplicat e semnalat | D-02 spune doar că sunt două documente (Q-08, P-02) | Faza 3 |

## Exemplele

### ED-01. Același bon, încărcat de doi colegi

Dat fiind că Radu și Ioana sunt membri ai firmei Exemplu SRL și amândoi au în mână bonul de 25,68
lei de la MINIMARKET LUNA SRL din 10.11.2026,
când fiecare îl fotografiază și îl confirmă în contul firmei,
atunci:

- în evidența firmei sunt două documente, fiecare cu imaginea lui;
- totalul lunii crește cu 51,36 lei;
- dacă Ioana îl șterge pe al ei, al lui Radu rămâne neschimbat.

Cu alternativa la D-02 (identitate după magazin, dată și total) ar fi existat un singur document,
iar a doua încărcare ar fi fost respinsă sau l-ar fi înlocuit pe primul. Exemplul arată și de ce
contează Q-08: firma a plătit 25,68 lei, dar evidența arată 51,36 lei.

Verifică: D-02, RD-01. Stare: propus.

### ED-02. Radu, în contul lui și în contul firmei

Dat fiind că Radu a confirmat în noiembrie două bonuri în contul firmei (25,68 lei și 40,00 lei) și
un bon de 12,00 lei în contul lui personal,
când Radu nu mai e membru al firmei,
atunci:

- cele două bonuri rămân în evidența firmei, iar Ioana le vede în continuare;
- Radu nu le mai vede. Pentru el nu mai există;
- bonul de 12,00 lei rămâne în contul personal al lui Radu, iar Ioana nu l-a văzut niciodată.

Cu alternativa la D-01 (documentul e al celui care l-a încărcat), bonurile de 65,68 lei ar fi
plecat cu Radu, iar exportul firmei pe noiembrie ar fi rămas fără ele.

Cum iese un membru dintr-o firmă nu e în nucleu. Exemplul verifică doar a cui sunt documentele.

Verifică: D-01, RD-01, RD-02. Stare: propus.

### ED-03. Valoarea citită și valoarea curentă

Dat fiind bonul din EA-02, cu ora citită 12:40 și siguranța 0,62,
când Andrei schimbă ora în 12:45,
atunci:

- valoarea citită rămâne 12:40, iar siguranța rămâne 0,62;
- valoarea curentă e 12:45, iar marcajul trece din „de verificat” în „corectat”;
- imaginea-sursă e aceeași ca înainte.

Dacă Andrei ar fi acceptat ora 12:40 fără s-o schimbe, valoarea curentă ar fi rămas 12:40, iar
marcajul ar fi devenit „confirmat” (P-04, propunere).

Verifică: D-03, D-04, RD-03. Stare: propus.

### ED-04. Pragul

Dat fiind un bon pe care data e citită cu siguranța 0,80 și ora cu siguranța 0,79,
când se termină citirea,
atunci:

- data nu are niciun marcaj;
- ora are marcajul „de verificat”;
- documentul nu poate fi confirmat până când ora nu e corectată sau acceptată.

Verifică: RD-03, RD-05. Stare: propus.

### ED-05. Aceeași denumire pe două bonuri

Dat fiind că Andrei are două bonuri confirmate, fiecare cu o linie „LAPTE 1,5%” de 14,98 lei, în
categoria Alimente,
când schimbă categoria liniei de pe primul bon în Altele,
atunci:

- linia de pe al doilea bon rămâne la Alimente;
- Alimente scade cu 14,98 lei, iar Altele crește cu 14,98 lei;
- totalul lunii nu se schimbă.

Cu alternativa la D-05 (produs de catalog), schimbarea categoriei ar fi atins ambele bonuri. La fel
pentru magazin: dacă Andrei corectează „MINIMARKET LUNA SRL” pe un bon, celelalte bonuri de la
același magazin rămân cum erau (D-06).

Verifică: D-05, D-06, RD-06, RD-09. Stare: propus.

### ED-06. Data documentului și data încărcării

Dat fiind că Andrei a cheltuit 300,00 lei în octombrie 2026 și 425,68 lei în noiembrie,
când pe 2 noiembrie fotografiază și confirmă un bon de 50,00 lei cu data 31.10.2026,
atunci:

- bonul apare în listă la 31 octombrie;
- totalul lui octombrie ajunge la 350,00 lei;
- totalul lui noiembrie rămâne 425,68 lei.

O consecință: totalul unei luni încheiate se poate schimba. La o firmă, dacă exportul pe octombrie
a fost făcut pe 1 noiembrie, bonul acesta nu e în fișier. Asta întărește întrebarea Q-03.

Verifică: D-08, RD-08, RD-09. Stare: propus.

### ED-07. Cheltuiala manuală

Dat fiind că e 12 noiembrie 2026 și Andrei a cheltuit 425,68 lei în noiembrie,
când trece de mână „Parcare”, 10,00 lei, 11.11.2026, categoria Altele, numerar,
atunci:

- apare o cheltuială adăugată manual, fără imagine-sursă și fără oră, direct în evidență;
- documentul are o singură linie: „Parcare”, 10,00 lei, Altele. Totalul lui e 10,00 lei;
- totalul lunii ajunge la 435,68 lei, iar Altele crește cu 10,00 lei;
- nicio valoare nu are siguranță sau marcaj.

Dacă Andrei ar fi scris suma 0 sau data 13.11.2026, cheltuiala n-ar fi fost primită (RD-10).

Verifică: D-07, RD-09, RD-10. Stare: propus.

### ED-08. Documentul neconfirmat și exportul

Dat fiind situația din EA-05 (trei documente confirmate ale firmei, în total 376,18 lei, și un bon
al lui Radu rămas cu valori de verificat) și că exportul pe noiembrie a fost făcut pe 1 decembrie,
când pe 3 decembrie Radu verifică bonul rămas, de 15,00 lei, cu data 28.11.2026, și îl confirmă,
atunci:

- bonul a fost tot timpul un document al firmei, dar a intrat în evidență abia pe 3 decembrie;
- exportul din 1 decembrie are în continuare 3 documente și 376,18 lei;
- totalul firmei pe noiembrie e acum 391,18 lei;
- un export nou pe noiembrie ar avea 4 documente. Ar fi alt export, cu alt moment al generării.

Cu alternativa la D-09 (exportul ca privire recalculată) n-am putea spune că fișierul primit de
contabil diferă de evidență cu 15,00 lei.

Verifică: D-09, D-10, RD-07, RD-12. Stare: propus.
