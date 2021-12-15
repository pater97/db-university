Query con Group by:

◉ Contare quanti iscritti ci sono stati ogni anno
*** SELECT COUNT(id),YEAR(enrolment_date) FROM students GROUP BY YEAR(enrolment_date) ***

◉ Contare gli insegnanti che hanno l'ufficio nello stesso edificio
*** SELECT COUNT(id),office_address FROM teachers GROUP BY office_address ***

◉ Calcolare la media dei voti di ogni appello d'esame
*** SELECT exam_id,AVG(vote) FROM exam_student GROUP BY exam_id ***

◉ Contare quanti corsi di laurea ci sono per ogni dipartimento
*** SELECT department_id,COUNT(name) FROM degrees GROUP BY department_id ***


Query con Join:

◉Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
***
SELECT students.name, students.surname, degrees.name
FROM degrees 
JOIN students 
ON degrees.id = students.degree_id 
WHERE degrees.name = "Corso di Laurea in Economia"
***

◉Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze
*** 
SELECT *
FROM degrees
JOIN departments
ON degrees.department_id = departments.id
WHERE departments.name = "Dipartimento di Neuroscienze" 
***

◉Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
***
SELECT courses.name AS "name course",teachers.id,teachers.name AS "teacher's name", teachers.surname AS "teachers's surname"
FROM teachers 
JOIN course_teacher 
ON teachers.id = course_teacher.teacher_id
JOIN courses
ON courses.id = course_teacher.course_id
WHERE teachers.id = 44
***

◉Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
***
SELECT students.name, students.surname,degrees.name AS "corso di laurea",departments.name AS "dipartimento"
FROM students
JOIN degrees
ON degrees.id = students.degree_id
JOIN departments 
ON departments.id = degrees.department_id
ORDER BY students.surname, students.name ASC;
***

◉Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
***
SELECT degrees.name AS "INDIZIRIZZO DI LAUREA", courses.name "CORSO",courses.period,courses.year,teachers.name,teachers.surname
FROM courses
JOIN degrees
ON degrees.id = courses.degree_id
JOIN course_teacher
ON course_teacher.course_id = courses.id
JOIN teachers 
ON course_teacher.teacher_id = teachers.id;
***
◉Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
***
SELECT DISTINCT teachers.name, departments.name AS "department's name"
FROM teachers
JOIN course_teacher
ON teachers.id = course_teacher.teacher_id 
JOIN courses 
ON courses.id = course_teacher.course_id 
JOIN degrees
ON degrees.id = courses.degree_id
JOIN departments
ON departments.id = degrees.department_id
WHERE departments.name = "Dipartimento di Matematica";
***
◉◉◉BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami◉◉◉
