**INFORMATION SYSTEMS AND DATABASES – PORTFOLIO ELEMENT 3**

**Student Name:**

Abdulhakim Ezedin

**🔹 Introduction**

This portfolio presents the design and implementation of an **Internship
and Placement Management System** developed using **Oracle APEX and
SQL**.

The system is designed to manage and organize key aspects of the
recruitment process, including:

- Student information

- Company details

- Job and internship openings

- Applications submitted by students

- Interview processes

- Job offers

The database has been carefully designed using **normalization
techniques** to ensure data integrity and reduce redundancy.
Many-to-many relationships have been resolved using associative entities
such as **Application** and **StudentSkill**.

In addition, an Oracle APEX application was developed to provide a
**user-friendly interface**, allowing users such as placement staff and
recruiters to interact with the system without needing to write SQL
queries.

**🔹 Aim of the System**

The main aim of this system is to:

- Efficiently manage internship and placement processes

- Store and retrieve data accurately

- Track student applications and outcomes

- Provide meaningful reports for decision-making

**🔹 Technologies Used**

- Oracle Database (SQL)

- Oracle APEX

- ER Modelling

A list of any assumptions/clarifications you have made that have
affected the design of your database.

1.  **Assumptions/Business Rules:**

<!-- -->

1.  Each student has a unique **StudentID**.

2.  Each company has a unique **CompanyID**.

3.  A **company** can post multiple internship or job openings.

4.  Each **opening** belongs to only one company.

5.  A student can apply to multiple openings.

6.  Each opening can receive applications from many students.

7.  Each application is associated with one student and one opening

8.  Each interview is linked to one specific application, and an
    application may involve multiple interview rounds.

9.  Each offer is linked to one specific application, and an application
    may result in at most one final offer.

10. Each recruiter has a unique RecruiterID.

11. A company can employ multiple recruiters.

12. Each recruiter belongs to only one company.

13. Each opening may be managed by one recruiter.

14. Each skill has a unique SKILLID.

15. A student can have multiple skills.

16. A skill can belong to multiple students.

17. The many-to-many relationship between Student and Skill is resolved
    through the StudentSkill entity.

18. Each StudentSkill record links one student to one skill.

These assumptions define the **Entities, Primary keys, and
Relationships** required to design a normalized database for managing
internships and campus placements.

2.  **An ER diagram:**

<!-- -->

1.  **Problem Many-To-Many Diagram**

<img src="./images/image1.png" style="width:6.5in;height:1.73333in" />

This initial ER diagram shows the many-to-many relationship issues in
the database design.

In this structure:

- A single Student can apply for many openings.

- A single Opening can receive applications from many Students.

This creates a Many-to-Many (M: N) relationship, which is not ideal in
relational database design because it can cause:

- Data redundancy

- Difficulty in storing additional information such as application date
  and status.

- Update, insertion, and deletion anomalies.

Similarly, a Student can have multiple Skills, and one skill can belong
to multiple students, creating another many-to-many relationship.

So, this design is incomplete and needs **normalization.**

2.  **Fixed Diagram:**

To fix the many-to-many issues, associative entities (bridge tables)
were introduced.

1.  The **Application** entity was added to fix the relationship between
    **Student** and **Opening** by converting the many-to-many
    relationship into two one-to-many relationships.

- One **Student** can submit many **Applications**.

- One **Opening** can receive many **Applications**.

The Application table also stores important attributes such as:

- ApplicationDate

- Status

2.  The **StudentSkill** entity was also introduced to fix the
    many-to-many relationship between **Student** and **Skill**.

> This improves the database by reducing redundancy and ensuring
> normalization.

<img src="./images/image2.png" style="width:6.7443in;height:5.04514in" />

3.  **Final Diagram:**

The final ER Diagram shows the complete normalized database structure
for the internship and placement system.

Additional entities were included to represent the full recruitment
process:

- **Company** – Stores company details

- **Recruiter** – represents recruiters linked to a company.

- **Interview** – stores interview rounds, feedback, and results.

