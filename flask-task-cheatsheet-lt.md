# Užduotis
- Sukurti Flask programą, kuri leistų išsaugoti studentus, dėstytojus ir paskaitas
- Kiekvienam dėstytojui leistų priskirti jo paskaitas (one2many ryšys)
- Kiekvienam studentui leistų priskirti daug paskaitų (many2many ryšys)

Duomenų bazės schema (atreipkite dėmesį į `studentai_paskaitos` pagalbinę lentelę, kuri leidžia padaryti Many2Many ryšį tarp studentų ir paskaitų):

![asd](students-db-schema.jpg)

## Step-by-step

### Teisinga Flask projekto struktūra
- Susikuriame naują projekto direktoriją `students_flask_project`
- Susikuriame naują modulį: naują direktoriją `students_flask` ir `__init__.py` failą joje
- Susikuriame kitus flask `.py` failus ir padedame juos į `students_flask` modulį
- Susikuriame `run.py` failą, kuris bus labai minimalus paleidimo failas
- Galutinė struktūra turėtų atrodyti taip:
```bash
.
├── run.py                     # Failas naudojamas projektui paleisti (app.run)
└── students_flask/            # Mūsų projekto modulis
    ├── forms.py               # Formų klasės (kodas panašus į models.py)
    ├── __init__.py            # Failas su Flask konfiguracija (app, db kintamaisiais)
    ├── models.py              # Duombazių modeliai (kodas panašus į forms.py)
    ├── routes.py              # Maršrutai ir jų logika (templates atvaizdavimas, duomenų siuntimas į templates ir į DB)
    └── templates/             # HMTL kodas, kuris bus atvaizduojamas naršyklėje; ką matys naudotojas
        ├── base.html          # Bazinis HTML šablonas, iš kurio visi kiti šablonai paveldėja struktūra (pvz. navbarą)
        └── index.html         # Pagrindinės svetainės HMTL kodas
```

### Flask ir SQLAlchemy pasiruošimas
- Flask programos sukūrimas `__init__.py` faile
- Konfiguracija:
  - Nurodyti secret key
  - Nurodyti path į sql database
  - Nurodyti sql modifikacijų nesekimą
- Inicijuoti SQLAlchemy `__init__.py` faile
- Kaip _paskutinį_ dalyką, importuoti `routes`

### Databases
**Pastaba:** PK = Primary Key, FK = Foreign Key. Kuriant naujas (ypač didesnes ir sudėtingesnes) duomenų bazes, rekomenduotina panašiai susiplanuoti savo DB prieš ją programuojant

- Susikurti tris lenteles (DB modelius):
  - Students:
    - id: INT, PK
    - name: STR
    - surname: STR
    - lectures: relationship (many2many: vienas studentas turi daug paskaitų, viena paskaita turi daug studentų)
  - Lecture:
    - id: INT, PK
    - title: STR
    - students: relationship (many2many: vienas studentas turi daug paskaitų, viena paskaita turi daug studentų)
    - professor_id: INT, FK (many2one: viena paskaita turi vieną dėstytoją)
  - Professor:
    - id: INT, PK
    - name: STR
    - surname: STR
    - name_and_surname: STR
    - lectures: relationship (one2many: dėstytojas turi daug paskaitų)
- Susikurti pagalbinę lentelę paskaitoms ir studentams susieti (paduoti studentų ID: INT kaip foreign key, taip pat paskaitų ID: Int kaip foreign key)

### Formos
- `StudentForm`
  - name: StringField, DataRequired validatorius
  - surname: StringField, DataRequired validatorius
  - lectures: QuerySelectMultipleField
  - SubmitField
- `LectureForm`
  - title: StringField, DataRequired validatorius
  - students: QuerySelectMultipleField
  - professor: QuerySelectField
  - submit: SubmitField
- `ProfessorForm`
  - name: StringField, DataRequired validatorius
  - surname: StringField, DataRequired validatorius
  - lectures: QuerySelectMultipleField
  - submit: SubmitField

