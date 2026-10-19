# Workshop / Lab Week 3

Source: [lab 1 part 3.docx](../lab%201%20part%203.docx)

3031ICT/3804ICT — (Applied) Data Mining  
by Dr Can Wang

[Figure: cover-page institutional graphic above the course title; OCR did not recover readable text.]

> The Word document reports 3 pages in its stored metadata. Its questions are preserved in document order below; automatic page wrapping is not reproduced as fixed page boundaries.

## Q1

Briefly compare the following concepts. You may use an example to explain your point(s).

- (a) Snowflake schema, fact constellation.
- (b) Data cleaning, data transformation, refresh.
- (c) Enterprise warehouse, data mart, virtual warehouse.

## Q2

Suppose that a data warehouse consists of the three dimensions time, doctor, and patient, and the two measures count and charge, where charge is the fee that a doctor charges a patient for a visit.

- (a) Enumerate three classes of schemas that are popularly used for modeling data warehouses.
- (b) Draw a schema diagram for the above data warehouse using one of the schema classes listed in (a).
- (c) Starting with the base cuboid [day; doctor; patient], what specific OLAP operations should be performed in order to list the total fee collected by each doctor in 2025?

## Q3

Suppose that a data warehouse for Big University consists of the following four dimensions: student, course, semester, and instructor, and two measures count and avg grade. When at the lowest conceptual level (e.g., for a given student, course, semester, and instructor combination), the avg grade measure stores the actual course grade of the student. At higher conceptual levels, avg grade stores the average grade for the given combination.

- (a) Draw a snowflake schema diagram for the data warehouse.
- (b) Starting with the base cuboid [student; course; semester; instructor], what specific OLAP operations (e.g., roll-up from semester to year) should one perform in order to list the average grade of CS courses for each Big University student.
- (c) If each dimension has five levels (including all), such as "student < major < status < university < all", how many cuboids will this cube contain (including the base and apex cuboids)?

## Q4

Answering the following questions:

- (a) Enumerate three categories of measures, based on the kind of aggregate functions used in computing a data cube.
- (b) What are the main types of data warehouse usage? And what are the differences between them?
- (c) Given the data in the following table, please draw a Bitmap Index table for column “Course”.

| StudentID | Course | Grade |
| --- | --- | --- |
| S1 | 2802ICT | C |
| S2 | 3802ICT | D |
| S3 | 3804ICT | D |
| S4 | 3803ICT | E |
| S5 | 4030ICT | H |

- (d) What is data generalization? Why we need data generalization?
