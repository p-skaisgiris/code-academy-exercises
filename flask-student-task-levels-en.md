# Student task with levels

Create a Flask application that simulates university lecture registration for both students and faculty. I.e., it would be possible to register for existing lectures for students, and indicate which lectures the lecturers are teaching

## Level 1 (Basics)
- Create a project structure according to the memo
- Configure the project in the `__init__.py` file according to the memory and old projects
- Take `base.html` from old projects, change it for the appropriate task (create records of students, teachers, lectures in the navbar)
- Do not use sqlalchemy databases, instead use only mock data dictionary, which you copy to `models.py` (we will add database models/tables to this file later)
```
students =[{
 'name': 'John',
 'surname': 'Jonaitis'
},
{
 'name': 'Peter',
 'surname': 'Petraitis'
},
{
 'name': 'Aust',
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
 'name': 'Management',
 'surname': 'Adamkus',
 'experience': 25
},
{
 'name': 'Antanas',
 'surname': 'Sour cream',
 'experience': 100
},
{
 'name': 'John',
 'surname': 'Tub',
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
- Create three routes that will take all existing data from a simple corresponding dictionary (shown below) and write each entry on the corresponding pages
- Create three appropriate templates that would receive data from route functions and write out all records as paragraphs or lists (`<ul>`)

## Level 2 (Data storage in databases)
- Create DB models/tables for students, teachers, lectures
- Manually (via sqlalchemy or via raw SQL) write the same data to the created DB file
- Print that data on the relevant website pages using DB

## Level 3 (Entering data through forms)
- Add Flask forms (using e.g. Flask WTForms) to save students, teachers and lectures
- Display the new data entered through the forms on the corresponding pages

## Level 4 (Multiple variables in databases)
- Rebuild the DB (don't forget to delete the old one or do a migration):
 - Each teacher would be allowed to assign his lectures (one2many connection)
 - Allow many lectures to be assigned to each student (many2many relationship)
- Again contribute new data as in level 2, but now adding values ​​to multi-numeric variables

## Level 5 (Multiple choices and validators in forms)
- Modify students form to select multiple lectures (QuerySelectMultipleField)
- Change lecture form to select many students (QuerySelectMultipleField) one teacher (QuerySelectField)
- Change the teachers form to select multiple lectures (QuerySelectMultipleField)
- Add validators in the forms, if you haven't done it yet (e.g. it is necessary to enter first and last names for students and teachers, name for lectures)

## Level 6 (Data editing)
- Make it possible to delete teachers, lectures, students
 - By pressing e.g. "Delete teacher" button, the record of the teacher must be deleted from the database
- Make it possible to edit teachers, lectures, students
 - By pressing e.g. "Edit Tutor", we need to be directed to the same form used to create the Tutor record, but already filled with that Tutor's information
 - If the information is potentially changed, we are directed to the teachers' page, where we can see the changed data