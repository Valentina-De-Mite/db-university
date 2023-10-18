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
Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