- **Offer** – stores salary and acceptance/ decline status.

The final design demonstrates:

- One-to-many relationships

- Many-to-many relationships resolved using bridge entities

- Proper use of **Primary Keys (PK)** and **Foreign Keys (FK)**

- A normalized and scalable database design

Overall, this final structure ensures data integrity and supports the
complete internship application lifestyle.

<img src="./images/image3.png" style="width:6.5in;height:5.65833in" />

<u>Entity Overview Table</u>

This table is to quickly summarize all entities and attributes.

| Entity       | Attributes                                                                                    |
|--------------|-----------------------------------------------------------------------------------------------|
| Student      | **StudentID (PK**), StudentName, Email, Course, CGPA                                          |
| Company      | **CompanyID (PK),** companyName, ContactEmail                                                 |
| Application  | **ApplicationID (PK**), ApplicationDate, Status, **StudentID, (FK),** **OpeningID (FK)**      |
| Offer        | **OfferID (PK),** OfferDate, OfferStatus, Salary, **ApplicationID (FK)**                      |
| Interview    | **InterviewID (PK),** InterviewDate, InterviewRound, Feedback, Result, **ApplicationID (FK)** |
| Opening      | **OpeningID (PK),** JobTitle, Deadline, **CompanyID (FK)**                                    |
| Recruiter    | **RecruiterID (PK),** RecruiterName, Email, Position, **CompanyID (FK)**                      |
| Skill        | **SkillID (PK),** SkillName                                                                   |
| StudentSkill | **StudentID (FK),** **SkillID (FK),** Composite **PK (StudentID, SkillID)**                   |

**Entity Specification Forms**

