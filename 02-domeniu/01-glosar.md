# Glosar

Termenii sunt grupați după subiect. Coloana „Sursa” arată de unde vine termenul: o cerință sau o
regulă din Faza 1, ori o decizie din această etapă.

## Cine

| Termen | Definiție | Sursa |
|--------|-----------|-------|
| Utilizator | O persoană care intră în aplicație cu adresa de email și parola ei. | CF-11 |
| Cont | Cel căruia îi aparțin documentele. E de două feluri: personal sau de firmă. | D-01 |
| Cont personal | Contul unei singure persoane. Fiecare utilizator are exact unul. | R-01 |
| Cont de firmă | Contul unei firme. Documentele din el sunt ale firmei, nu ale celui care le-a încărcat. | CF-12, I-04 |
| Membru | Un utilizator care lucrează în contul unei firme. Poate fi administrator sau angajat. | I-04 |
| Contabil | Persoana care primește exportul și îl importă în SAGA. Nu e utilizator al sistemului. | I-01 |

## Documentul

| Termen | Definiție | Sursa |
|--------|-----------|-------|
| Document | O cheltuială ținută în sistem: un bon, o factură, o chitanță sau o cheltuială manuală. | 01-problema/README |
| Document scanat | Un document pornit de la o poză sau un PDF: bon, factură sau chitanță. | CF-01 |
| Cheltuială manuală | O cheltuială adăugată manual: utilizatorul completează un formular, fără să scaneze sau să importe un document. Nu are imagine-sursă și nici oră. | CF-13, R-07, D-07 |
| Tipul documentului | Bon, factură, chitanță sau cheltuială adăugată manual. | CF-14 |
| Imagine-sursă | Poza sau PDF-ul din care a pornit un document scanat. Nu se schimbă niciodată. | CF-01, D-03 |
| Magazin | Numele celui care a emis documentul, așa cum apare pe el. La o factură e furnizorul. | CF-02, D-06 |
| Data documentului | Ziua plății, scrisă pe document. Nu e ziua în care a fost încărcat. | CF-02, D-08 |
| Plata | Cum s-a plătit: numerar, card sau transfer. | CF-13 |
| Notă | Un text liber, opțional, adăugat de utilizator. | CF-08, CF-13 |
| Linie (produs) | Un rând de pe document: o denumire, o sumă și o categorie. În Faza 1 apare ca „produs”. | CF-02, D-05 |
| Categorie | Una dintre cele 9 etichete fixe ale aplicației, de exemplu Alimente sau Altele. | CF-07, R-04 |

Lista completă a celor 9 categorii nu apare în Faza 1 (vezi QD-01).

## Extragerea și verificarea

| Termen | Definiție | Sursa |
|--------|-----------|-------|
| Motorul OCR | Sistemul extern care citește imaginea-sursă și întoarce valori. | CF-02 |
| Valoare citită | Ce a întors motorul OCR pentru un câmp al documentului sau al unei linii. | CF-02 |
| Siguranță | Un număr între 0 și 1, dat de motorul OCR pentru fiecare valoare citită. Nu e o garanție. | CF-02, P-03 |
| Prag | 0,8. Sub el, o valoare citită trebuie verificată. | R-02, I-08 |
| Valoare curentă | Valoarea pe care o are câmpul acum: cea citită sau cea pusă de utilizator. | D-04 |
| Marcaj | Ce se știe despre o valoare: „de verificat”, „corectat”, „confirmat” sau niciunul. | CF-04, P-04 |
| Corectare | Schimbarea unei valori curente de către utilizator. | CF-04, CF-08 |

## Sumele

| Termen | Definiție | Sursa |
|--------|-----------|-------|
| Totalul documentului | Suma de plată scrisă pe document. E o valoare citită, ca oricare alta. | CF-02 |
| Suma liniilor | Sumele liniilor unui document, adunate. E calculată, nu citită. | CF-05 |
| Diferență | Totalul documentului minus suma liniilor. | CF-05 |
| Totalul se potrivește | Diferența e zero, la ban. | I-10 |
| Totalul lunii | Totalurile documentelor din evidența unui cont, cu data în luna respectivă, adunate. | CF-14, CN-02 |
| Suma pe categorie | Sumele liniilor dintr-o categorie, din aceleași documente, adunate. | CF-15 |

## Evidența și exportul

| Termen | Definiție | Sursa |
|--------|-----------|-------|
| Confirmare | Hotărârea utilizatorului că documentul e corect și intră în evidență. | CF-06 |
| Evidență | Documentele confirmate ale unui cont. Doar ele apar în listă, în totaluri și în export. | I-05 |
| Starea documentului | Unde a ajuns documentul pe drumul lui: Încărcat, În procesare, De verificat, Confirmat sau Eroare. Tranzițiile le stabilește Faza 3. | Q-01, D-10 |
| Export | Fișierul cu documentele din evidența unei firme pentru o lună, făcut la un moment anume. | CF-10, D-09 |
| SAGA | Programul de contabilitate al contabilului. E extern și nu vorbește cu sistemul. | I-01 |

## Termeni pe care îi evităm

| Termen | De ce | Ce folosim |
|--------|-------|------------|
| „Salvare” | În Faza 1 înseamnă confirmare, dar se poate înțelege și ca păstrarea unei ciorne. | Confirmare |
| „Produs” ca articol de catalog | Sistemul nu ține un catalog de produse. LAPTE de pe două bonuri sunt două linii. | Linie |
| „Contul lui Radu” pentru documentele firmei | Documentele firmei nu sunt ale angajatului (CF-12). | Contul firmei |
