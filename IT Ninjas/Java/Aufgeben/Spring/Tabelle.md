
|                       Beschreibung                       | Http-Methode |         URL         | Request-Body -Beispiel | Path-Variable |   Response-Body Beispiel   |
|:--------------------------------------------------------:|:------------:|:-------------------:|:----------------------:|:-------------:|:--------------------------:|
|                Neues Schulfach hinzufügen                |     POST     | /admin/subject |   {"name":"Physik"}    |     keine     | keine |
|                       Fach Löschen                       |    DELETE    |       /admin/subject       |   {"name":"Physik"}    | /subject_id              | keine                           |
|                     Fach Bearbeiten                      |     PUT      |       /admin/subject        |   keine    | /subject_id              | keine                           |
|                  Alle Fächer auflisten                   | GET             |       /admin/subject/al        | keine                       | keine              | {"name":"Physiks"}                           |
|                                                          |              |                     |                        |               |                            |
|                                                          |              |                     |                        |               |                            |
|                                                          |              |                     |                        |               |                            |
|                                                          |              |                     |                        |               |                            |
|        Alle Fächer und all deren Noten auflisten         |     GET      |      /student/school_subject_grade<br>      | keine                       | keine              | {"name":"Physik","grade":"5"}                           |
|    Alle Fächer und deren Durchschnittsnote auflisten     |     GET      |      /student/school_subject_grade<br>/average      | keine                       | keine              | {"name":"Physik","AVG":"5"}                           |
| Alle Noten und die Durchschnittsnote des Fachs auflisten |     GET      |      /student/school_subject_grade<br>/average      | keine                       | /subject_id              | {"grade":"5","AVG":"5"}                           |
|                     Note Hinzufügen                      |     POST     |      /student/school_subject_grade/grade<br>      | {"name":"Physik", "grade":"5", "Date":"1.1.2024"}                       | keine              | keine                           |
|                       Note Ändern                        |     PUT      |      /student/school_subject_grade/grade<br>      | {"name":"Physik", "grade":"5", "Date":"1.1.2024"}                       | /school_subject_grade_id              | keine                           |
|                       Note Löschen                       |    DELETE    |      /student/school_subject_grade/grade<br>      | keine                       | /school_subject_grade_id              | kein                           |
