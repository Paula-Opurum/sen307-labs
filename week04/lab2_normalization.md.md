1. Unnormalized Form (UNF)
The initial raw registration sheet containing repeating groups and multi-valued attributes for students, courses, and lecturers.

| Matric_no | Student_name | Student_dept | Course_codes | Course_titles | Lecturers | Lecturer_depts | Session |
| 20231234 | Ada Obi | Software Engineering | SEN307, SEN301 | Database Systems, Software Architecture | Dr A. Okafor, Dr M. Bello | Software Eng., Software Eng. | 2026/2027 |
| 20231235 | John Musa | Computer Science | SEN307, COS301 | Database Systems, Operating Systems | Dr A. Okafor, Mrs F. Eze | Software Eng., Computer Sci. | 2026/2027 |
| 20231236 | Grace Okon | Software Engineering | SEN301 | Software Architecture | Dr M. Bello | Software Eng. | 2026/2027 |

2. First Normal Form (1NF)
Explanation:Removed multi-valued cells so that every cell contains a single atomic value, and expanded rows to give each student-course pair its own row.

| Matric_no | Student_name | Student_dept | Course_code | Course_title | Lecturer_name | Lecturer_dept | Session |
| 20231234 | Ada Obi | Software Engineering | SEN307 | Database Systems | Dr A. Okafor | Software Eng. | 2026/2027 |
| 20231234 | Ada Obi | Software engineering | SEN301 | Software Architecture | Dr M. Bello | Software Eng. | 2026/2027 |
| 20231235 | John Musa | Computer Science | SEN307 | Database Systems | Dr A. Okafor | Software Eng. | 2026/2027 |
| 20231235 | John Musa | Computer Science | COS301 | Operating Systems | Mrs F. Eze | Computer Sci. | 2026/2027 |
| 20231236 | Grace Okon | Software Engineering | SEN301 | Software Architecture | Dr M. Bello | Software Eng. | 2026/2027 |

3. Second Normal Form (2NF)
Explanation: Removed partial dependencies by splitting attributes that only depend on a part of the composite primary key into separate, dedicated entity tables (`Student`, `Course`, `Lecturer`, `Enrolment`).

STUDENT
| Matric_no (PK) | Student_name | Student_dept |
| :--- | :--- | :--- |
| 20231234 | Ada Obi | Software Engineering |
| 20231235 | John Musa | Computer Science |
| 20231236 | Grace Okon | Software Engineering |

 COURSES
| Course_code | Course_title |
| :--- | :--- |
| SEN307 | Database Systems |
| SEN301 | Software Architecture |
| CSC301 | Operating Systems |

 LECTURER
| Lecturer | Lecturer_dept |
| :--- | :--- |
| Dr A. Okafor | Software Engineering |
| Dr M. Bello | Software Engineering |
| Mrs F. Eze | Computer Science |

ENROLMENT
| Matric_no | Course_code | Session | Lecturer |
| :--- | :--- | :--- | :--- |
| 20231234 | SEN307 | 2026/2027 | Dr A. Okafor |
| 20231234 | SEN301 | 2026/2027 | Dr M. Bello |
| 20231235 | SEN307 | 2026/2027 | Dr A. Okafor |
| 20231235 | COS301 | 2026/2027 | Mrs F. Eze |
| 20231236 | SEN301 | 2026/2027 | Dr M. Bello |

---

4. Third Normal Form (3NF)
Explanation: Removed transitive dependencies (such as department details depending on non-key attributes) by creating a standalone `Department` entity and linking it via Foreign Keys.

Department
| Dept_name (PK) |

| Software Engineering |
| Computer Science |

Student
| Matric_no | Student_name | Dept_name |

| 20231234 | Ada Obi | Software Engineering |
| 20231235 | John Musa | Computer Science |
| 20231236 | Grace Okon | Software Engineering |

Course
| Course_code | Course_title |

| SEN307 | Database Systems |
| SEN301 | Software Architecture |
| CSC301 | Operating Systems |

 Lecturer
| Lecturer | Lecturer_dept | Course |

| Dr A. Okafor | Software Engineering | SEN307 |
| Dr M. Bello | Software Engineering | SEN301 |
| Mrs F. Eze | Computer Science | COS301 |

 Enrolment
| Matric_no | Course_code | Session |

| 20231234 | SEN307 | 2026/2027 |
| 20231234 | SEN301 | 2026/2027 |
| 20231235 | SEN307 | 2026/2027 |
| 20231235 | COS301 | 2026/2027 |
| 20231236 | SEN301 | 2026/2027 |

Course_Lecturer
| Course_code (PK, FK) | Lecturer (PK, FK) | Session (PK) |

| SEN307 | Dr A. Okafor | 2026/2027 |
| SEN301 | Dr M. Bello | 2026/2027 |
| COS301 | Mrs F. Eze | 2026/2027 |

---
 5. Final 3NF Relational Schema

```text
Department (
    dept_name PK
)

Student (
    matric_no PK,
    student_name,
    dept_name FK → Department.dept_name
)

Course (
    course_code PK,
    course_title
)

Lecturer (
    lecturer PK,
    lecturer_dept FK → Department.dept_name
)

Enrolment (
    matric_no PK, FK → Student.matric_no,
    course_code PK, FK → Course.course_code,
    session PK
)

Course_Lecturer (
    course_code PK, FK → Course.course_code,
    lecturer PK, FK → Lecturer.lecturer,
    session PK
)