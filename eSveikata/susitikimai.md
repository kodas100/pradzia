# Susitikimai su suinteresuotais asmenimis

## 2017-12-13 - Nortal

https://docs.google.com/document/d/1pcmXNmpxjIstOkc9cpuOhdhW7gVw98KexxPiH8C945k/edit?usp=sharing

Dalyviai:
- Donatas Prialgauskas #kodas100 projekto vadovas
- Justina Jančiauskienė #kodas100 bendruomenės vadovė
- Arūnas Baubinas - load integration consultant
- Laura Šinkūnaitė - JGA narė (suinteresuota eSveikata, dirbanti LSMU Kauno klinikų neurologijos rezidente)
- Andrius Šimėnas - eHealth team leader

Tikslas: pristatymas kodas100, kaip veikiame, veiklos modelis, bendradarbiavimo galimybės su Nortal.

Rezultatai:
- ...

## 2017-12-06 - Registrų centras

Dalyviai:
- Paulius Rimavičius
- Donatas Prialgauskas
- ...
- ...
- ...

Tikslas - ...

Rezultatai:
- Sistema veikia REST api pagrindu, naudojamas FHIR(HL7)[https://en.wikipedia.org/wiki/Health_Level_7] (medicininiams duomenims skirtas) REST formatas. Problema, kad darant užklausas per REST nėra ribojamas duomenų kiekis, t.y. galima suformuoti užklausą, kuri gražina visus duomenis, nėra nustatytas joks maksimalus LIMITAS. Tokios užklausos pjauna DB. Išorinės sistemos kurios jungiasi prie API, kurių yra apie 30, tiesiog laiks nuo laiko "užmuša" DB.
- Sistemos gamintojas suprojektavo sistemą taip, kad gavus kažkokią užklausą į REST api, ta užklausa yra konvertuojama į SQL užklausą, t.y. nėra individualių SQL užklausų, kurias galima būtų tiuninti.
- Yra keletas lentelių, į kurias yra "loginama" visi vartotojų veiksmai (na toks savotiškas logas į DB, kas labai smarkiai užkrauna DB), ir vartotojai daro SELECT'us iš tų lentelių, kad gautų prieigos teises. Gaunasi, kad sistema, norėdama užtikrinti, ar vartotojas gali pasiekti kažkokią informaciją, turi daryti FULL SCAN per lentelę iš 100 milijonų įrašų (O tų įrašų kiekis kaupiasi eksponentišai, po kelių mėn. gali būti ir milijardas įrašų).
- RC viską iš esmės nori spręsti pirkdami naujus core'us, naujas licencijas ir tt.
- Šiuo metu naudojami 3 fiziniai Oracle DB serveriai, po 6 core'us, Enterprise licencijos (standartinė kaina $50k). 3x6x50k = $900k už licencijas. Šiuo metu vyksta/vyko konkursas nupirkti naujų core'ų ir naujų Oracle DB licencijų.
- Platforma: JAVA SPRING ir kiti JAVA framework'ai, hibernate ORM.
- Galėtumėm gauti labiausiai stabdančias "Slow queries", per ministeriją (nepasižimėjau kurią).
- Concurrent user'ių būna iki kelių šimtų vienu metu.
- Kiekvieną dieną RC veikimo ataskaitą siunčia į ministeriją, pej jie pasidalintų galėtumėm gauti. Bandėm įrodyti, kad gal viešai tiesiog tą statistiką įdėtų, nesėkmingai.
