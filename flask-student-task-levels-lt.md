# Studentų užduotis su lygmenimis

Sukurti Flask programą, kuri simuliuotų universiteto paskaitų registraciją tiek studentams, tiek dėstytojams. T.y., būtų galima prisiregistruoti prie esamų paskaitų studentams, ir nurodyti kurias paskaitas dėstytojai dėsto

## Level 1 (Pagrindai)
- Susikurti projekto struktūrą pagal atmintinę
- Susikonfiguruoti projektą `__init__.py` faile pagal atmintinę ir senus projektus
- Pasiimti `base.html` iš senų projektų, pakeisti atitinkamai užduočiai (sukurti studentų, dėstytojų, paskaitų įrašus navbare)
- Nenaudoti sqlalchemy duomenų bazių, vietoj to naudoti tik mock data dictionary, kuriuos nukopijuoti į `models.py` (vėliau į šį failą sudėsime duombazių modelius/lenteles)
```
students =[{
    'name': 'Jonas',
    'surname': 'Jonaitis'
},
{
    'name': 'Petras',
    'surname': 'Petraitis'
},
{
    'name': 'Auste',
    'surname': 'Austaityte'
},
{
    'name': 'Igne',
    'surname': 'Ignaityte'
}]

professors =[{
    'name': 'George',
    'surname': 'Washington',
    'experience': 12
},
{
    'name': 'Valdas',
    'surname': 'Adamkus',
    'experience': 25
},
{
    'name': 'Antanas',
    'surname': 'Smetona',
    'experience': 100
},
{
    'name': 'Jonas',
    'surname': 'Kubilius',
    'experience': 2
},
{
    'name': 'Algis',
    'surname': 'Algiauskas',
    'experience': 3
}]

lectures =[{
    'title': 'Introduction to Modal Logic'
},
{
    'title': 'Molecular Biology'
},
{
    'title': 'History of Lithuania'
},
{
    'title': 'Epidemiology'
}]
```
- Sukurti tris maršrutus kurie pasiimtų visus esančius duomenis iš paprasto atitinkamo dictionary (nurodyto žemiau) ir išrašytų kiekvieną įrašą atitinkamuose puslapiuose
- Sukurti tris atitinkamus templates, kurie gautų duomenis iš maršrutų funkcijų ir išrašytų visus įrašus kaip paragrafus ar sąrašus (`<ul>`)

## Level 2 (Duomenų saugojimas duombazėse)
- Sukurti DB modelius/lenteles studentams, dėstytojams, paskaitoms
- Ranka (per sqlalchemy ar per raw SQL) įrašyti tuos pačius duomenis į sukurtą DB failą 
- Išrašyti tuos duomenis atitinkamuose svetainės puslapiuose naudojant DB

## Level 3 (Duomenų įrašymas per formas)
- Pridėti Flask formas (naudojant pvz. Flask WTForms), per kurias būtų įmanoma išsaugoti studentus, dėstytojus ir paskaitas
- Atvaizduoti naujus, per formas įrašytus duomenis atitinkamuose puslapiuose

## Level 4 (Daugiaskaitiniai kintamieji duombazėse)
- Perkurti DB (nepamiršti išrinti senos arba daryti migraciją):
  - Kiekvienam dėstytojui leistų priskirti jo paskaitas (one2many ryšys)
  - Kiekvienam studentui leistų priskirti daug paskaitų (many2many ryšys)
- Vėlgi prisidėti naujų duomenų kaip ir level 2, bet dabar pridedant reikšmes į daugiaskaitinius kintamuosius

## Level 5 (Daugiaskaitiniai pasirinkimai ir validatoriai formose)
- Pakeisti studentų formą, kad būtų galima pasirinkti daug paskaitų (QuerySelectMultipleField)
- Pakeisti paskaitų formą, kad būtų galima pasirinkti daug studentų (QuerySelectMultipleField) vieną dėstytoją (QuerySelectField)
- Pakeisti dėstytojų formą, kad būtų galima pasirinkti daug paskaitų (QuerySelectMultipleField)
- Pridėti validatorius formose, jei dar to nepadarėte (pvz. būtina įrašyti vardus ir pavardes studentams ir dėstytojams, pavadinimą paskaitoms)

## Level 6 (Duomenų redagavimas) 
- Padaryti, kad būtų galima ištrinti dėstytojus, paskaitas, studentus
  - Paspaudus pvz. "Ištrinti dėstytoją" mygtuką, dėstytojo įrašas turi būti ištrintas iš duomenų bazės
- Padaryti, kad būtų galima redaguoti dėstytojus, paskaitas, studentus
  - Paspaudus pvz. "Redaguoti dėstytoją", turime būti nukreipti į tokią pačią formą, naudotą dėstytojo įrašo sukūrimui, bet kuri jau būtų užpildytą su to dėstytojo informacija 
  - Potencialiai pakeitus informaciją esame nukreipiami į dėstytojų puslapį, kur matome pakeistus duomenis