<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 18%" />
<col style="width: 14%" />
<col style="width: 22%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Students</strong></p>
<p>Entity Description: store information about students applying for
internship.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td>StudentID</td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>1000</td>
</tr>
<tr class="even">
<td>StudentName</td>
<td>VARCHAR2(50)</td>
<td>Not Null</td>
<td>Letters Only</td>
<td>Abdulhakim</td>
</tr>
<tr class="odd">
<td>Email</td>
<td>VARCHAR2(100)</td>
<td>Not Null</td>
<td>Must Contain @</td>
<td>abdul@gmail.com</td>
</tr>
<tr class="even">
<td>Course</td>
<td>VARCHAR2(50)</td>
<td>Not Null</td>
<td>Text Only</td>
<td>Cybersecurity</td>
</tr>
<tr class="odd">
<td>CGPA</td>
<td>NUMBER(3,2)</td>
<td>Nullable</td>
<td>Between 0 and 4.00</td>
<td>3.75</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 21%" />
<col style="width: 22%" />
<col style="width: 13%" />
<col style="width: 21%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Company</strong></p>
<p>Entity Description: store information about companies offering
internship.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td>CompanyID</td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>1101</td>
</tr>
<tr class="even">
<td>CompanyName</td>
<td>VARCHAR2(50)</td>
<td>Not Null</td>
<td>Letters Only</td>
<td>Cloudflare</td>
</tr>
<tr class="odd">
<td>ContactEmail</td>
<td>VARCHAR2(100)</td>
<td>Not Null</td>
<td>Must Contain @</td>
<td>cloudflare@co.uk</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 18%" />
<col style="width: 13%" />
<col style="width: 20%" />
<col style="width: 21%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Application</strong></p>
<p>Entity Description: stores information about students applying for
internship opportunities.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td><strong>ApplicationID</strong></td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>1001</td>
</tr>
<tr class="even">
<td>ApplicationDate</td>
<td>DATE</td>
<td>Not Null</td>
<td>Valid date format</td>
<td>2026-04-24</td>
</tr>
<tr class="odd">
<td>Status</td>
<td>VARCHAR2(20)</td>
<td>Not Null</td>
<td>Pending / Accepted / Rejected</td>
<td>Pending</td>
</tr>
<tr class="even">
<td>StudentID</td>
<td>NUMBER(10)</td>
<td>FK, Not Null</td>
<td>Must exist in Student table</td>
<td>1000</td>
</tr>
<tr class="odd">
<td>OpeningID</td>
<td>NUMBER(10)</td>
<td>FK, Not Null</td>
<td>Must exist in Opening table</td>
<td>4001</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 18%" />
<col style="width: 14%" />
<col style="width: 23%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Offer</strong></p>
<p>Entity Description: stores information about internship/ job offers
made to applicants.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td>OfferID</td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>200</td>
</tr>
<tr class="even">
<td>OfferDate</td>
<td>DATE</td>
<td>Not Null</td>
<td>Valid date format</td>
<td>2026-02-10</td>
</tr>
<tr class="odd">
<td>OfferStatus</td>
<td>VARCHAR2(20)</td>
<td>Not Null</td>
<td>Accepted / Declined / Pending</td>
<td>Accepted</td>
</tr>
<tr class="even">
<td>Salary</td>
<td>NUMBER(8,2)</td>
<td>Not Null</td>
<td>Must be Positive</td>
<td>25000</td>
</tr>
<tr class="odd">
<td>ApplicationID</td>
<td>NUMBER(10)</td>
<td>FK, Not Null</td>
<td>Must Exist in Application Table</td>
<td>1001</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 16%" />
<col style="width: 14%" />
<col style="width: 22%" />
<col style="width: 26%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: Student<strong>Skill</strong></p>
<p>Entity Description: stores the relationship between students and
their skill.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td>StudentID</td>
<td>NUMBER(10)</td>
<td>PK, FK, Not Null</td>
<td>Must exist in Student table.</td>
<td>1000</td>
</tr>
<tr class="even">
<td>SkillID</td>
<td>NUMBER(10)</td>
<td>PK, FK, Not Null</td>
<td>Must exist in skill table</td>
<td>5201</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 18%" />
<col style="width: 14%" />
<col style="width: 23%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Interview</strong></p>
<p>Entity Description: store information about interviews scheduled for
applicants.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td>InterviewID</td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>100</td>
</tr>
<tr class="even">
<td>InterviewDate,</td>
<td>DATE</td>
<td>Not Null</td>
<td>Valid date format</td>
<td>2026-05-22</td>
</tr>
<tr class="odd">
<td>InterviewRound</td>
<td>VARCHAR2(100)</td>
<td>Not Null</td>
<td>Text Only</td>
<td>second round</td>
</tr>
<tr class="even">
<td>Feedback</td>
<td>VARCHAR2(50)</td>
<td>Not Null</td>
<td>Text Only</td>
<td>Good communication skill</td>
</tr>
<tr class="odd">
<td>Result</td>
<td>VARCHAR2(10)</td>
<td>Not Null</td>
<td>Passed / Failed / Pending</td>
<td>Passed</td>
</tr>
<tr class="even">
<td>ApplicationID</td>
<td>NUMBER(10)</td>
<td>FK, Not Null</td>
<td>Must exist in Application table</td>
<td>1001</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 16%" />
<col style="width: 14%" />
<col style="width: 22%" />
<col style="width: 26%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Opening</strong></p>
<p>Entity Description: stores information about internship/job openings
posted by companies.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td>OpeningID</td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>4001</td>
</tr>
<tr class="even">
<td>JobTitle</td>
<td>VARCHAR2(20)</td>
<td>Not Null</td>
<td>Text only</td>
<td>Accountant</td>
</tr>
<tr class="odd">
<td>Deadline</td>
<td>DATE</td>
<td>Not Null</td>
<td>Valid Date format</td>
<td>2026-06-20</td>
</tr>
<tr class="even">
<td>CompanyID</td>
<td>NUMBER(10)</td>
<td>FK, Not Null</td>
<td>Must exist in Company table</td>
<td>1101</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 17%" />
<col style="width: 13%" />
<col style="width: 22%" />
<col style="width: 26%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Recruiter</strong></p>
<p>Entity Description: stores information about recruiters employed by
companies.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td>RecruiterID</td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>4201</td>
</tr>
<tr class="even">
<td>RecruiterName</td>
<td>VARCHAR2(20)</td>
<td>Not Null</td>
<td>Text only</td>
<td>Mike johnson</td>
</tr>
<tr class="odd">
<td>Email</td>
<td>VARCHAR2(100)</td>
<td>Not Null</td>
<td>Must contain @</td>
<td>miami@gmail.com</td>
</tr>
<tr class="even">
<td>Position</td>
<td>VARCHAR2(20)</td>
<td>Not Null</td>
<td>Must be text</td>
<td>Administrator</td>
</tr>
<tr class="odd">
<td>CompanyID</td>
<td>NUMBER(10)</td>
<td>FK, Not Null</td>
<td>Must exist in Company table</td>
<td>1101</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 16%" />
<col style="width: 14%" />
<col style="width: 22%" />
<col style="width: 26%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="5"><p>Entity Name: <strong>Skill</strong></p>
<p>Entity Description: stores information about skills required by
students/applicants.</p></td>
</tr>
<tr class="even">
<td>Attribute</td>
<td>Data type and width</td>
<td>Status</td>
<td>Validation</td>
<td>Example of input and any other relevant info</td>
</tr>
<tr class="odd">
<td><strong>SkillID</strong></td>
<td>NUMBER(10)</td>
<td>PK, Not Null</td>
<td>Must be Unique</td>
<td>5201</td>
</tr>
<tr class="even">
<td>SkillName</td>
<td>VARCHAR2(50)</td>
<td>Not Null</td>
<td>Text only</td>
<td>Communication</td>
</tr>
</tbody>
</table>

