TODO:
# Group by:
1. Contare quanti iscritti ci sono stati ogni anno

SELECT 
YEAR(`enrolment_date`) AS `year`,
COUNT(`id`) AS `total_students`
FROM `students`
GROUP BY YEAR(`enrolment_date`)
ORDER BY `year`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT 
`office_address`,
COUNT(`id`) AS `total_teachers`
FROM `teachers`
GROUP BY `office_address`;

3. Calcolare la media dei voti di ogni appello d'esame

SELECT 
`exam_id`, 
AVG(`vote`) AS `average_vote`
FROM `exam_student`
GROUP BY `exam_id`
ORDER BY `exam_id`;



4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT 
`department_id`,
COUNT(`id`) AS `degree_count`
FROM `degrees`
GROUP BY `department_id`;

# Joins:

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.*, `degrees`.`name`
FROM `students`
JOIN `degrees` 
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT `degrees`.*
FROM `degrees`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `degrees`.`level` = 'magistrale'
AND `departments`.`name` = 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.*, teachers.name, teachers.surname
FROM `courses`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono 5. iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT 
`students`.*, 
`degrees`.`name` ,
`departments`.`name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;

6. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti


SELECT 
`degrees`.`name`,
`courses`.`name` ,
`teachers`.`name` ,
`teachers`.`surname` 
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`

7. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT
`teachers`.*,
`departments`.`name`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';


# BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

