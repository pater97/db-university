1. Selezionare tutti gli studenti nati nel 1990 (160)
*** SELECT * FROM `students` WHERE `date_of_birth` BETWEEN "1990-01-01" AND "1990-12-31"; *** || SELECT * FROM STUDENTS WHERE YEAR(DATE_OF_BIRTH) = '1990'

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
*** SELECT `cfu` FROM `courses` WHERE `cfu` > "10" ***

3. Selezionare tutti gli studenti che hanno più di 30 anni
*** SELECT * FROM `students` WHERE `date_of_birth` < "1990-01-01" ***

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
*** SELECT * FROM `courses` WHERE `period` = "I semestre" AND `year` = "1" ***

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
*** SELECT * FROM `exams` WHERE `hour` > "14:00:00" AND `date` = "2020-06-20" ***

6. Selezionare tutti i corsi di laurea magistrale (38)
*** SELECT * FROM `degrees` WHERE `level` = "magistrale" ***

7. Da quanti dipartimenti è composta l'università? (12)
*** SELECT * from `departments` ***

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
*** SELECT * FROM `teachers` WHERE `phone` IS NULL ***


APPUNTI:unione di 3 tabelle 
SELEZIONARE TUTTI GLI APPELLI D'ESAME DEL CORSO DI LAURE MAGISTRALE IN FISICA DEL PRIMO ANNO 

SELECT  courses.name,courses.period,courses.year,courses.cfu,courses.website,exam.date,exams.location,exams.adress 
FROM degrees 
JOIN courses ON degrees.id = courses.degree_id 
JOIN exams ON course.id = exams.course_id
WHERE degree.name = 'corso di laurea magistrale in fisica'
AND courses.year = 1


APPUNTI: 
SELEZIONARE TUTTI I DOCENTI CHE INSEGNANO NEL CORSO DI LAUREA IN LETTERE

SELECT DISTINCT teachers.name,teachers.surname,    ***DISTINCT SERVE PER NON VISUALIZZARE DUPLICATI**
FROM 'teachers'
JOIN 'course_tacher'
ON teachers.id = course_teacher.teacher_id
JOIN courses 
ON course_teacher.course_id = courses.id
JOIN degrees
ON courses.degree_id = degrees.id
WHERE degrees.name = 'corso di laurea in lettere'

