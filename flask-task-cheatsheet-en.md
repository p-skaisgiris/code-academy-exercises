# Task
- Create a Flask application that allows you to save students, teachers and lectures
- Each teacher would be allowed to assign his lectures (one2many connection)
- Allow many lectures to be assigned to each student (many2many relationship)

Database schema (note the `students_lectures' auxiliary table, which allows for a Many2Many relationship between students and lectures):

![asd](students-db-schema.jpg)

## Step-by-step

### Correct Flask project structure
- We create a new project directory `students_flask_project`
- We create a new module: a new directory `students_flask` and a `__init__.py` file in it
- We create other flask `.py` files and put them in the `students_flask` module
- We create a `run.py` file, which will be a very minimal startup file
- The final structure should look like this:
```bash
.
├── run.py            # File used to run the project (app.run)
└── students_flask/   # Our project module
 ├── forms.py         # Form classes (code similar to models.py)
 ├── __init__.py      # File with Flask configuration (app, db variables)
 ├── models.py        # Database models (code similar to forms.py)
 ├── routes.py        # Routes and their logic (displaying templates, sending data to templates and to DB)
 └── templates/       # HMTL code that will be displayed in the browser; what the user will see
     ├── base.html    # Base HTML template from which all other templates inherit structure (eg navbar)
     └── index.html   # The HMTL code of the main site
```

### Getting ready for Flask and SQLAlchemy
- Creating a Flask program in the `__init__.py` file
- Configuration:
 - Specify the secret key
 - Specify the path to the sql database
 - Specify not to track sql modifications
- Initialize SQLAlchemy in the `__init__.py` file
- As a _last_ thing, import `routes`

### Databases
**Note:** PK = Primary Key, FK = Foreign Key. When creating new (especially larger and more complex) databases, it is recommended to similarly plan your DB before programming it

- Create three tables (DB models):
 - Students:
 - id: INT, PK
 - in the house: STR
 - surname: STR
 - lectures: relationship (many2many: one student has many lectures, one lecture has many students)
 - Lecture:
 - id: INT, PK
 - title: STR
 - students: relationship (many2many: one student has many lectures, one lecture has many students)
 - professor_id: INT, FK (many2one: one lecture has one teacher)
 - Professor:
 - id: INT, PK
 - in the house: STR
 - surname: STR
 - name_and_surname: STR
 - lectures: relationship (one2many: the teacher has many lectures)
- Create an auxiliary table to link lectures and students (submit student ID: INT as foreign key, as well as lecture ID: Int as foreign key)

### Forms
- `StudentForm`
 - name: StringField, DataRequired validator
 - surname: StringField, DataRequired validator
 - lectures: QuerySelectMultipleField
 - SubmitField
- `LectureForm`
 - title: StringField, DataRequired validator
 - students: QuerySelectMultipleField
 - professor: QuerySelectField
 - submit: SubmitField
- `ProfessorForm`
 - name: StringField, DataRequired validator
 - surname: StringField, DataRequired validator
 - lectures: QuerySelectMultipleField
 - submit: SubmitField

### Routes
- We are working with `routes.py` file
- Create main route functions: `index`, `professors`, `students`, `lectures`
 - Using these functions will output the relevant data
 - We have to do e.g. `Professor.query.all()` and then pass the result to the `render_template` function
- Create `new_professor`, `new_student`, `new_lecture` route functions
 - Using these functions will create new records in the corresponding database tables
 - We create an instance of the appropriate form, check whether the validators pass
 - We create a new instance of the corresponding class, e.g. `Professor(name=form.name.data, surname=form.surname.data, ...)`
 - If the form (and class) has a polynomial variable (eg professor has many lectures `professor.lectures`), then we iterate through the polynomial variable by doing query.get (eg `Lecture.query.get(lecture.id))` and we assign that object to the newly created object (eg `new_professor.lectures.append(assigned_lecture))`
 - We add all newly created data to the database editing session e.g. `db.session.add(new_professor)`
 - We write data to the database: `db.session.commit()`
 - Most of the time, we redirect to a page where new data changes can be seen (e.g. `redirect(url_for('professors'))`)
 - We render the form if this function has not received a POST method. For example `return render_template("add_professor.html", form=form)`
- Create `delete_professor`, `delete_student`, `delete_lecture` route functions
 - A route will have ID variables in it, e.g. "/delete_
