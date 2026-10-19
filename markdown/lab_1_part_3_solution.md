# Lab 1 Part 3 Solution

Source: [lab 1 part 3 solution.pdf](../lab%201%20part%203%20solution.pdf)

## Page 1

### Q1. Briefly compare the following concepts

You may use an example to explain your point(s).

- (a) Snowflake schema, fact constellation.
- (b) Data cleaning, data transformation, refresh.
- (c) Enterprise warehouse, data mart, virtual warehouse.

**Answer:**

- (a) The snowflake schema and fact constellation are both variants of the star schema model, which consists of a fact table and a set of dimension tables; the snowflake schema contains some normalized dimension tables, whereas the fact constellation contains a set of fact tables that share some common dimension tables.
- (b) Data cleaning is the process of detecting errors in the data and rectifying them when possible. Data transformation is the process of converting the data from heterogeneous sources to a unified data warehouse format or semantics. Refresh is the function propagating the updates from the data sources to the warehouse.
- (c) An enterprise warehouse collects all of the information about subjects spanning the entire organization, whereas a data mart contains a subset of corporate-wide data that is of value to a specific group of users.
  - An enterprise warehouse provides corporate-wide data integration, usually from one or more operational systems or external information providers, and is cross-functional in scope, whereas the data mart is confined to specific selected subjects (such as customer, item, and sales for a marketing data mart).
  - An enterprise warehouse typically contains detailed data as well as summarized data, whereas the data in a data mart tend to be summarized.
  - An enterprise data warehouse may be implemented on traditional mainframes, computer super-servers, or parallel architecture platforms, while data marts are usually implemented on low-cost departmental servers that are UNIX/LINUX- or Windows-based.
  - The implementation cycle of an enterprise warehouse may take months or years, whereas that of a data mart is more likely to be measured in weeks.
  - A virtual warehouse is a set of views over operational databases. For efficient query processing, only some of the possible summary views may be materialized. A virtual warehouse is easy to build but requires excess capacity on operational database servers.

### Q2. Time, doctor, and patient data warehouse

Suppose that a data warehouse consists of the three dimensions time, doctor, and patient, and the two measures count and charge, where charge is the fee that a doctor charges a patient for a visit.

**(a) Enumerate three classes of schemas that are popularly used for modeling data warehouses.**

Answer: The star schema, the snowflake schema, and the fact constellations schema.

**(b) Draw a schema diagram for the above data warehouse using one of the schema classes listed in (a).**

The answer diagram is on page 2.

## Page 2

### Q2(b). Schema diagram

[Figure: star schema with a central fact table connected to time, doctor, and patient dimension tables.]

Text recovered from the embedded diagram:

| Table | Fields recovered |
| --- | --- |
| time dimension table | time_key, day, day_of_week, month, quarter, year |
| fact table | time_key, doctor_id, patient_id |
| doctor dimension table | doctor_id (printed “dooctor_id”), doctor_name, phone#, address, sex |
| patient dimension table | patient_id, patient_name, phone_#, sex, description, address |

### Q2(c). OLAP operations

Starting with the base cuboid [day; doctor; patient], what specific OLAP operations should be performed in order to list the total fee collected by each doctor in 2025?

**Answer:**

- Roll-up on time from day to year.
- Slice for time=2025.
- Roll-up on patient from individual patient to all.

### Q3. Big University data warehouse

Suppose that a data warehouse for Big University consists of the following four dimensions: student, course, semester, and instructor, and two measures (count and avg grade). When at the lowest conceptual level (e.g., for a given student, course, semester, and instructor combination), the avg grade measure stores the actual course grade of the student. At higher conceptual levels, the avg grade stores the average grade for the given combination.

- Draw a snowflake schema diagram for the data warehouse.

The diagram is on page 3.

## Page 3

### Q3. Snowflake schema and OLAP operations

[Figure: Big University snowflake schema with a central univ fact table linked to course, student, semester, and instructor dimensions; the student dimension links to an area table. Some small labels and connecting lines are only partly recovered by OCR.]

| Table | Fields recovered from the diagram |
| --- | --- |
| course dimension table | course_id, course_name, department |
| univ fact table | student_id, course_id, semester_id, instructor_id, count, avg_grade |
| student dimension table | student_id, student_name, area_id, major, status, university |
| area | city, province, country (other small labels unclear) |
| semester dimension table | semester_id, semester, year |
| instructor dimension | instructor_id, dept, rank (heading partly recovered) |

**Starting with the base cuboid [student; course; semester; instructor], what specific OLAP operations (e.g., roll-up from semester to year) should one perform in order to list the average grade of CS courses for each Big University student?**

Answer: The specific OLAP operations to be performed are:

- Roll-up on course from course_id to department.
- Roll-up on student from student_id to university.
- Dice on course, student with department="CS" and university="Big University".
- Drill-down on student from university to student_name.

**If each dimension has five levels (including all), such as "student < major < status < university < all", how many cuboids will this cube contain (including the base and apex cuboids)?**

Answer: This cube will contain `5^4 = 625` cuboids.

### Q4. Answering the following questions

**Enumerate three categories of measures, based on the kind of aggregate functions used in computing a data cube.**

Answer: The three categories of measures are distributive, algebraic, and holistic.

**What are the main types of data warehouse usage? And what are the differences between them?**

Answer: There are three main types of data warehouse usage: information processing, analytical processing, and data mining.

- Information processing involves using queries to find and report useful information using crosstabs, tables, charts, or graphs.
- Analytical processing uses basic OLAP operations such as slice-and-dice, drill-down, roll-up, and pivoting on historical data in order to provide multidimensional analysis of data warehouse data.
- Data mining uses knowledge discovery to find hidden patterns and associations, constructing analytical models, performing classification and prediction, and presenting the mining results using visualization tools.

## Page 4

### Q4. Bitmap index

Given the data in the following table, please draw a Bitmap Index table for column “Course”.

| StudentID | Course | Grade |
| --- | --- | --- |
| S1 | 2802ICT | C |
| S2 | 3802ICT | D |
| S3 | 3804ICT | D |
| S4 | 3803ICT | E |
| S5 | 4030ICT | H |

**Answer: Index on Course:**

| RecID | 2802ICT | 3802ICT | 3803ICT | 3804ICT | 4030ICT |
| --- | --- | --- | --- | --- | --- |
| S1 | 1 | 0 | 0 | 0 | 0 |
| S2 | 0 | 1 | 0 | 0 | 0 |
| S3 | 0 | 0 | 0 | 1 | 0 |
| S4 | 0 | 0 | 1 | 0 | 0 |
| S5 | 0 | 0 | 0 | 0 | 1 |

### Q4. Data generalization

What is data generalization? Why we need data generalization?

Answer: Data generalization summarizes data by replacing relatively low-level values with higher-level concepts or by reducing the number of dimensions to summarize data in concept space involving fewer dimensions.

Given the large amount of data stored in databases, it is useful to be able to describe concepts in concise and succinct terms at generalized (rather than low) levels of abstraction.
