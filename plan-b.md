## Planas B

Šis planas galioja tuomet, jeigu esamos sistemos pernaudojamumas yra per mažas ir yra protingiau/pigiau mažais žingsniais sukurti sistemą iš naujo. Taip būtų sukuriama reali vertė, nes sistema galėtų daug greičiau pradėti veikti ir padėti realiems žmonėms.

### Problemos (prielaidos)

 - Dabartinė specifikacija yra abstrakti ir parašyta ne technine, o biurokratų/teisine kalba. Todėl iš jos negalima suprasti ką ir kodėl kuriama sistema turės daryti bei kaip su ja dirbs vartotojai. 
 - Sistema yra lėta dėl netinkamos architektūros, bottleneck'ų ir/ar klaidų kode.
 - Sistema yra monolitinė, jos kodas nemobilus, sunkiai plečiamas (???).
 - Sistema yra nepatogi naudotojams (gydytojams, vaistininkams, pacientams), nes buvo kuriama neatsižvelgus į jų poreikius.
 - Sistemos palaikymas brangus dėl pasirinktų enterprise-level technologijų (ir jos nėra išnaudojamos pagal galimybes).

### Kertiniai momentai

 - Sistema turėtų būti perprojektuota įsigilinant į galutinių vartotojų problemas ir realiai jas spręsti - jiems padėti (palengvinti, pagreitinti darbą), o ne pridaryti rūpesčių.
 - Visos atskiros sistemos dalys turi būti modulinės - veikti nepriklausomai ir prie jų galėtų dirbti nepriklausomos komandos ar pavieniai asmenys.
 - Infrastruktūra paremta mikroservisų architektūra ir autoscaling'u tam, kad taupytume resursus (darom prielaidą, jog naktį sistema naudosis mažiau, todėl gali būti mažiau ją palaikančių serverių)
 - Visas tech-stack'as parinktas iš atviro kodo technologijų ir šiuolaikinių framework'ų atsižvelgiant į jų populiarumą (Lietuvoje???)
 - Visas sistemos kodas yra atviras.

## Siūlomi žingsniai

1. Pasikalbėti su dabartiniais sistemos vartotojais ir iškristalizuoti pačias skaudžiausias vietas - išsiaiškinti didžiausias problemas, tikslus.
1. Shortlist'inti problemas, kurias norima išspręsti.
1. Pasidaryti use-case / user-flow scenarijus, kaip sistema funkciškai sprendžia šias problemas.
1. Pagal scenarijus sukurti low-fidelity lygio prototipus, kuriuos galėtų įvertinti bendruomenė ir visi suinteresuoti naudotojai.
1. Pagal prototipus padaryti backlog'us, ką tiksliai reikia padaryti.
1. **Parinkti technologijas**.
1. Sukurti viešas repozitorijas tam, kad žmonės galėtų commit'inti kodą. 
1. Pasiskirstyti backlog'o task'us. 
1. Sukurti testinę aplinką cloud'e, kad visi galėtų bandytis integracijas ir matyti baseline resultatą (???)
