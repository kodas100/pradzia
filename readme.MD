# KODAS 100
Kodas 100 yra visuomeninė iniciatyva skirta pagerinti Lietuvos sveikatos apsaugos informacinę sistemą ir sukurti pagrindą kitų Lietuvos informacinių sistemų tobulinimo iniciatyvoms.
https://kodas100.lt

## Įvadas
Ši iniciatyva gimė matant kaip neefektyviai tvarkomas valstybinis IT ūkis. Išleidžiama 40 mln. eurų. Sukuriama sistema, kuri net po pusės metų po paleidimo stringa.

Pradiniame etape buvo pastebėti šie dabartinės sistemos trūkumai: interoparability - Dauguma sveikatos sistemos įstaigų neprisijungia arba turi savo sistemą, kuri neprijunta; sistemos greitis -  kuo daugiau receptų asmeniui yra išrašyta anksčiau, tuo ilgiau krauna. Dideli duomenų bazės (Oracle) palaikymo kaštai.
Projekto metu bus bandoma įsigilinti į suinteresuotų šalių poreikius, sistemos trūkumų priežastis bei pasiūlyti sistemos patobulinimus, kurie darbą su sistema padarytų spartesnį:
* "User experience" patobulinimai - net jei sistema lėta, jeigu užduočių atlikimui reikalinga mažiau žingsnių - galutinio vartotojo UX pagerėja.
* Techninės optimizacijos - pataisymai galintys atnešti didžiausią spartos prieaugį investuojant mažiausiai lėšų/laiko (neoptimalių užklausų patobulinimas, nebūtinų nuotolinių užklausų optimizavimas (pvz. atliekant tik po pareikalavimo iš vartotojo) it pan.)
* Serverinės optimizacijos - duomenų bazės, OS ir kitų komponentų konfigūracijos patobulinimai leidžiantys geriau išnaudoti turimą tech. įrangą.
* Kaštų optimizacijos - brangių/perteklinių komponentų pakeitimas atviro kodo analogais (jau minėta Oracle -> PostgreSQL migracija)
* Darbo optimizacijos - neautomatizuotų procesų palengvinimas ar automatizavimas (rodos minėta, kad gydytojai po darbo turi atlikti veiksmus su tos dienos vizitais - galbūt galima pasidomėti, kiek iš tų darbų būtų galima automatizuoti)

## Kodas 100 - Tikslas 
Atnaujinti Lietuvos sveikatos apsaugos informacinę sistemą.
Šis projektas - pavyzdys, kaip visuomenė gali prisidėti prie valstybės atviro kodo IT sistemų kūrimo.

