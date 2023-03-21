_Esercizio di oggi:_

#### Query con GROUP BY

**1. Contare quanti iscritti ci sono stati ogni anno**\
SELECT COUNT(\*) AS "numero degli studenti iscritti", YEAR(`enrolment_date`) AS "anno di iscrizione"\
FROM `students`\
GROUP by YEAR(`enrolment_date`);

**2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio**
SELECT COUNT(\*) AS "numero_insegnanti", `office_address` AS "indirizzo_edificio"\
FROM `teachers`\
GROUP BY `office_address`;

**3. Calcolare la media dei voti di ogni appello d'esame**\
SELECT ROUND(AVG(`vote`)) AS "la media dei voti ", `exam_id` AS "exam_id "\
FROM `exam_student`\
GROUP BY `exam_id`;

**4. Contare quanti corsi di laurea ci sono per ogni dipartimento**
SELECT COUNT(\*) AS "numero_corsi_di_laurea", `department_id`\
FROM `degrees`\
GROUP BY `department_id`;
