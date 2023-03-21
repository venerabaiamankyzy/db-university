_Esercizio di oggi:_

#### Query con JOIN

**1. Selezionare tutti gli studenti(studenti) iscritti al (degrees) Corso di Laurea in Economia**
SELECT `students`.\*\
FROM `students`\
JOIN `degrees` ON `students`.`degree.id` = `degrees`.`id`\
WHERE `degrees`.`name` = "Corso di Laurea in Economia";\
ORDER BY `students`.`degree.id` DESC

**2. Selezionare tutti i (degrees) Corsi di Laurea Magistrale del (departments) Dipartimento di Neuroscienze**
SELECT `degrees`.\*\
FROM `degrees`\
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`\
WHERE `degrees`.`level` = "magistrale"\
AND `departments`.`name` = "Dipartimento di Neuroscienze";

**3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)**
SELECT `courses`.\*\
FROM `course_teacher`\
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`\
WHERE `course_teacher`.`teacher_id` = "44";

<!-- SELECT `courses`.\*\
FROM `course_teacher`\
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`\
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`\
WHERE `teachers`.`name` = "Fulvio"\
AND `teachers`.`surname` = "Amato"; -->

**4. Selezionare tutti gli studenti (students) con i dati relativi al (degrees) corso di laurea a cui sono iscritti e il relativo dipartimento (departments), in ordine alfabetico per cognome e nome**
SELECT \
`students`.`id` AS `id_student`\,
`students`.`name` AS `name_student`\,
`students`.`surname` AS `surname_student`\,

`degrees`.`id` AS `id_degree`\,
`degrees`.`name` AS `name_degree`\,

`departments`.`id` AS `id_department`\,
`departments`.`name` AS `name_department`\,

FROM `students`\
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`\
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`\
ORDER BY `students`.`surname`, `students`.`name`, `students`.`id`

**5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti**
SELECT\
`degrees`.`id` AS `id_degree`\,
`courses`.`id` AS `id_course`\,
`teachers`.`id` AS `id_teacher`\,

`degrees`.`name` AS `name_degree`\,
`couses`.`name` AS `name_course`\,
`teachers`.`name` AS `name_teacher`\,
`teachers`.`surname` AS `surname_teacher`\,

FROM `degrees`\
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`\
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`\
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`

**6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)**
SELECT\
`teachers`.`id` AS `id_teacher`\,
`teachers`.`name` AS `name_teacher`\,
`teachers`.`surname` AS `surname_teacher`\,

FROM `degrees`\
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`\
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`\
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`\
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`

WHERE `departments`.`name` = "Dipartimento di Matematica";

**7. BONUS: Selezionare per ogni studente (students) quanti tentativi (exam_student) d’esame ha sostenuto per superare ciascuno dei suoi (exams) esami**
-- selezionare conteggio tentativi d'esame
-- per ogni studente ed ogni esame
-- avendo raggiunto un voto pari o maggiore di 18

SELECT\
COUNT(\*) AS `tentativi_esame`,\
`exam_student`.`student_id`,\
`students`.`name` AS `student_name`,\
`students`.`surname` AS `student_surname`,\
`courses`.`name` AS `course_name`,\
MAX(`exam_student`.`vote`) AS `max_vote`

FROM `exam_student`\
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`\
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`\
JOIN `students` ON `exam_student`.`student_id` = `sdudents`.`id`

GROUP BY\
`exam_student`.`student_id`,
`courses`.`id`,\
HAVING MAX(`exam_student`.`vote`) >= 18\
ORDER BY `max_vote` ASC