5\. The SQL scripts you used to create your tables (including all
constraints) which should match your entity specification forms.

CREATING TABLES:

1.  Students:

This screenshot shows the creation of the STUDENT table in oracle APEX.
The table stores student information such as studentID, name, email,
course, and CGPA. The studentID was set as the PRIMARY KEY to uniquely
identify each student.

<img src="./images/image4.png" style="width:7.5in;height:3.47708in" />

2.  Company:

This screenshot shows the creation of the COMPANY table, which stores
company details including company name, contact information and industry
details. Company ID was used as primary key.

<img src="./images/image5.png" style="width:7.5in;height:3.47917in" />

3.  Skill:

This screenshot shows the SKILL table used to store different technical
and professional skills that can be linked to students through the
StudnetSkill relationship table.

<img src="./images/image6.png" style="width:7.5in;height:3.49514in" />

4.  Recruiter:

This screenshot shows the RECRUITER table, which stores recruiter
details associated with companies. A foreign key relationship was
created between Recruiter and Company

<img src="./images/image7.png"
style="width:7.29305in;height:3.50166in" />

5.  Opening:

This Screenshot shows the OPENING table, which stores internship or job
opportunities posted by companies. The table includes foreign key
references to the Company table.

<img src="./images/image8.png"
style="width:7.37609in;height:3.48473in" />

6.  Application:

This Screenshot show the APPLICATION table, which acts as a bridge
entity between Student and Opening. It records application dates and
statuses for each student applications.

<img src="./images/image9.png" style="width:7.5in;height:3.48333in" />

7.  Interview:

This screenshot shows the INTERVIEW table used to manage interview
schedules, interview types, and interview outcomes related to
applications.

<img src="./images/image10.png"
style="width:7.15672in;height:3.47361in" />

8.  Offer:

This screenshot shows the OFFER table, which stores final job or
internship offers linked to application. Constraints were added to
ensure valid offer statuses.

<img src="./images/image11.png"
style="width:7.19403in;height:3.46528in" />

9.  StudentSkill:

This Screenshot shows the STUDENTSKILL table, which resolves the
many-to-many relationship between Student and Skill by connection
students with their skills.

<img src="./images/image12.png" style="width:7.25in;height:3.80208in" />

6\. Insert In to:

A. **Student Insertion:**

INSERT INTO STUDENT (StudentID, StudentName, Email, Course, CGPA)

VALUES (1000, 'Abdulhakim', 'abdul@gmail.com', 'Cybersecurity', 3.75);

