# Ce se întâmplă dacă se schimbă o cerință

Am luat două schimbări care s-ar putea cere. Prima atinge multe lucruri, a doua aproape nimic.
Pentru fiecare notăm ce cerințe, reguli și exemple se schimbă și ce rămâne la fel. Efectul asupra
proiectării îl analizează etapa de verificare.

## S-01. Confirmarea permisă și când totalul nu se potrivește

Schimbarea: utilizatorul poate confirma un document chiar dacă produsele adunate nu dau totalul, cu
condiția să accepte explicit diferența. De ce s-ar cere: pe unele bonuri motorul OCR sare peste un
produs, iar utilizatorul nu are chef să caute linia care lipsește.

| Ce se atinge | Cum se schimbă |
|--------------|----------------|
| R-03 | Confirmarea o mai blochează doar valorile de verificat. Diferența de total nu o mai blochează |
| CF-05, CF-06 | Diferența rămâne afișată. Apare o cerință nouă: documentul ține minte diferența acceptată și faptul că a fost acceptată |
| O-02 | Nu mai e garantat. Devine „în evidență nu intră documente cu sume care nu se potrivesc decât dacă utilizatorul a acceptat explicit diferența” |
| R-09 | Nu mai ține. Totalul lunii adună totalurile documentelor, iar categoriile adună produsele, deci diferența acceptată nu ajunge în nicio categorie. Ar trebui o regulă nouă, de exemplu ca diferența să intre la Altele |
| EA-03 | Se rescrie. Andrei acceptă diferența de 3,00 lei și confirmă. Totalul lunii crește cu 28,68 lei, dar categoriile doar cu 25,68 lei, dacă nu adoptăm regula de mai sus |
| EA-05 | Contabilul ar trebui să vadă în export ce documente au o diferență acceptată. Asta e o întrebare nouă |
| Ce rămâne la fel | Încărcarea, extragerea, valorile de verificat (CF-04), confidențialitatea și cheltuiala manuală |

R-03 e deci o decizie centrală. Dacă o slăbim, se schimbă un obiectiv, o regulă a statisticilor, două
exemple și invariantul pe care îl propunem pentru proiectare: „un document confirmat are totalul egal
cu produsele adunate”.

## S-02. Pragul de siguranță urcă de la 0,8 la 0,9

| Ce se atinge | Cum se schimbă |
|--------------|----------------|
| R-02, CF-04 | Se schimbă doar valoarea pragului |
| EA-01 | Nu mai e un bon citit clar. Plata (0,88) și denumirea DETERGENT (0,89) ajung de verificat, iar confirmarea e blocată până le corectează Andrei |
| Ce rămâne la fel | Restul cerințelor, regulile R-03 la R-09 și forma exemplelor |

Pe hârtie efectul e mic, dar utilizatorul îl simte: are mai multe valori de verificat, deci mai mult
de lucru, iar O-01 se atinge mai greu. Dacă pragul ar deveni o setare, I-08 nu mai ține.
