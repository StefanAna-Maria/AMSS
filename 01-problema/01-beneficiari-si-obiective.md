# Beneficiari și obiective

## Cine folosește sistemul

| Beneficiar | Profil | Ce vrea | Ce face în sistem | Etichetă |
|------------|--------|---------|-------------------|----------|
| Persoana fizică (de exemplu Andrei, angajat) | B2C | Să știe cât cheltuie pe lună și pe ce, fără să tasteze | Fotografiază sau încarcă documente, verifică valorile nesigure, se uită la totaluri și categorii | Stabilit |
| Administratorul firmei (de exemplu Ioana, care are o firmă mică) | B2B | Să aibă toate documentele firmei într-un loc și să ajungă la contabil | Încarcă și corectează documentele firmei, cere exportul | Ipoteză |
| Angajatul firmei (de exemplu Radu) | B2B | Să încarce repede bonul de serviciu | Încarcă și verifică documente în contul firmei | Ipoteză |
| Contabilul firmei | B2B, indirect | Documentele lunii într-o formă pe care o poate importa | Nu intră în sistem. Primește exportul și îl importă în SAGA | Ipoteză |

Profilul B2B și exportul către contabil sunt ipoteze ale noastre (I-01 la I-04, în
[04-ipoteze-si-intrebari.md](04-ipoteze-si-intrebari.md)).

## Obiective

| ID | Obiectiv | Pentru cine | Cum verificăm | Etichetă |
|----|----------|-------------|---------------|----------|
| O-01 | Documentul ajunge în evidență fără să tastăm datele de pe el | B2C, B2B | Utilizatorul modifică doar valorile marcate ca nesigure și, dacă totalul nu iese, produsele care explică diferența | Stabilit |
| O-02 | În evidență nu intră documente cu sume care nu se potrivesc | B2C, B2B | Un document confirmat nu mai are valori de verificat, iar produsele adunate dau totalul | Stabilit |
| O-03 | Utilizatorul știe cât a cheltuit și pe ce | B2C | Vede totalul lunii, cât e față de luna trecută și sumele pe categorii | Stabilit |
| O-04 | Documentele firmei ajung la contabil fără să mai fie strânse pe hârtie | B2B | Pentru o lună, firma obține un fișier cu documentele confirmate, pe care contabilul îl poate importa în SAGA | Ipoteză |
| O-05 | Nimeni nu vede documentele altui cont | B2C, B2B | Un document din alt cont se comportă ca și cum n-ar exista | Stabilit (pentru B2B, vezi I-04) |

## Ce nu ne propunem

- Nu înlocuim programul de contabilitate. SAGA rămâne la contabil.
- Nu citim noi textul de pe poză. Asta o face motorul OCR, care e extern.
- Nu facem bugete sau alerte de cheltuieli și nici nu împărțim un bon între mai mulți oameni.
