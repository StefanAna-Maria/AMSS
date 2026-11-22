# Proiectarea sistemului

Autor: Luisa Frincu. Faza 3, 15.11-22.11.2026. Ciornă, înainte de revizuire.

Aici împărțim responsabilitățile sistemului OCRInvoice în componente logice, delimităm granițele cu
sistemele externe, formulăm invarianții și contractele operațiilor, definim stările și tranzițiile
documentului și propunem decizii pentru întrebările rămase deschise. Pornim de la
[../01-problema/](../01-problema/) și [../02-domeniu/](../02-domeniu/). Nu alegem tehnologii, baze
de date, framework-uri sau clase de cod.

## Fișierele

| Fișier | Ce găsești acolo |
|--------|------------------|
| [01-responsabilitati.md](01-responsabilitati.md) | Cele 6 componente logice (`C-01`–`C-06`), dependențele dintre ele și justificarea granițelor |
| [02-granite-sisteme-externe.md](02-granite-sisteme-externe.md) | Contractele și tratarea eșecurilor pentru Motorul OCR, SAGA și Serviciul de email |
| [03-contracte-si-invarianti.md](03-contracte-si-invarianti.md) | Invarianții sistemului (`INV-01`–`INV-06`) și contractele operațiilor (`OP-01`–`OP-06`) |
| [04-stari-si-tranzitii.md](04-stari-si-tranzitii.md) | Diagrama de stări, tranzițiile permise (`TR-01`–`TR-10`), tranzițiile interzise și alegerea pentru `Q-02` |
| [05-decizii-proiectare.md](05-decizii-proiectare.md) | Deciziile de proiectare (`DP-01`–`DP-05`), alternativele respinse și ce rămâne pentru Faza 4 |

## Pe scurt

1. Sistemul este împărțit în 6 componente logice (`C-01`–`C-06`) cu dependențe fără cicluri, separând
   fluxul documentelor neconfirmate (`C-02`) de evidența confirmată (`C-04`).
2. Cele trei sisteme externe (Motorul OCR, SAGA, Serviciul de email) sunt izolate în spatele unor
   componente dedicate (`C-03`, `C-06`, `C-01`), cu contracte clare și tratare explicită a eșecurilor.
3. Corectitudinea datelor și izolarea între conturi sunt păzite prin 6 invarianți (`INV-01`–`INV-06`)
   și 6 contracte de operații (`OP-01`–`OP-06`) cu precondiții, postcondiții și cazuri de eșec.
4. Ciclul de viață al documentului acoperă cele 5 stări din domeniu (`Încărcat`, `În procesare`,
   `De verificat`, `Confirmat`, `Eroare`), prin 10 tranziții permise (`TR-01`–`TR-10`) și un set
   explicit de tranziții interzise.
5. Întrebările lăsate din etapele anterioare pentru Faza 3 (`Q-01`–`Q-05`, `Q-08`) primesc propuneri
   de proiectare cu alternative evaluate (`DP-01`–`DP-05`), marcate `Propunere AI` până la decizia
   echipei.

## Etichete și identificatori

Păstrăm etichetele din [../01-problema/README.md](../01-problema/README.md): `Stabilit`, `Ipoteză`,
`Întrebare` și `Propunere AI`. Cerințele și regulile preluate își păstrează eticheta din sursă, iar
deciziile noi de proiectare sunt marcate `Propunere AI`.

Identificatorii noi din această etapă:

- `C-xx`: componentă logică, în [01-responsabilitati.md](01-responsabilitati.md);
- `OP-xx`: contract de operație, în [03-contracte-si-invarianti.md](03-contracte-si-invarianti.md);
- `INV-xx`: invariant al sistemului, în [03-contracte-si-invarianti.md](03-contracte-si-invarianti.md);
- `TR-xx`: tranziție de stare a documentului, în [04-stari-si-tranzitii.md](04-stari-si-tranzitii.md);
- `DP-xx`: decizie de proiectare (`Propunere AI`), în [05-decizii-proiectare.md](05-decizii-proiectare.md).

> Am lucrat la ciornă cu un asistent AI, în rol de proiectant. Revizuirea se face separat, într-o
> conversație nouă (vezi [../revizuiri/handoff-faza-3.md](../revizuiri/handoff-faza-3.md)).