INSERT INTO STUDENT (StudentID, StudentName, Email, Course, CGPA)

VALUES (1002, 'Ali', 'ali@gmail.com', 'Computer Science', 3.20);

INSERT INTO STUDENT (StudentID, StudentName, Email, Course, CGPA)

VALUES (1003, 'Sara', 'sara@gmail.com', 'Cybersecurity', 3.90);

INSERT INTO STUDENT (StudentID, StudentName, Email, Course, CGPA)

VALUES (1004, 'Mike', 'mike@gmail.com', 'Accountant', 3.50);

INSERT INTO STUDENT (StudentID, StudentName, Email, Course, CGPA)

VALUES (1005, 'Ekram', 'ekru@gmail.com', 'Engineer', 3.99);

B. **Company Insertion:**

INSERT INTO Company (CompanyID, CompanyName, ContactEmail)

VALUES (1101, 'Cloudflare', 'cloudflare@gmail.com');

INSERT INTO COMPANY (CompanyID, CompanyName, ContactEmail)

VALUES (1102, 'Google', 'hr@google.com');

INSERT INTO COMPANY (CompanyID, CompanyName, ContactEmail)

VALUES (1103, 'Microsoft', 'jobs@microsoft.com');

INSERT INTO COMPANY (CompanyID, CompanyName, ContactEmail)

VALUES (1104, 'Computing', 'jobs@computing.com');

INSERT INTO COMPANY (CompanyID, CompanyName, ContactEmail)

VALUES (1105, 'Engineers', 'jobs@engineers.com');

3.  **Skill Insertion:**

INSERT INTO SKILL (SKILLID, SkillName)

VALUES (5201, 'Communication');

INSERT INTO SKILL (SkillID, SkillName)

VALUES (5202, 'Python');

INSERT INTO SKILL (SkillID, SkillName)

VALUES (5203, 'Networking');

INSERT INTO SKILL (SkillID, SkillName)

VALUES (5204, 'Maths ');

4.  **Recruiter Insertion:**

INSERT INTO RECRUITER (RecruiterID, RecruiterName, Email, Position,
CompanyID)

VALUES (4201, 'Mike johnson', 'miami@gmail.com', 'Administrator', 1101);

INSERT INTO RECRUITER (RecruiterID, RecruiterName, Email, Position,
CompanyID)

VALUES (4202, 'Sarah Ahmed', 'sarah@microsoft.com', 'HR Manager', 1103);

INSERT INTO RECRUITER (RecruiterID, RecruiterName, Email, Position,
CompanyID)

VALUES (4203, 'John Smith', 'john@cloudflare.com', 'Talent Acquisition',
1101);

5.  **Opening Insertion:**

INSERT INTO OPENING (OpeningID, JobTitle, Deadline, CompanyID)

VALUES (4001, 'Accountant', DATE '2026-06-20',1101);

INSERT INTO OPENING (OpeningID, JobTitle, Deadline, CompanyID)

VALUES (4002, 'Security Analyst', DATE '2026-07-10', 1102);

INSERT INTO OPENING (OpeningID, JobTitle, Deadline, CompanyID)

VALUES (4003, 'Database Admin', DATE '2026-08-01', 1103);

INSERT INTO OPENING (OpeningID, JobTitle, Deadline, CompanyID)

VALUES (4004, 'Cybersecurity ', DATE '2026-01-01', 1104);

INSERT INTO OPENING (OpeningID, JobTitle, Deadline, CompanyID)

VALUES (4005, ' Engineer ', DATE '2026-01-01', 1105);

6.  **Application Insertion:**

INSERT INTO APPLICATION (ApplicationID, ApplicationDate, Status,
StudentID, OpeningID)

VALUES (1001, DATE '2026-04-24','Pending', 1000, 4001);

INSERT INTO APPLICATION (ApplicationID, ApplicationDate, Status,
StudentID, OpeningID)

VALUES (1002, DATE '2026-05-01', 'Accepted', 1002, 4002);

INSERT INTO APPLICATION (ApplicationID, ApplicationDate, Status,
StudentID, OpeningID)

