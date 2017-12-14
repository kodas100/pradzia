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
- Grubiai eSveikata darbai prasidėjo nuo NESS1 ir NESS2 projektų dar 2005-2011 laikotarpyje. Pradėta buvo, užbaigta ne. Projektas palaidotas. Suinvestuota apie 9mln. EUR
- 2011-2015 laikotarpyje buvo pradėta dirbti su esama eSveikata, tam skirta iš EU apie 26mln. EUR. Šiame laikotarpyje vienaip ar kitaip atsirado šios grandys: ESPBI, E-receptas, MeDVais ir kt.
- Iš esmės finansavimą gavus 2011 darbai buvo pradėti 2013 metų paskutiniame ketvirtyje. T.y. NORTAL laimi konkursą ESPBI kūrimui.
- 2015 metais darbus priduoda.
- 2016 metais SAM vėl gauna EU paramą 28mln. EUR, kur juos panaudoti dar nenuspręsta. Terminas baigiasi 2020 metais.

NORTAL pusė:
- Darbai buvo atlikti pagal ESPBI IS specifikaciją (kaip ji surašyta mes jau spėjom susipažinti). T.y. iš esmės patenkintas interesas, darbai priduoti liko garantinis.
- Garantinis už kurį buvo sumokėta papildomai baigiasi kitų metų antrame ketvirtyje.
- Ligoninėms pradėjus naudotis ESPBI ir HIS išlindo bėdos, kurios iki šios dienos nėra sutvarkytos. Kodėl? Nes tai nėra garantiniai darbai. Iš esmės didžioji dalis darbų nurašomi palaikymui, optimizavimui ir jų niekas neatlieka. Jei kas nors nori, kad jie būtų atlikti, turi susimokėti ir tai tiesioginė ligoninių ir kitų suinteresuotų šalių atsakomybė. Mokėti nenori. Kodėl? Sužinosim paklausę, prielaidų šiame etape nedarysim. Išklausėme tik vieną pusę.

Ar ten tikrai yra bug’ai, ar plėtiniai sužinosime priėję prie sistemos.

Pastaba:  
Kalbėti apie techninius klausimus Nortal nebuvo linkę, sakydami, jog tai neaktualu. Kad kai ką galima pataisyti savaičių bėgyje, bet jiems tai elementariai nepriklauso. Žodžiu laukiam kol pasibaigs garantinis. Atsiprašau už grubų išsireiškimą, bet skamba taip.

Grėsmė:
- Nortal pasibaigus garantiniam laikotarpiui ir iš jų neužsakant palaikymo, galimybių dirbti Lietuvoje nemato. Viskas tvarkoj. Tai privatus verslas, jis žiūrės savo intereso.
- Pozicija dėl RC, kurie yra ESPBI, MeDVais ir E-recepto užsakovai, bei prižiūrėtojai buvo gana palanki, bet ne sykį pastebėta, kad jei jiems pritrūks resursų ar specialistų, viskas grius, bent jau taip mano Nortal Lietuvos padalinio darbuotojas. Tad tikrosios situacijos reiktų palaukti. Ar galima daryti prielaidą, jog 2018 metais eSveikata išnyks kaip išnyko NESS1 ir NESS2? Paliekam klausimą atvirą.


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
