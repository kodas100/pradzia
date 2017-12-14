
## Projekto specifikacijos analizė 
ESPBI    
- Elektroniniai sveikatos įrašai ir jų mainai
- Siuntimai (konsultuoti / gydyti / tyrimams / reabilitacija)
- Mėginių registravimas ir identifikavimas
- Pacientino registravimas / išregistravimas prie ASPĮ (asmens sveikatos priežiūros įstaiga)
- Išankstinė paciento registracija (vizitams)
- Prieigos prie metodinės pagalbos priemonių suteikimas sveikatinimo specialistams gydymo sprendimų priėmimo metu
- E nedarbingumo pažymėjimai / nėštumo bei gimdymo atostogų pažymėjimai
- Ataskaitos
- E-receptas    
- E-recepto išrašymas
- Vaistų / med priemonių / centralizuotų vaistų išdavimas pagal receptą
- Paciento informacija apie jam išrašytus receptus

medVAIS    
- Medicininių vaizdų paėmimas iš ASPĮ ir saugojimas
- Medicininių vaizdų pateikimas peržiūrai
    
Būtinos integracijos    
- 35 ir 221 psl
- LGR (Lietuvos gyventojų registras)
- METAS (Medicinos elektroninė tobulinimo administravimo sistema)
- DPSDR (draudžiamųjų privalomuoju sveikatos draudimu registras)
- VAPRIS (vaistinių preparatų informacinė sistema)
- iDrug
- SODRA IS
- JAR

# Nefukciniai reikalavimai
- LifeRay frameworkas		
- Oracle DB		
- Fhir DSTU1 + atom feed		
		
- GDPR		
	- Pateikti pacientui informaciją, kuri laikoma IS	
	- Pateikti informaciją pacientui, kas matė kokius jo duomenis	
	- Šifruota duomenų bazė (tikrus duomenis gali matyti tik autorizuoti asmenys)	
- Informacija pasiekiama per API (ligoninėms, turinčioms vidines sistemas) / WEN interface (tiems, kas neturi vidinių sistemų)		
- Paciento duomenis vietoj paciento gali peržiūrėti jo įgaliotas asmuo (sutuoktinis / tėvai)		