VALUES (1003, DATE '2026-05-03', 'Rejected', 1003, 4003);

INSERT INTO APPLICATION (ApplicationID, ApplicationDate, Status,
StudentID, OpeningID)

VALUES (1004, DATE '2026-05-10', 'Pending', 1004, 4002);

INSERT INTO APPLICATION (ApplicationID, ApplicationDate, Status,
StudentID, OpeningID)

VALUES (1005, DATE '2026-05-12', 'Accepted', 1005, 4003);

7.  **Interview Insertion:**

INSERT INTO INTERVIEW (InterviewID, InterviewDate, InterviewRound,
Feedback, Result, ApplicationID)

VALUES (100, DATE '2026-05-22','Second round', 'Good communcation
skill', 'Passed', 1001);

INSERT INTO INTERVIEW (InterviewID, InterviewDate, InterviewRound,
Feedback, Result, ApplicationID)

VALUES (101, DATE '2026-05-30', 'Technical Round', 'Strong technical
knowledge', 'Passed', 1002);

INSERT INTO INTERVIEW (InterviewID, InterviewDate, InterviewRound,
Feedback, Result, ApplicationID)

VALUES (102, DATE '2026-06-30', 'Final Round', 'Strong technical
knowledge', 'Passed', 1002);

INSERT INTO INTERVIEW (InterviewID, InterviewDate, InterviewRound,
Feedback, Result, ApplicationID)

VALUES (103, DATE '2026-06-30', 'Final Round', 'No experience',
'Failed', 1004);

8.  **Offer Insertion:**

INSERT INTO OFFER (OfferID, OfferDate, OfferStatus, Salary,
ApplicationID)

VALUES (200, DATE '2026-02-10','Accepted', 25000.00, 1001);

INSERT INTO OFFER (OfferID, OfferDate, OfferStatus, Salary,
ApplicationID)

VALUES (201, DATE '2026-06-05', 'Pending', 28000.00, 1002);

INSERT INTO OFFER (OfferID, OfferDate, OfferStatus, Salary,
ApplicationID)

VALUES (202, DATE '2026-06-05', 'Accepted', 29000.00, 1003);

INSERT INTO OFFER (OfferID, OfferDate, OfferStatus, Salary,
ApplicationID)

VALUES (203, DATE '2026-06-05', 'Rejected', 24000.00, 1004);

9.  **StudentSkill Insertion:**

INSERT INTO STUDENTSKILL (StudentID, SkillID)

VALUES (1000, 5201);

INSERT INTO STUDENTSKILL (StudentID, SkillID)

VALUES (1002, 5202);

INSERT INTO STUDENTSKILL (StudentID, SkillID)

VALUES (1003, 5203);

INSERT INTO STUDENTSKILL (StudentID, SkillID)

VALUES (1004, 5204);

**7. Functional Requirement**

A. **Student**

**Aim:** To display student names, the internship openings they applied
for, the application date, and the current application status.

**User:** Placement staff / system administrator.

SELECT s.StudentName, o.JobTitle, a.ApplicationDate, a.Status

FROM Student s

JOIN Application a ON s.StudentID = a.StudentID

JOIN Opening o ON a.OpeningID = o.OpeningID;

**Screenshot:**

<img src="./images/image13.png" style="width:7.5in;height:3.47569in" />

B. **Company** Openings Report:

**Aim**:

To show which companies are offering internship/job openings.

**User:**

Placement staff / students.

**Query:**

SELECT c.CompanyName, o.JobTitle, o.Deadline

FROM Company c

JOIN Opening o ON c.CompanyID = o.CompanyID;

**Screenshot: OutPut**

<img src="./images/image14.png" style="width:7.5in;height:3.47153in" />

- **Student Skills Report**

**Aim:**

To show students and the skills linked to them.

**User:**

Placement staff / recruiters

**SQL:**

SELECT s.StudentName, sk.SkillName

FROM Student s

JOIN StudentSkill ss ON s.StudentID = ss.StudentID

JOIN Skill sk ON ss.SkillID = sk.SkillID;

**Screenshot:**

<img src="./images/image15.png" style="width:7.5in;height:3.46389in" />

- **Offer Report**

**Aim:**

To show offers made to applicants, including salary and offer status.

**User:**

Placement staff / recruiters.

**SQL:**

SELECT s.StudentName, o.OfferDate, o.OfferStatus, o.Salary

FROM Student s

JOIN Application a ON s.StudentID = a.StudentID

JOIN Offer o ON a.ApplicationID = o.ApplicationID;

**Screenshot:**

<img src="./images/image16.png" style="width:7.5in;height:3.46736in" />

- **Interview**

Aim:

To show interview details, including round, feedback, and result.

User:

Recruiters / placement staff

SQL:

SELECT s.StudentName, i.InterviewDate, i.InterviewRound, i.Feedback,
i.Result

FROM Student s

JOIN Application a ON s.StudentID = a.StudentID

JOIN Interview i ON a.ApplicationID = i.ApplicationID;

Screenshot:

<img src="./images/image17.png" style="width:7.5in;height:3.47014in" />  
**G. Recruiters:**

Aim:

To show each recruiter and the company they work for.

User: Admin / Placement team.

SQL: SELECT r.RecruiterName, r.Email, r.Position, c.CompanyName

FROM Recruiter r

JOIN Company c ON r.CompanyID = c.CompanyID;

Screenshot:

<img src="./images/image18.png" style="width:7.5in;height:3.31667in" />

**8.** **VIEW:**

**\* Student Application**

**Purpose:**

This view simplifies access to application information by combining data
from multiple table into one virtual table.

It can be used by:

- Placement staff

- Administrators

- Recruiters

> For a quick access without rewriting complex JOIN queries.

**Security:**

It can hide unnecessary columns such as:

- StudentID

- OpeningID

- Internal IDs

> And only shows relevant data.

**SQL:**

CREATE VIEW Student_Application_View AS

SELECT s.StudentName, o.JobTitle, a.ApplicationDate, a.Status

FROM Student s

JOIN Application a ON s.StudentID = a.StudentID

JOIN Opening o ON a.OpeningID = o.OpeningID;

QUERY Select:

SELECT \* FROM Student_Application_View;

**Screenshot Output:**

<img src="./images/image19.png" style="width:7.5in;height:3.4625in" />

The result displays:

- Student names

- Job titles they applied for

- Application dated

- Current application status

So, instead of writing multiple JOIN statements each time, the view
allows users to retrieve the same information using a simple:

SELECT \* FROM student_Applicatiom_VIEW

This improves:

- Efficiency

- Readability

- Usability

**Final Conclusion**

- Conclusion

This project successfully designed and implemented a normalized database
system for managing internship and placement processes.

The system includes key entities such as:

- 

- Student

- Company

- Opening

- Application

- Interview

- Offer

- Recruiter

- Skill

The database was designed using:

- Primary keys and Foreign Keys to maintain relationships:

- Normalization techniques to remove redundancy

- Bridge tables (Application and StudentSkill) to resolve many-to-many
  relationships.

The SQL implementation demonstrates:

- Table Creation with constraints

- Data insertion

- Complex queries using JOINS

- Views for simplified data access

The Oracle APEX interface improves usability by:

- Allowing non-technical users to interact with the system

- Providing structured forms and reports

- Reducing the need to write SQL manually

**Reflection**

During the project, I learned

- How to design a real world relational database

- The importance of normalization (1NF, 2NF, 3NF)

- How to resolve many-to many relationships.

- Writing efficient SQL queries

- Building user interfaces using Oracle APEX

**Possible Improvements:**

- Add authentication and user roles (Admin, Recruiter, Student)

- Implement automated notification for application updates

- Add more validation rules (e.g., email format, salary limits)

- Includes analytics dashboards (e.g., success rate of applications)

**Final Statements:**

Overall, the system is scalable, efficient, and meets the requirements
of managing internship and placement processes while ensuring data
integrity and usability.
