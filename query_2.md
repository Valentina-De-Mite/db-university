Group by:
Contare quanti iscritti ci sono stati ogni anno
SELECT courses.`year`, count(\*)
FROM students
JOIN degrees ON degrees.id = students.degree_id
JOIN courses ON courses.degree_id = degrees.id
GROUP BY courses.`year`;

Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT teachers.office_address as "Ufficio", COUNT(teachers.office_address) AS "N. di insegnanti"
FROM teachers
GROUP BY teachers.office_address
HAVING COUNT(teachers.office_address) > 1;

Calcolare la media dei voti di ogni appello d'esame
SELECT courses.`name` , exam_student.exam_id as "Appello n.", exams.date as "data appello", AVG(exam_student.vote) as "Media"
FROM exam_student
JOIN exams ON exams.id = exam_student.exam_id
join courses ON courses.id = exams.course_id
GROUP BY exam_student.exam_id;

Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT departments.`name` as "Dipartimento", COUNT(degrees.id) as "Numero di corsi di laurea"
FROM degrees
JOIN departments ON degrees.department_id = departments.id
GROUP BY department_id;

Joins:
Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT students.`name`, students.surname
FROM students
JOIN degrees ON degrees.id = students.degree_id
WHERE degrees.`name` like "%economia%";

Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT degrees.`name`
FROM degrees
JOIN departments ON degrees.department_id = departments.id
WHERE degrees.`name` like "%magistrale%" AND departments.`name` like "%Neuroscienze%" ;

Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT degrees.`name` as "Corso di laurea", courses.`name` as "Nome Corso"
FROM courses
JOIN degrees ON courses.degree_id = degrees.id
JOIN course_teacher ON course_teacher.course_id = courses.id
JOIN teachers ON course_teacher.teacher_id = teachers.id
WHERE teachers.id=44 ;

Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT students.surname as "Cognome", students.`name` as "Nome", departments.`name` as "Dipartimento", degrees.`name` as "Corso di laurea", degrees.`level` as "Tipo di laurea"
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.surname, students.`name`;

Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT degrees.`name` as "Corso di laurea", degrees.`level` as "Tipo di laurea", courses.`name` as "nome corso", teachers.`name` ,teachers.surname
FROM degrees
JOIN courses ON courses.degree_id = degrees.id
join course_teacher ON course_teacher.course_id = courses.id
JOIN teachers ON course_teacher.teacher_id = teachers.id;

Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT DISTINCT teachers.`name` as "Nome Insegnante" ,teachers.surname as "Cognome Insegnante", departments.`name` as "Dipartimento"
FROM teachers
JOIN course_teacher ON course_teacher.teacher_id = teachers.id
JOIN courses ON courses.id= course_teacher.course_id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments on degrees.department_id = departments.id
WHERE departments.`name` LIKE "%matematica%";
