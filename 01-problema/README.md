# Problema și cerințele

Autor: Florențiu Mihai. Faza 1, 01.11-08.11.2026. Gata de revizuire.

Aici stabilim ce problemă rezolvă OCRInvoice, pentru cine și unde se oprește sistemul. Domeniul și
proiectarea vin în etapele următoare.

## Problema

Bonurile, chitanțele și facturile se pierd, iar cine vrea să știe cât a cheltuit trebuie să le adune
și să le treacă de mână. Puțini au răbdare pentru asta. Așa ajung să nu știe cât au cheltuit într-o
lună, dacă stau mai bine decât luna trecută și pe ce s-au dus banii.

OCRInvoice citește automat datele de pe document și îi cere utilizatorului să verifice doar ce e
nesigur. Un document ale cărui sume nu se potrivesc nu poate fi salvat. Documentele salvate sunt
puse pe categorii.

## Fișierele

| Fișier | Ce găsești acolo |
|--------|------------------|
| [01-beneficiari-si-obiective.md](01-beneficiari-si-obiective.md) | Cine folosește sistemul și ce urmărim |
| [02-limitele-sistemului.md](02-limitele-sistemului.md) | Ce intră în nucleu, ce rămâne pe dinafară și cu ce sisteme externe lucrăm |
| [03-cerinte.md](03-cerinte.md) | Cerințele funcționale și nefuncționale, fără detalii de implementare |
| [04-ipoteze-si-intrebari.md](04-ipoteze-si-intrebari.md) | Regulile stabilite, separat de ipoteze, întrebări deschise și propuneri AI |
| [05-exemple-de-acceptare.md](05-exemple-de-acceptare.md) | Cinci exemple concrete, cu rezultatul așteptat |
| [06-schimbarea-unei-cerinte.md](06-schimbarea-unei-cerinte.md) | Ce se schimbă în analiză dacă se schimbă o cerință |

## Câțiva termeni

Glosarul complet îl face etapa de domeniu. Până atunci, în fișierele de aici folosim:

- document: un bon, o factură, o chitanță sau o cheltuială trecută de mână;
- produs: o linie de pe document, cu denumire, sumă și categorie;
- valoare de verificat: o valoare pe care motorul OCR a citit-o cu siguranță sub 0,8;
- confirmare: salvarea documentului după verificare. Un document confirmat e un document salvat.

## Etichete

Fiecare cerință și regulă are una dintre etichetele de mai jos.

- Stabilit: e hotărât pentru produs.
- Ipoteză: presupunem că e așa și spunem ce se schimbă dacă nu e.
- Întrebare: nu știm încă, trebuie să decidă cineva.
- Propunere AI: o idee venită de la asistentul AI, pe care echipa n-a discutat-o încă.

Exemplele de acceptare sunt propuse. Nu le-am rulat.

> Am lucrat la ciornă cu un asistent AI, în rol de analist. Revizuirea limitelor și a ipotezelor se
> face separat, într-o conversație nouă (vezi [../revizuiri/handoff-faza-1.md](../revizuiri/handoff-faza-1.md)).
