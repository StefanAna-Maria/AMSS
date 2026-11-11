# Reguli, ipoteze și întrebări deschise

Le ținem separat. Regulile sunt hotărâte, ipotezele sunt presupuneri ale noastre, întrebările
așteaptă o decizie, iar propunerile AI n-au fost încă discutate în echipă.

## Reguli stabilite

| ID | Regula | Legată de |
|----|--------|-----------|
| R-01 | Un document personal e al unui singur utilizator. Nimeni altcineva nu-l poate vedea, modifica sau șterge. | CN-01 |
| R-02 | O valoare citită cu siguranță sub 0,8 trebuie verificată de utilizator. | CF-04 |
| R-03 | Un document nu se poate confirma cât timp are valori de verificat sau produsele adunate nu dau totalul. | CF-05, CF-06 |
| R-04 | Sunt exact 9 categorii, iar fiecare produs are una singură. | CF-07 |
| R-05 | Înainte ca un document să fie șters, utilizatorul trebuie să confirme. | CF-09 |
| R-06 | O sumă trecută de mână e mai mare decât 0 și are cel mult două zecimale. Data plății e cel târziu azi. | CF-08, CF-13 |
| R-07 | O cheltuială manuală are dată, dar nu are oră. | CF-13 |
| R-08 | Cine nu și-a confirmat adresa de email nu poate intra în cont. | CF-11 |
| R-09 | Într-o lună, sumele pe categorii adunate dau totalul lunii, iar procentele adunate dau 100%, cu o mică abatere de rotunjire. | CF-15, CN-02 |

## Ipoteze

| ID | Ce presupunem | De ce | Ce se schimbă dacă nu e așa |
|----|---------------|-------|-----------------------------|
| I-01 | Exportul e un fișier pe care contabilul îl importă singur în SAGA. Sistemul nu vorbește direct cu SAGA. | SAGA e un program separat, pe care îl folosește contabilul | SAGA devine un sistem cu care schimbăm date în ambele sensuri, cu erori de comunicare și confirmări de primire |
| I-02 | Exportul cuprinde doar documentele confirmate ale firmei dintr-o lună calendaristică. | Documentele neconfirmate nu sunt în evidență (I-05) | Se schimbă contractul exportului și invarianții lui |
| I-03 | Exportul există doar pentru firme. O persoană fizică nu exportă. | Contabilul lucrează pentru o firmă | CF-10 se extinde și la B2C |
| I-04 | Toți membrii firmei văd documentele firmei și oricare dintre ei le poate corecta sau șterge. | Firma e un spațiu comun al membrilor | Apar roluri cu drepturi diferite, iar corectarea și ștergerea primesc o condiție de rol |
| I-05 | Un document încărcat, dar neconfirmat, nu apare în listă, în totaluri sau în export. | Documentul apare în listă abia după confirmare (CF-06) | Totalurile ar trebui să deosebească documentele confirmate de cele neconfirmate |
| I-06 | Dintr-un PDF se citește doar prima pagină. | E o simplificare a noastră | La o factură pe mai multe pagini ar lipsi produse, iar totalul n-ar mai putea fi verificat |
| I-07 | Totul e în lei, într-o singură monedă. | Nicio cerință nu vorbește de altă monedă | Totalurile și exportul ar avea nevoie de conversie |
| I-08 | Pragul de 0,8 e fix și nu se poate schimba din setări. | Nicio cerință nu cere un prag configurabil | Pragul devine o setare cu o valoare implicită (vezi S-02) |
| I-09 | Dacă citirea nu se termină într-un timp stabilit, o considerăm eșuată. | Altfel utilizatorul n-ar afla că motorul OCR nu răspunde (CN-03) | Utilizatorul ar putea aștepta la nesfârșit |
| I-10 | Produsele adunate „se potrivesc” cu totalul doar dacă sunt egale la ban, fără nicio toleranță. | Totalurile trebuie să fie corecte la ban (CN-02) | Cu o toleranță, de exemplu de un ban, ar intra în evidență documente cu mici diferențe, iar R-09 n-ar mai ieși exact |

## Întrebări deschise

| ID | Întrebarea | De ce contează | Cine decide și până când |
|----|------------|----------------|--------------------------|
| Q-01 | Sistemul păstrează documentele încărcate, dar neconfirmate (Încărcat, În procesare, De verificat, Eroare), sau ele stau doar pe telefon până la confirmare? | Așa aflăm dacă acestea sunt stări ale documentului în sistem sau doar ale ecranului | Echipa, înainte de Faza 3 |
| Q-02 | Dacă un document confirmat e corectat, revine la „De verificat”? Sau totalul se recalculează din produse și documentul rămâne confirmat? | De aici rezultă tranzițiile de după confirmare | Echipa, înainte de Faza 3 |
| Q-03 | Ce facem cu un document deja exportat care e apoi corectat sau șters? | Contabilul are deja varianta veche în SAGA | Echipa, înainte de Faza 3 |
| Q-04 | Exportul se face la cerere sau automat, la final de lună? Ce format acceptă SAGA? | De aici rezultă ce pornește exportul și contractul cu SAGA | Echipa, după ce ne uităm în documentația SAGA, în Faza 3 |
| Q-05 | Cine poate exporta: orice membru sau doar administratorul? | E condiția de pornire a exportului | Echipa, în Faza 3 |
| Q-06 | Utilizatorul poate schimba categoria propusă de motorul OCR înainte de confirmare sau doar după, când corectează? | Ne spune unde intră categorisirea în drumul documentului | Echipa, în Faza 2 |
| Q-07 | Dacă o valoare nesigură e de fapt corectă, cum scapă utilizatorul de marcajul „de verificat” fără s-o modifice? | Altfel ar trebui să rescrie o valoare corectă doar ca să poată confirma | Echipa, în Faza 2 |
| Q-08 | Ce se întâmplă dacă același bon e încărcat de două ori, de exemplu de doi colegi? | Apar dubluri în totaluri și în export | Echipa, în Faza 3 |
| Q-09 | Cine hotărăște tipul documentului (bon, factură, chitanță): motorul OCR, utilizatorul sau amândoi? | Tipul se folosește la filtrare, deci trebuie să știm de unde vine | Echipa, în Faza 2 |

## Propuneri AI, nediscutate încă

| ID | Propunerea | Legată de |
|----|------------|-----------|
| P-01 | Documentele exportate să fie marcate „exportat în {lună}”, ca o corectare făcută după export să poată fi semnalată contabilului. | Q-03 |
| P-02 | Un posibil duplicat (același magazin, aceeași dată și același total în același cont) să fie semnalat, dar nu blocat. | Q-08 |
| P-03 | Siguranța raportată de motorul OCR nu e o garanție. O valoare cu siguranță mare poate fi greșită, iar potrivirea totalului prinde o parte din aceste greșeli. | R-02, R-03 |
| P-04 | Pentru Q-07, utilizatorul să poată confirma o valoare nesigură fără s-o modifice, iar valoarea să apară ca „confirmat”. | Q-07, CF-04 |
