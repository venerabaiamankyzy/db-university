_Esercizio di oggi:_

#### Query con GROUP BY

**1. Contare quanti iscritti ci sono stati ogni anno**\
SELECT COUNT(\_) AS "numero degli studenti iscritti", YEAR(`enrolment_date`) AS "anno di iscrizione"\
FROM `students`\
GROUP by YEAR(`enrolment_date`);

**2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio**
SELECT COUNT(\_) AS "quantità di insegnanti", `office_address` AS "indirizzo edificio"\
FROM `teachers`\
GROUP BY `office_address`;

**3. Calcolare la media dei voti di ogni appello d'esame**\
SELECT AVG(`vote`) AS "la media dei voti ", `exam_id` AS "exam_id "\
FROM `exam_student`\
GROUP BY `exam_id`;

**4. Contare quanti corsi di laurea ci sono per ogni dipartimento**
SELECT COUNT(\*) AS "quantità corsi di laurea", `department_id` AS "id dipartimento" \
FROM `degrees`\
GROUP BY `department_id`;