## Roadmap
1. Sukurti svetainę, kurioje pateikiama informacija, kas per iššūkis, kokie tikslai, terminai.
2. Užtikrinti vyriausybės pagalbą, kad piliečių pagalba būtų priimta.
3. Suformuoti modernius IT sistemų kūrimo principus. (Open source pvz. github'e ir tt)


## PLANAS A: IŠŠŪKIS PRIIMAMAS (darbai)

1. Išnagrinėti specifikacija.
1. Surasti kontaktus galinčius supažindinti su projekto teisiniais ir techniniais aspektais.
1. Susipažinti su technologijomis naudotomis kuriant sistemą.
1. Surinkti komandą turinčią patirties dirbti su naudojamomis ar analogiškomis technologijomis.
1. Pasiskirstyti atsakomybėmis ir darbais/sritimis (UX, kodo optimizacijos, serverio optimizacijos, kaštų optimizacijos ir t.t.) 
   * Išsiaiškinti pagrindinius naudotojų poreikius ir nusiskundimus (UX sritis)
   * Išsiaiškinti pagrindinius "karštuosius taškus" sistemose (kodo optimizavimo sritis)
   * Atlikti serverių resursų, apkrovų ir konfigūracijų auditą (serverio sritis)
   * Įvertinti Oracle ir Postgresql suderinamumą bei galimybę migruoti (kaštų sritis)
   * Pasinaudojant UX srities žmonių atradimais ir įžvalgomis įvertinti galimybę automatizuoti dalį užduočių (darbo sritis)
1. Dirbti iteracijomis (Išsigryninti smulkius tikslus, dirbti ties jų įgyvendinimu, reguliariai susitikti aptarimui - ir vėl išsigryninti sekančius smulkius tikslus).
   
## Kodas 100 Komanda
- Paulius Rimavičius.
- Justina Marija Jančiauskienė. Community manager (Bendruomenes vadove/koordinatore/globėja>)
- (Kokiu budu patenkama?)


## Suinteresuotos šalys

1. Jaunųjų gydytojų asociacija (JGA)
2. Sveikatos apsaugos ministerija
3. VUL SK (?)
4. Registru centro sveikatos skyrius. Skyriaus vedėja Audronė Ciesiūnienė http://bit.ly/2iLUrc6. 
5. EuroRec http://www.eurorec.org/

# Situacijos analizė

## Registrų Centro paaiškinimai
1. Sistema veikia REST api pagrindu, naudojamas FHIR(HL7)[https://en.wikipedia.org/wiki/Health_Level_7] (medicininiams duomenims skirtas) REST formatas. Problema, kad darant užklausas per REST nėra ribojamas duomenų kiekis, t.y. galima suformuoti užklausą, kuri gražina visus duomenis, nėra nustatytas joks maksimalus LIMITAS. Tokios užklausos pjauna DB. Išorinės sistemos kurios jungiasi prie API, kurių yra apie 30, tiesiog laiks nuo laiko "užmuša" DB. 
2. Sistemos gamintojas suprojektavo sistemą taip, kad gavus kažkokią užklausą į REST api, ta užklausa yra konvertuojama į SQL užklausą, t.y. nėra individualių SQL užklausų, kurias galima būtų tiuninti.
3. Yra keletas lentelių, į kurias yra "loginama" visi vartotojų veiksmai (na toks savotiškas logas į DB, kas labai smarkiai užkrauna DB), ir vartotojai daro SELECT'us iš tų lentelių, kad gautų prieigos teises. Gaunasi, kad sistema, norėdama užtikrinti, ar vartotojas gali pasiekti kažkokią informaciją, turi daryti FULL SCAN per lentelę iš 100 milijonų įrašų (O tų įrašų kiekis kaupiasi eksponentišai, po kelių mėn. gali būti ir milijardas įrašų).
4. RC viską iš esmės nori spręsti pirkdami naujus core'us, naujas licencijas ir tt.

Kiti duomenys, ką pavyko surinkti:
- Šiuo metu naudojami 3 fiziniai Oracle DB serveriai, po 6 core'us, Enterprise licencijos (standartinė kaina $50k). 3x6x50k = $900k už licencijas. Šiuo metu vyksta/vyko konkursas nupirkti naujų core'ų ir naujų Oracle DB licencijų.
- Platforma: JAVA SPRING ir kiti JAVA framework'ai, hibernate ORM.
- Galėtumėm gauti labiausiai stabdančias "Slow queries", per ministeriją (nepasižimėjau kurią).
- Concurrent user'ių būna iki kelių šimtų vienu metu.
- Kiekvieną dieną RC veikimo ataskaitą siunčia į ministeriją, pej jie pasidalintų galėtumėm gauti. Bandėm įrodyti, kad gal viešai tiesiog tą statistiką įdėtų, nesėkmingai.

## Sistemos naudotoju komentarai
Svarbu surinkti sistemos naudotojų komentarus.

> Sveiki. Esu VUL SK gydytojas neurologas ir Jaunųjų gydytojų asociacijos (JGA) valdybos narys. JGA be galo džiaugiasi šia IT specialistų iniciatyva. E. sveikatos tema susidomėjome daugiau nei prieš metus, kadangi tarp asmens sveikatos priežiūros įstaigų informacinių sistemų skirtumai yra astronominiai, ir laisvu nuo darbo metu į e. sveikatos temą gilinamės bei stengiamės teikti racionalius pasiūlymus SAM. Deja, dėl įvairių priežasčių absoliučiai nematome lyderystės. Jau daugiau nei metus sekame E. sveikatos valdybos SAM veiklą, o nuo 2017 m. birželio esame į traukti į pačią valdybą, tad pradedame suprasti užkulisius. Mes iškėlėme Lietuvos vyriausiojo e. sveikatos architekto idėją, taip pat siekėme, kad būtų įkurtas e. sveikatos kompetencijų centras. Savo iniciatyva pavasarį buvome nuvykę į Estiją, kur bendravome su beveik visais svarbiausiais eHealth stakeholder'iais, susidarėme gerą įspūdį apie pačią Estų e. sveikatos sistemą, pradėjome aktyvų bendradarbiavimą. Visus pokalbius esame nufilmavę. Prieš mėnesį pasikvietemė estus, kad pasidalintų savo įspūdžiias su SAM ir E. sveikatos valdyba. Rugsėjį buvau nuvykęs į Kopenhagą, paprašiau kad Pasaulio sveikatos organizacijos atsakingi asmenys peržiūrėtų ir pateiktų pasiūlymus naujai ruošiamam Lietuvos E. sveikatos plėtros priemonių planui. Bandėme įtraukti IT specialistus, tačiau nesisekė - pats savo iniciatyva organizavau Oxbridge'o absolventų, INFOBALT ir kitų IT specialistų vizitą susipažinti su kasdieniu gydytojo darbu VUL SK ir ten naudojama ELI sistema, nuvykome į jungtinį inovatyvios medicinos centrą, kur pabendravome su ją kūrusiais IT specialiastais, po to į Registrų centrą, kurie pasakojo apie ESPBI IS, taip pat į ligonių kasą, kuri turi SVEIDRA sistemą. Deja, didesnio IT specialistų susidomėjimo nesulaukėme - dėl to esame be galo laimingi, kad iniciatyva pradeda rastis jūsų pačių bendruomenėje. Todėl kaip jaunieji gydytojai labai norėtume pasidalinti savo įžvalgomis apie dabartinę e. sveikatos situaciją ir pasiūlymais, kuriuos patys esame suformulavę po vizito į Estiją. Kadangi patys "įsiprašėme" į E. sveikatos valdybą, manau, kad mūsų kaip vartotojų ir jūsų kaip kūrėjų bendruomenės turi labai rimtų taškų bendradarbiauti.

> Dėl lėtai veikiančios sistemos, vienos vaistininkės/vaistinės vedėjos manau naudingas pastebėjimas nustatant "diagnozę", kad kuo daugiau receptų asmeniui yra išrašyta anksčiau, tuo ilgiau krauna. Jei pvz zmogus pirma karta perka pgl el.receptą, tai užkrauna žymiai greičiau. O jei jau pirko kokius 8 kartus ir dar išrašyti kokie 3 receptai, tai be 15 min neužkraus...ir dar pridursiu, kad nuo užpraeito ketvirtadienio sakė jau nebuvo dienų kad išvis neužkrautų (kas vaistininkams jau didžiulė laimė). (Laima Šidlauskienė)


# Projekto trūkumų išgryninimas
Šioje dalyje siūlyčiau eiti prie esminių problemų gryninimo. 
1. Interoperability
2. Sistemos greitis
3. Neefektyvūs programinės įrangos (duomenų bazės) pasirinkimas. Analizė: http://nbviewer.jupyter.org/gist/sirex/13420936108549cea62668521dedaffe

4. Nepakankamas suinteresuotų šalių įtraukimas į projekto valdymą. M. Zimnickas: "Projektas nebuvo sekmingas, kadangi projekto valdyme daugiausiai dalyvavo biurokratai" siūlo grupes kuriose būtų atstovaujamos įvairios šalys. https://www.facebook.com/groups/1972865706318006/permalink/1973702002901043/ 


# Kitos idėjos ir pasiūlymai.
Čia dedame dar patvirtinimo/palaikymo negavusias idėjas.
- Code4Vilnius. Organizatorių (Povilas Poderskis) patirtis
- Darius Barušauskas. Concept to Clinic Open Source challenge. https://www.facebook.com/groups/1972865706318006/permalink/1973643686240208/
- http://www.eurorec.org/
- Svetainėje būtinai laikrodukas, per kuri laiką iššūkį reikia priimti arba atmesti

# Nuorodos
ELEKTRONINĖS SVEIKATOS PASLAUGŲ IR BENDRADARBIAVIMO INFRASTRUKTŪROS INFORMACINĖ SISTEMA
- https://sam.lrv.lt/uploads/sam/documents/files/Veiklos_sritys/E.%20sveikata/El._sveikatos_paslaugu_ir_bendradarbiavimo_infrastrukturos_IS/ESPBIISspecifikacija.pdf
- https://sam.lrv.lt/lt/veiklos-sritys/e-sveikata/elektronine-sveikatos-paslaugu-ir-bendradarbiavimo-infrastrukturos-informacine-sistema

# Kodas 100 žiniasklaidoje
- https://sam.lrv.lt/lt/veiklos-sritys/e-sveikata/elektronine-sveikatos-paslaugu-ir-bendradarbiavimo-infrastrukturos-informacine-sistema
