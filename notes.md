

--------CREATING A TABLE ------------- 

CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype
);




--------------DML--------------
->Data Manipulation Language

1> INSERT --- for inserting data 

INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
 

    eg ->
    INSERT INTO students (id, name, age, course)
    VALUES
        (2, 'Aman', 21, 'ECE'),
        (3, 'Karan', 19, 'CSE'),
        (4, 'Riya', 20, 'IT');



2> UPDATE --- modifying existing data  
    eg->
    UPDATE students
    SET age = 22,
        course = 'IT'
    WHERE id = 1;


    note -> if we dont write the 'WHERE'.. every filed will be update 
        UPDATE student 
        SET age = 22;


3> DELETE --- delete data 

    eg -> 
        DELETE FROM students 
            WHERE id = 1;;


    note --> imp to add the 'WHERE' statement or all data will be gone 



| Operation | Syntax                         |
| --------- | ------------------------------ |
| Add       | `INSERT INTO ... VALUES ...`   |
| Change    | `UPDATE ... SET ... WHERE ...` |
| Remove    | `DELETE FROM ... WHERE ...`    |






----------AND , OR , IN , BETWEEN , LIKE , NOT , BETWEEN ----------------

AND -> 
        UPDATE student 
            SET grade = 'A' 
            WHERE marks > 90 
            AND course ='CSE';


OR ->  
        UPDATE students 
            SET couse = 'CSE'
            WHERE marks > 90 
            OR name = 'RAS'

IN -> 
        DELET FROM students 
        WHERE course IN ('CSE','IT','ECE');


        meaning -> WHERE department = 'CSE'
                    OR department = 'ECE'

                    too muct to write 


BETWEEN->  
        UPDATE students
            SET marks = marks + 10
            WHERE marks BETWEEN 60 AND 70;

LIKE-> useful for searching 
        SELECT *
            FROM students
            WHERE name LIKE 'R%';


            R% means anything after R 
            
            %r would have ment , anything ending with r 


NOT -> 
        SELECT *
        FROM students
        WHERE NOT department = 'CSE';

-------------------------------------------------------

SELECT -> 

    SELECT name, marks
        FROM students
        WHERE marks > 80;


SELECT *
FROM students
WHERE course = 'CSE'
AND marks > 80;
    
SELECT *
FROM students
WHERE course = 'CSE'
OR course = 'IT';

SELECT *
FROM students
ORDER BY marks DESC;

SELECT *
FROM students
ORDER BY marks ASC;


--->SORTING multiple columns 

SELECT *
FROM students
ORDER BY course ASC, marks DESC;

-> sort courses aplhabetically , within each course , put the highest marks first 

LIMIT ->
SELECT * FROM student 
ORDER BY marks DESC
LIMIT 3;

-- shows only top 3


-------genral order for queries----------
SELECT
FROM
WHERE
ORDER BY
HAVING 
ORDER BY
LIMIT





------------------CONSTTRAINTS--------------------------

NOT NULL ( COLUMN CANNOT BE NULL)
UNIQUE (ALL VALUES MUST BE DIFF)
PRIMARY KEY (UNIQUE + NOT NULL + IDENTIFIES EACH ROW )
FOREIGH KEY (LINKS TO ANOTHER TABLE PRIMARY KEY )
CHECK ( VALUE MUST SATISFY A CONDITION )
DEFAULT (GIVE A VALUE IF NONE IS PROVIDED)

CANDIDATE KEY ( ANY COLUMN THAT COULD BE A PRIMARY KEY )
COMPOSIT KEY ( PRIMARY KEY MADE OF 2+ COLUMNS )

EG -> 

CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 18),
    course VARCHAR(10) DEFAULT 'CSE'
);





--------------------AGGREGATE FUNCTIONS------------------------

COUNT() -> NO. OF ROWS 
SUM() -> TOTAL 
AVG()
MIN()
MAX()

eg -> 
SELECT COUNT(*) FROM students;
SELECT AVG(marks) FROM students;
SELECT MAX(marks) FROM students WHERE course = 'CSE';




GROUP BY ->
    SELECT course, AVG(marks)
    FROM students
    GROUP BY course;


HAVING ->
    SELECT course, AVG(marks) AS avg_marks
    FROM students
    GROUP BY course
    HAVING AVG(marks) > 75;

    note-> u cannot use WHERE AVG(MARKS)>75 thats why HAVING exist 








--------------------------JOINS-----------------------------
-> combines rows or columns of two or more tables ( exception->self joint , only one table required)


1> INNER JOIN
    return only matching rows in both tables 

    QUERY -> 
        SELECT  students.name , marks.score 
        FROM students
        INNER JOINT marks ON students.id = marks.students_id;


2>LEFT JOIN 
    all rows from left tabel + matching from right (NULL if no match)

    SELECT student.name , marks.score
    FROM students 
    LEFT JOIN marks ON students.id = marks.students_id;


3> RIGHT JOIN
    opposite of right join 

4> FULL JOIN 
    all rows from both tables 

5> CROSS JOIN 
    Every row of table A X evry row of table B 
    
6> SELF JOIN 
    SELECT e1.name AS employee, e2.name AS manager
    FROM employees e1
    JOIN employees e2 ON e1.manager_id = e2.id;


----------------------------------------------------------------







ALTER -> to add or remove columns in the table 
    eg -> ALTER TABLE students ADD email VARCHAR(50);
          ALTER TABLE students DROP COLUMN email:
          ALTER TABEL students MODIFY age INT;



----------------------DROP , TRUNCATE , DELETE--------------------------------



Command	            What it does	                Can rollback?

DELETE	            Removes rows (WHERE possible)	    Yes
TRUNCATE	        Removes all rows fast	            No
DROP	            Removes entire table structure	    No 


DELETE FROM students WHERE id = 5;
TRUNCATE TABLE students;
DROP TABLE students;

--------------------------------------------------------------------------------



DISTINCT -> remove all duplicates from the result 


SELECT DISTINCT course FROM student;

--------------------------------------------------------------------


ALIASES -> rename columns or tables temporarily 

eg ->   SELECT name AS student_name, marks AS score
        FROM students AS s;



---------------------------------------------------------------------------------

NULL HANDLING -> 

eg-> SELECT * FROM students WHERE email IS NULL;


----------------------------------------------------------------------------------

UNION / UNION ALL 

SELECT name FROM students
UNION
SELECT name FROM teachers;


UNION removes duplicates ;
UNION ALL kepps duplicates 


-------------------------------------------------------------------------------------

VIEWS -> 

    saved query that acts like a virtual table 
    benifits -> security , simplicity 

CREATE VIEW top_students AS 
SELECT name , marks FROM stud WHERE marks>80;

SELECT * FROM top_students;


-------------------------------------------------------------------------------------

INDEXES -> 
    speed up searching 

    CREATE INDEX idx_name ON students(name);:> [!WARNING]
    



