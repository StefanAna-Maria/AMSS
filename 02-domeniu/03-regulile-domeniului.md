# Regulile domeniului

Regulile R-01 la R-09 din [../01-problema/04-ipoteze-si-intrebari.md](../01-problema/04-ipoteze-si-intrebari.md)
sunt reformulate aici pe conceptele din glosar. Nu adăugăm reguli de funcționare noi fără să le
marcăm.

Planul echipei cere reformularea regulilor RP01-RP04 din documentul OCRInvoice scris pentru cursul
de Scrum. Documentul acela nu e în repository, așa că legătura dintre RP01-RP04 și regulile de mai
jos rămâne de făcut (QD-01).

## Reguli

| ID | Regula | Vine din | Etichetă |
|----|--------|----------|----------|
| RD-01 | Fiecare document aparține exact unui cont, personal sau de firmă. Contul se stabilește la creare și nu se schimbă. | R-01, CF-12 | Stabilit. „Nu se schimbă” e Propunere AI |
| RD-02 | Un utilizator ajunge doar la documentele din contul lui personal și din contul firmei în care e membru. Pentru el, celelalte documente nu există. | R-01, CN-01, I-04 | Stabilit pentru contul personal, Ipoteză pentru firmă |
| RD-03 | O valoare citită cu siguranța sub 0,8 primește marcajul „de verificat”. La exact 0,8 nu îl primește. | R-02, I-08 | Stabilit |
| RD-04 | Totalul unui document se potrivește dacă e egal, la ban, cu suma liniilor lui. | R-03, I-10 | Stabilit. „La ban” e Ipoteză (I-10) |
| RD-05 | Un document poate fi confirmat doar dacă nicio valoare a lui nu are marcajul „de verificat” și totalul se potrivește. Un document confirmat respectă condițiile acestea cât timp rămâne confirmat, inclusiv după o corectare. | R-03, CF-06, CF-08 | Stabilit |
| RD-06 | Fiecare linie are exact o categorie, dintre cele 9. Dacă nu se știe alta, e Altele. | R-04, CF-07 | Stabilit |
| RD-07 | În evidența unui cont intră doar documentele confirmate. Lista, totalurile și exportul se uită doar în evidență. | CF-06, I-05 | Ipoteză (I-05) |
| RD-08 | Un document ține de luna în care cade data documentului, după fusul orar al utilizatorului. Data încărcării nu contează. | CN-02 | Stabilit pentru fusul orar. „Data documentului, nu a încărcării” e Propunere AI (D-08) |
| RD-09 | Totalul lunii e suma totalurilor documentelor din evidență care țin de luna aceea. Suma pe o categorie e suma liniilor din categoria aceea, din aceleași documente. Sumele pe categorii adunate dau totalul lunii. | R-09, CF-15 | Stabilit |
| RD-10 | O sumă scrisă de utilizator e mai mare decât 0 și are cel mult două zecimale. Data plății pusă de utilizator e cel târziu azi, fie la o cheltuială manuală, fie la corectarea oricărui document. O cheltuială manuală nu are oră. | R-06, R-07, CF-08, CF-13 | Stabilit |
| RD-11 | Un document se șterge doar după ce utilizatorul confirmă ștergerea. Odată șters, dispare definitiv din evidență, cu liniile și imaginea-sursă. | R-05, CF-09 | Stabilit. „Cu liniile și imaginea-sursă” e Propunere AI |
| RD-12 | Exportul unei firme pentru o lună cuprinde exact documentele din evidența firmei care țin de luna aceea. | CF-10, I-02, I-03 | Ipoteză |
| RD-13 | Un utilizator care nu și-a confirmat adresa de email nu poate intra în aplicație. | R-08 | Stabilit. E în afara nucleului |

## Ce observăm

**RD-09 rezultă din RD-05 și RD-06.** Dacă fiecare document din evidență are totalul egal cu suma
liniilor (RD-04, RD-05) și fiecare linie are exact o categorie (RD-06), atunci sumele pe categorii
dau totalul lunii fără nicio verificare în plus. De aceea schimbarea S-01 din Faza 1, care slăbește
R-03, strică și R-09. Pentru Faza 3: invariantul de păzit e RD-05, iar RD-09 e o proprietate de
verificat, nu o regulă de impus separat.