### Maršrutai
- Dirbame su `routes.py` failu
- Sukurti pagrindinių maršrutų funkcijas: `index`, `professors`, `students`, `lectures`
  - Naudojant šias funkcijas bus išrašomi atitinkami duomenys
  - Turime daryti pvz. `Professor.query.all()` ir tada rezultatą paduoti į `render_template` funckiją
- Sukurti `new_professor`, `new_student`, `new_lecture` maršrtų funkcijas
  - Naudojant šias funkcijas bus sukuriami nauji įrašai atitinkamose duombazės lentelėse
  - Sukuriame instance atitinkamos formos, patikriname ar praeina validators
  - Sukuriame naują instance atitinkamos klasės, pvz. `Professor(name=form.name.data, surname=form.surname.data, ...)`
  - Jei forma (ir klasė) turi daugiaskaitinį kintmąjį (pvz. profesorius turi daug paskaitų `professor.lectures`), tuomet iteruojame per daugiaskaitinį kintamąjį, darydami query.get (pvz. `Lecture.query.get(lecture.id))` ir priskiriame tą objektą prie naujai kuriamo objekto (pvz. `new_professor.lectures.append(assigned_lecture))`
  - Visus naujai sukurtus duomenis pridedame į duomenų bazės redagavimo sesiją pvz. `db.session.add(new_professor)`
  - Įrašome duomenis į duomenų bazę: `db.session.commit()`
  - Dažniausiai šiuo metu redirectinam į puslapį, kuriame būtų galima pamatyti naujų duomenų pasikeitimus (pvz. `redirect(url_for('professors'))`)
  - Atvaizduojame formą, jei ši funkcija negavo POST metodo. Pvz. `return render_template("add_professor.html", form=form)`
- Sukurti `delete_professor`, `delete_student`, `delete_lecture` maršrutų funkcijas
  - Maršrutas turės ID kintamuosius jame, pvz. "/delete_professor/\<int:id\>" ir todėl python funckija turės argumentą id: `def delete_professor(id):`
  - Su šia funkcija ištrinsime pasirinkto objektą iš duomenų bazės
  - Pirma, gauname specifinį objektą iš duomenų bazės. Pvz., jei esame `delete_professor` funkcijoje `res = Professor.query.get(id)`
  - Ištriname iš DB: `db.session.delete(res)`
  - Užskaitome DB redagavimą: `db.session.commit()`
  - Dažniausiai šiuo metu redirectinam į puslapį, kuriame būtų galima pamatyti naujų duomenų pasikeitimus (pvz. `redirect(url_for('professors'))`)
- Sukurti `edit_professor`, `edit_student`, `edit_lecture` maršrutų funkcijas
  - Maršrutas vėl turės ID kintamuosius jame, pvz. "/edit_professor/\<int:id\>" ir todėl python funckija turės argumentą id: `def edit_professor(id):`
  - Šios funkcijos labai panašios į `add` funkcijas. Esminis skirtumas pvz. tarp `edit_professor` ir `add_professor` yra prieš formos validavimo patikrinimą, darome užklausą į duomenų bazę (naudodami `id` argumentą) ir gauname dėstytoją, kurio duomenis norime keisti.
  - Šiuos dėstytojo duomenis, kartu su forma (taip pat kaip `add` funkcijoje) paduodame į `render_template("edit_professor.html", form=form, professor=professor)`
  - Atkreipktie dėmesį, kad naujo įrašo kurti (kviesti `db.session.add`) NEREIKIA. Užtenka tik `db.session.commit()`, nes mes pakeičiame duomenis EGZISTUOJANČIAM įrašui duomenų bazėje
  - `edit_professor.html` reikia pridėti `{{ form.name(class="form-control", value=professor.name) }}` t.y. `value=professor.name` argumentą. Šioje būtent vietoje ir naudosime paduotus specifiško dėstytojo duomenis, kad redaguojant šio dėstytojo duomenis pradėtume ne nuo pradžių
