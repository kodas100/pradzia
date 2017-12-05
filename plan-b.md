## Planas B
Šis planas galioja tuomet jeigu esamos sistemos pernaudojamumas yra per mažas ir yra protingiau/pigiau mažais žingsniais sukurti sistemą iš naujo.
Taip būtų sukuriama reali vertė, nes sistema galėtų daug greičiau pradėti veikti ir padėti realiems žmonėms.

### Problemos (prielaidos)

 - Dabartinė specifikacija yra abstrakti irparašyta ne technine, o biurokratų/teisine kalba. Todėl iš jos negalima suprasti ką ir kodėl kuriama sistema turės daryti, bei kaip su ja dirbs vartotojai. 
 - Sistema yra lėta, dėl netinkamos architektūros, bottleneck'ų kode.
 - Sistema yra monolitinė, jos kodas nemobilus, sunkiai plečiamas (???).
 - Sistema yra nepatogi naudotojams (gydytojams, vaistininkams), nes buvo kuriama neatsižvelgus į jų poreikius.
 - Sistemos palaikymas brangus dėl pasirinktų enterprise-level technologijų, ir jo nėra išnaudojamos pagal galimybes.

### Kertiniai momentai:

 - Sistema turėtų būti perprojektuota įsigilinant į galutinių vartotojų problemas ir realiai jas spręsti - t.y. jiems padėti, o ne pridaryti rūpėsčių.
 - Visos atskiros sistemos dalys turi būti modulinės - t.y. veikti nepriklausomai ir prie jų galetų dirbti nepriklausomos komandos.
 - Infrastruktūra paremta and mikroservisų architektūros ir autoscaling'o tam, kad taupyti resursus (Darom prielaidą jog naktį sistema naudosis mažiau, todėl gali būti mažiau ją palaikančių serverių) 
 - Visas tech-stack'as parinktas iš atviro kodo technologijų ir šiuolaikinių framework'ų atsižvelgiant į jų populiarumą (Lietuvoje???)
 - Visas sistemos kodas atviro kodo.

## Siūlomi žingsniai

1. Pasikalbėti su dabartiniais sistemos vartotojais ir iškristalizuoti pačias skaudžiausias vietas - išsiaiškinti sunkiausias problemas. 
2. Shortlistinti problemas, kurias norima išspręsti.
3. Pasidaryti use-case / user-flow scenarijus kaip sistema funkciškai sprendžia šias problemas.
4. Pagal scenarijus sukurti low-fidelity lygio prototipus, kuriuos galėtų įvertinti bendruomenė ir visi suinteresuoti naudotojai.
5. Pagal prototipus padaryti backlog'us, ką tiksliai reikia padaryti. **Parinkti technologijas**
6. Paleisti viešas repozitorijas, tam kad žmonės galėtų commitinti kodą. 
7. Pasiskirstyti backlog'o task'us. 
8. Sukurti testinę aplinką cloud'e, kad visi galėtų bandytis integracijas ir matyti baseline resultatą (???)