**RD-05 leagă confirmarea de corectare.** Regula spune ce e adevărat despre un document confirmat,
nu ce se întâmplă când corectarea ar strica potrivirea. Sunt două căi: corectarea e respinsă sau
documentul iese din starea Confirmat. Asta e întrebarea Q-02, pentru Faza 3.

**Procentele din R-09 nu sunt o regulă a domeniului.** „Procentele adunate dau 100%, cu o mică
abatere de rotunjire” ține de cum sunt afișate sumele. În domeniu rămâne doar egalitatea sumelor.

## Răspunsuri propuse la întrebările din Faza 1

Faza 1 a cerut ca Q-06, Q-07 și Q-09 să fie lămurite în Faza 2. Mai jos sunt propuneri. Decizia e a
echipei.

| Întrebarea | Propunerea | De ce | Ce se schimbă dacă echipa decide altfel |
|------------|------------|-------|-----------------------------------------|
| Q-06: categoria se poate schimba înainte de confirmare? | Da, oricând documentul poate fi corectat, înainte și după confirmare. | Categoria e o valoare a liniei, ca denumirea și suma. Nu vedem un motiv să fie tratată altfel. | Categorisirea devine un pas separat, după confirmare, iar documentul intră în evidență cu categoriile propuse de motorul OCR. |
| Q-07: cum scapă utilizatorul de marcaj dacă valoarea e corectă? | O acceptă fără s-o schimbe, iar marcajul devine „confirmat” (P-04). | Altfel ar rescrie o valoare corectă doar ca să poată confirma, ceea ce contrazice O-01. | Marcajul are doar trei valori, iar EA-02 rămâne fără răspuns pentru ora corectă. |
| Q-09: cine hotărăște tipul documentului? | Utilizatorul, la încărcare, și îl poate schimba la corectare (D-11). | CF-02 enumeră ce întoarce motorul OCR, iar tipul nu e în listă. | Dacă îl propune motorul OCR, CF-02 se extinde, iar tipul devine o valoare cu siguranță și marcaj. |

## Întrebări deschise apărute în această etapă

| ID | Întrebarea | De ce contează | Cine decide |
|----|------------|----------------|-------------|
| QD-01 | Care sunt regulile RP01-RP04 și cele 9 categorii din documentul de la Scrum? | Planul cere să le reformulăm, iar CF-07 trimite lista categoriilor la glosar. Fără sursă nu le putem scrie. | Echipa, înainte de revizuirea Fazei 2 |
| QD-02 | O linie poate avea sumă negativă, de exemplu o reducere tipărită pe bon? | R-06 cere sume mai mari decât 0. Un bon cu „REDUCERE -2,00” n-ar putea fi confirmat niciodată, pentru că fără linia aceea suma liniilor nu dă totalul. | Echipa, înainte de Faza 3 |
| QD-03 | La o factură, sumele liniilor sunt cu TVA sau fără? | Dacă liniile sunt fără TVA și totalul e cu TVA, RD-04 nu e îndeplinită niciodată pentru facturi. | Echipa, înainte de Faza 3 |
| QD-04 | Ce valori sunt obligatorii pentru fiecare tip de document? | O chitanță poate să nu aibă linii, iar o factură nu are de obicei oră. Trebuie să știm dacă o valoare lipsă blochează confirmarea. | Echipa, înainte de Faza 3 |
| QD-05 | Un utilizator poate fi membru în mai multe firme? | Dacă da, la încărcare alege între mai multe conturi, iar „firma lui” din CN-01 devine „firmele lui”. | Echipa, în Faza 3 |
| QD-06 | Ce înseamnă „suma” și „categoria” din CF-08 la un document cu mai multe linii? | La un bon cu trei linii, categoria e pe fiecare linie, nu pe document. Textul din CF-08 se potrivește doar cheltuielii manuale. | Florențiu, la revizuirea Fazei 1 |
| QD-07 | Categoria propusă de motorul OCR are siguranță și poate fi marcată „de verificat”? | CF-02 spune că fiecare valoare are siguranță, dar exemplele din Faza 1 dau siguranță doar pentru denumire și sumă. Dacă are, o categorie nesigură blochează confirmarea. | Echipa, înainte de Faza 3 |

Până la un răspuns, lucrăm cu aceste ipoteze: o linie are sumă mai mare decât 0 (QD-02), un
document are cel puțin o linie (QD-04), un utilizator e membru în cel mult o firmă (QD-05), iar
categoria nu are siguranță și nu blochează confirmarea (QD-07).
