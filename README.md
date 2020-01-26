# Pewlett-Hackard-Analysis

By creating  new lists of potential mentors, we show a current list of employees that may be available and what role they are in.


-- Joining 2 tables
SELECT e.emp_no,
     e.first_name,
     e.last_name,
     s.salary,
	 s.from_date

INTO mod_seven
FROM employees as e 
Right JOIN salaries as s
ON e.emp_no = s.emp_no;

SELECT ms.emp_no,
		ti.title,
     ms.first_name,
     ms.last_name,
     ms.salary,
	 ms.from_date

INTO challenge
FROM titles as ti
LEFT JOIN mod_seven as ms
ON ms.emp_no = ti.emp_no

SELECT emp_no,
	    title,
		count(*)
FROM challenge
GROUP BY emp_no,title
HAVING count(*) >1;

SELECT DISTINCT ON (emp_no,title) * FROM challenge

SELECT ch.emp_no,
		ch.title,
     ch.first_name,
     ch.last_name,
     s.to_date,
	 ch.from_date
FROM salaries as s
LEFT JOIN challenge as ch
ON ch.emp_no = s.emp_no
-- WHERE (ch.from_date BETWEEN '1965-12-31' AND '1965-01-01')
-- AND (s.to_date <= '9999-01-01');

SELECT mt.emp_no,
		mt.title,
     mt.first_name,
     mt.last_name,
     mt.to_date,
	 mt.from_date,
	 e. birth_date,
	 e. emp_no
FROM employees as e
LEFT JOIN mentor_table as mt
ON mt.emp_no = e. emp_no
WHERE (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
AND (mt.to_date <= '9999-01-01');
	 

SELECT de.to_date,
		fp.emp_no,
		fp.title,
     fp.first_name,
     fp.last_name,
     fp.to_date,
	 fp.from_date,
	 fp.birth_date
	 
FROM final_part as fp
LEFT JOIN dept_emp as de
ON fp.emp_no = de.emp_no
WHERE (fp.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
AND de.to_date = ('9999-01-01')






