# Cerințele

Cerințele spun ce face sistemul, nu cum îl construim, așa că nu apar tehnologii, ecrane sau formate
interne. Prin confirmare înțelegem salvarea documentului după verificare.

## Cerințe funcționale din nucleu

| ID | Ce | Cerința | Etichetă |
|----|----|---------|----------|
| CF-01 | Încărcarea | Utilizatorul poate aduce un document fotografiindu-l cu camera, alegând o poză din galerie sau un fișier (PDF sau imagine). Imaginea rămâne atașată documentului confirmat. | Stabilit |
| CF-02 | Extragerea | Sistemul primește de la motorul OCR magazinul, data, ora, totalul, modul de plată și fiecare produs cu categoria lui. Fiecare valoare are un grad de siguranță între 0 și 1. | Stabilit |
| CF-03 | Progresul și eșecul | Cât durează citirea, utilizatorul vede în ce etapă e. Sunt patru, în ordine: încărcarea, citirea, găsirea magazinului, a datei și a totalului, apoi extragerea produselor. Dacă documentul nu se poate citi sau motorul OCR nu răspunde, utilizatorul află și poate încerca din nou. | Stabilit |
| CF-04 | Valorile de verificat | O valoare citită cu siguranță sub 0,8 e marcată „de verificat”. După ce utilizatorul o corectează, apare ca „corectat”. | Stabilit |
| CF-05 | Totalul | Sistemul arată cât fac produsele adunate și dacă suma se potrivește cu totalul de pe document. Dacă nu, arată diferența. | Stabilit (ce înseamnă „se potrivește”: I-10) |
| CF-06 | Confirmarea | Documentul se poate confirma doar dacă nu mai are valori de verificat și totalul se potrivește. După confirmare apare în listă și în totaluri. | Stabilit |
| CF-07 | Categoriile | Fiecare produs are exact una din cele 9 categorii ale aplicației, de exemplu Alimente. Implicit e Altele. Lista completă intră în glosarul domeniului. | Stabilit |
| CF-08 | Corectarea după confirmare | Utilizatorul poate schimba magazinul, data, suma, categoria, plata și nota. Se aplică aceleași validări ca la adăugare, iar lista și totalurile se actualizează. | Stabilit |
| CF-09 | Ștergerea | Sistemul întreabă „Ștergi documentul?”. După confirmare, documentul dispare din listă și din totaluri. | Stabilit |
| CF-10 | Exportul (B2B) | Pentru o firmă și o lună, sistemul face un fișier cu documentele confirmate ale firmei, pe care contabilul îl poate importa în SAGA. | Ipoteză (I-01 la I-03) |

## Cerințe funcționale din jurul nucleului

| ID | Ce | Cerința | Etichetă |
|----|----|---------|----------|
| CF-11 | Contul | Utilizatorul are un cont cu email și parolă. Adresa se confirmă cu un cod primit pe email, iar fără confirmare nu poate intra. Dacă uită parola, o resetează tot cu un cod pe email. | Stabilit |
| CF-12 | Contul de firmă | Un document e fie personal, fie al unei firme, niciodată amândouă. Documentele firmei sunt ale firmei, nu ale angajatului care le-a încărcat. | Ipoteză (I-04) |
| CF-13 | Cheltuiala manuală | Utilizatorul poate trece o plată pentru care nu are document: pentru ce a plătit, suma, data (cel târziu azi), categoria, cum a plătit (numerar, card sau transfer) și, dacă vrea, o notă. Nu trece prin extragere și verificare. | Stabilit |
| CF-14 | Consultarea | Utilizatorul vede documentele lunii grupate pe zile, cu suma fiecărei zile, totalul lunii față de luna trecută, detaliul unui document și un filtru după tip (bonuri, facturi, chitanțe, manuale). | Stabilit |
| CF-15 | Categoriile lunii | Pentru fiecare categorie în care a cheltuit luna asta, utilizatorul vede suma și ce procent e din totalul lunii, de la cea mai mare la cea mai mică. Sumele pe categorii adunate dau totalul lunii (R-09). | Stabilit |
| CF-16 | Ștergerea contului | După confirmare se șterg definitiv contul, sesiunile și documentele. | Stabilit |

## Cerințe nefuncționale

| ID | Tip | Cerința | Etichetă |
|----|-----|---------|----------|
| CN-01 | Confidențialitate | Un utilizator vede și modifică doar documentele din contul lui. La B2B le vede și pe ale firmei lui (I-04). Un document din alt cont se comportă ca și cum n-ar exista. | Stabilit |
| CN-02 | Corectitudine | Totalurile sunt corecte la ban. Luna începe la miezul nopții pe 1, după fusul orar al utilizatorului. | Stabilit |
| CN-03 | Fiabilitate | Dacă serverul sau motorul OCR nu răspund, utilizatorul află, iar ce a scris nu se pierde. | Stabilit |
| CN-04 | Fiabilitate | Dacă aceeași salvare pleacă de două ori (o dublă apăsare sau o reîncercare), se creează un singur document. | Stabilit pentru cheltuiala manuală, ipoteză pentru documentele scanate |
| CN-05 | Securitate | Parolele și codurile se păstrează doar într-o formă din care nu pot fi recuperate. Încercările repetate de intrare în cont sunt limitate. Sistemul nu lasă pe nimeni să afle dacă o adresă are cont. | Stabilit |
| CN-06 | Utilizabilitate | Aplicația e în română sau engleză, implicit în limba telefonului. Sumele și datele se scriu după limba aleasă. Mesajele de eroare spun ce poate face utilizatorul mai departe. | Stabilit |
