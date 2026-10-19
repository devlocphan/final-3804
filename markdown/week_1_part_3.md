## Slide 1
### Lecture Week 3: Data Warehouse and Online Analytical Processing

3031ICT: Applied Data Mining  
3804ICT: Data Mining

Dr Can Wang  
School of Information and Communication Technology

## Slide 2
### Contents

- Data Warehouse: Basic Concepts.
- Data Warehouse Modeling: Data Cube and OLAP.
- Data Warehouse Implementation.
- Data Generalization by Attribute-Oriented Induction.
- Summary.

## Slide 3
### What is a Data Warehouse?

- Defined in many different ways, but not rigorously.
  - A decision support database that is maintained separately from the organization’s operational database.
  - Support information processing by providing a solid platform of consolidated, historical data for analysis.
- “A data warehouse is a subject-oriented, integrated, time-variant, and nonvolatile collection of data in support of management’s decision-making process.” — William H. Inmon.
  - An American computer scientist, recognized by many as the father of the data warehouse.
- Data warehousing:
  - The process of constructing and using data warehouses.

## Slide 4
### Data Warehouse—Subject-Oriented

- Organizes around major subjects, such as customer, product, sales.
- Focuses on the modeling and analysis of data for decision makers, not on daily operations or transaction processing.
- Provides a simple and concise view around particular subject issues by excluding data that are not useful in the decision support process.
- E.g. “sales” can be a particular subject to be analyzed.

## Slide 5
### Data Warehouse—Integrated

- Constructed by integrating multiple, heterogeneous data sources (multiple data sources), such as
  - Relational databases, flat files, on-line transaction records.
- Data cleaning and data integration techniques are applied.
  - Ensure consistency in naming conventions, encoding structures, attribute measures, etc. among different data sources.
    - E.g. source A and source B may have different ways of identifying a product, but in a data warehouse, there will be only a single way of identifying a product.
  - When data is moved to the warehouse, it is converted.

## Slide 6
### Data Warehouse—Time Variant

- The time horizon for the data warehouse is significantly longer than that of operational systems.
  - Operational database: current or most recent value data.
  - Data warehouse data: provide information from a historical perspective (e.g., past 5–10 years).
- Every key structure in the data warehouse
  - Contains an element of time, explicitly or implicitly.
  - But the key of operational data may or may not contain “time element”.

## Slide 7
### Data Warehouse—Nonvolatile

- A physically separate store of data transformed from the operational environment.
- Operational update of data does not occur in the data warehouse environment.
  - Historical data in a data warehouse should never be altered.
  - Does not require transaction processing, recovery, and concurrency control mechanisms.
  - Requires only two operations in data accessing:
    - Initial loading of data and access of data.

## Slide 8
### Why a Separate Data Warehouse?

- High performance for both systems (operational vs warehouse)
  - DBMS—tuned for OLTP: access methods, indexing, concurrency control, recovery.
  - Warehouse—tuned for OLAP: complex OLAP queries, multidimensional view, consolidation.
- Different functions and different data:
  - Missing data: Decision support requires historical data which operational DBs do not typically maintain.
  - Data consolidation: DS requires consolidation (aggregation, summarization) of data from heterogeneous sources which operational DBs have raw data.
  - Data quality: Different sources typically use inconsistent data representations, codes and formats which have to be reconciled.

## Slide 9
### Data Warehouse: A Multi-Tiered Architecture

- The top tier is a front-end client layer, which contains query and reporting tools, analysis tools, and/or data mining tools (e.g., trend analysis, prediction, visualization, and so on).
- The middle tier is an OLAP server that is typically implemented using either (1) a relational OLAP (ROLAP) model; or (2) a multidimensional OLAP (MOLAP) model.
- The bottom tier is a warehouse database server that is almost always a relational database system. This tier also contains a metadata repository, which stores information about the data warehouse and its contents.
- Back-end tools and utilities perform data extraction, cleaning, and transformation (e.g., to merge similar data from different sources into a unified format), as well as load and refresh functions to update the data warehouse (ETL process).

[Figure: Operational databases and External sources feed Extract, Clean, Transform, Load and Refresh tools. These populate a Data warehouse and Data marts, with Metadata, Monitoring and Administration. The bottom tier is the Data warehouse server; the middle tier is the OLAP server; the top tier consists of Front-end tools labeled Query/report, Analysis, and Data mining.]

## Slide 10
### Extraction, Transformation, and Loading (ETL)

- Data extraction
  - Get data from multiple, heterogeneous, and external sources.
- Data cleaning (process missing, inconsistent, noisy, …)
  - Detect errors in the data and rectify them when possible.
- Data transformation
  - Convert data from legacy or host format to warehouse format.
- Load
  - Sort, summarize, consolidate, compute views, check integrity, and build index and partitions.
- Refresh
  - Propagate the updates from the data sources to the warehouse.

## Slide 11
### Three Data Warehouse Models

From the architecture point of view, there are three data warehouse models:

- Enterprise warehouse
  - Collects all of the information about subjects spanning the entire organization.
  - Provides corporate-wide data integration, usually from one or more operational systems or external information providers.
  - Requires extensive business modeling and may take years to design and build.
- Data Mart
  - A subset of corporate-wide data that is of value to a specific groups of users.
  - Its scope is confined to specific, selected groups, such as marketing data mart.
  - The implementation cycle is more likely to be measured in weeks.
  - Depending on the source of data, data marts can be categorized as
    - Independent (from one or more operational systems or external information providers).
    - Dependent (directly from warehouse) data mart.
- Virtual warehouse
  - A set of views over operational databases.
  - Only some of the possible summary views may be materialized.

## Slide 12
### Data Warehousing and On-line Analytical Processing

- Data Warehouse: Basic Concepts.
- Data Warehouse Modeling: Data Cube and OLAP.
- Data Warehouse Implementation.
- Data Generalization by Attribute-Oriented Induction.
- Summary.

## Slide 13
### Multidimensional Data Model

- The multidimensional data model
  - An integral part of OLAP.
  - Designed to solve complex queries in real time.
  - Allows users to understand databases easily.
  - Facilitates applications to efficiently access databases.
  - Contains:
    - Data cubes (data structure).
    - Measures.
    - Dimensions.
    - Hierarchies.
    - Levels.

## Slide 14
### From Tables and Spreadsheets to Data Cubes

- A data warehouse is based on a multidimensional data model which views data in the form of a data cube.
- A data cube, such as sales, allows data to be modeled and viewed in multiple dimensions, e.g. time, item, branch, and location (buy bread, morning, Coles).
  - Dimension table
    - Further describes dimension, such as item (item_name, brand, type), or time (day, week, month, quarter, year) or customer (cust_id, cust_firstname, cust_lastname, contact).
  - Fact table contains measures (such as dollars_sold) and keys to each of the related dimension tables such as sale_records (item, time, cust_id, product_id, quantity).

## Slide 15
### From Tables and Spreadsheets to Data Cubes

Table 4.2: 2-D View of Sales Data for AllElectronics According to time and item. Location = “Vancouver”.

| Time (quarter) | Home entertainment | Computer | Phone | Security |
| --- | --- | --- | --- | --- |
| Q1 | 605 | 825 | 14 | 400 |
| Q2 | 680 | 952 | 31 | 512 |
| Q3 | 812 | 1023 | 30 | 501 |
| Q4 | 927 | 1038 | 38 | 580 |

Note: The sales are from branches located in the city of Vancouver. The measure displayed is dollars_sold (in thousands).

- In this 2-D representation, the sales for Vancouver are shown with respect to the time dimension (organized in quarters) and the item dimension (organized according to the types of items sold). The fact or measure displayed is dollars sold (in thousands).

## Slide 16
### From Tables and Spreadsheets to Data Cubes

Table 4.3: 3-D View of Sales Data for AllElectronics According to time, item, and location.

Location = “Chicago”:

| Time | Home ent. | Comp. | Phone | Sec. |
| --- | --- | --- | --- | --- |
| Q1 | 854 | 882 | 89 | 623 |
| Q2 | 943 | 890 | 64 | 698 |
| Q3 | 1032 | 924 | 59 | 789 |
| Q4 | 1129 | 992 | 63 | 870 |

Location = “New York”:

| Time | Home ent. | Comp. | Phone | Sec. |
| --- | --- | --- | --- | --- |
| Q1 | 1087 | 968 | 38 | 872 |
| Q2 | 1130 | 1024 | 41 | 925 |
| Q3 | 1034 | 1048 | 45 | 1002 |
| Q4 | 1142 | 1091 | 54 | 984 |

Location = “Toronto”:

| Time | Home ent. | Comp. | Phone | Sec. |
| --- | --- | --- | --- | --- |
| Q1 | 818 | 746 | 43 | 591 |
| Q2 | 894 | 769 | 52 | 682 |
| Q3 | 940 | 795 | 58 | 728 |
| Q4 | 978 | 864 | 59 | 784 |

Location = “Vancouver”:

| Time | Home ent. | Comp. | Phone | Sec. |
| --- | --- | --- | --- | --- |
| Q1 | 605 | 825 | 14 | 400 |
| Q2 | 680 | 952 | 31 | 512 |
| Q3 | 812 | 1023 | 30 | 501 |
| Q4 | 927 | 1038 | 38 | 580 |

Note: The measure displayed is dollars_sold (in thousands).

- Now, suppose that we would like to view the sales data with a third dimension. For instance, suppose we would like to view the data, according to time and item, as well as location, for the cities Chicago, New York, Toronto, and Vancouver. The 3-D data in the table are represented as a series of 2-D tables. Conceptually, we may also represent the same data in the form of a 3-D data cube.

## Slide 17
### From Tables and Spreadsheets to Data Cubes

[Figure: A 3-D data cube representation of the data in Table 4.3, according to time, item, and location. The measure displayed is dollars_sold (in thousands). Axes are time (quarters Q1–Q4), item (types: home entertainment, computer, phone, security), and location (cities: Vancouver, Toronto, New York, Chicago). The visible front and upper faces contain the following values.]

Front face, Vancouver:

| Time | Home entertainment | Computer | Phone | Security |
| --- | --- | --- | --- | --- |
| Q1 | 605 | 825 | 14 | 400 |
| Q2 | 680 | 952 | 31 | 512 |
| Q3 | 812 | 1023 | 30 | 501 |
| Q4 | 927 | 1038 | 38 | 580 |

Upper face, Q1:

| Location | Home entertainment | Computer | Phone | Security |
| --- | --- | --- | --- | --- |
| Chicago | 854 | 882 | 89 | 623 |
| New York | 1087 | 968 | 38 | 872 |
| Toronto | 818 | 746 | 43 | 591 |
| Vancouver | 605 | 825 | 14 | 400 |

## Slide 18
### Cube: A Lattice of Cuboids

- Given a set of dimensions, we can generate a cuboid for each of the possible subsets of the given dimensions. The result would form a lattice of cuboids, each showing the data at a different level of summarization, or group-by. The lattice of cuboids is then referred to as a data cube.

The 0-D cuboid, which holds the highest level of summarization, is called the apex cuboid. In our example, this is the total sales, or dollars sold, summarized over all four dimensions. The apex cuboid is typically denoted by all.

The cuboid that holds the lowest level of summarization is called the base cuboid.

This example shows a lattice of cuboids forming a data cube for the dimensions time, item, location, and supplier.

[Figure: Lattice of cuboids, making up a 4-D data cube for time, item, location, and supplier. Each cuboid represents a different degree of summarization. Edges connect each subset to supersets formed by adding one dimension.]

- 0-D (apex) cuboid: all.
- 1-D cuboids: time; item; location; supplier.
- 2-D cuboids: time, item; time, location; time, supplier; item, location; item, supplier; location, supplier.
- 3-D cuboids: time, item, location; time, item, supplier; time, location, supplier; item, location, supplier.
- 4-D (base) cuboid: time, item, location, supplier.

## Slide 19
### Conceptual Modeling of Data Warehouses

- Three forms of multidimensional model in data warehouse
  - Star schema: A fact table in the middle connected to a set of dimension tables.
  - Snowflake schema: A refinement of star schema where some dimensional hierarchy is normalized into a set of smaller dimension tables, forming a shape similar to snowflake.
  - Fact constellations: Multiple fact tables share dimension tables, viewed as a collection of stars, therefore called galaxy schema or fact constellation.

## Slide 20
### Measures

- A measure is an attribute on which aggregate calculations (sum, max, min, mean, etc.) can be made.

Car_sales table:

| Receipt_no | Make | Color | Size | Date | Price |
| --- | --- | --- | --- | --- | --- |
| 0001 | Toyota | white | small | 01/01/01 | 20000 |
| 0002 | Nissan | red | Medium | 01/01/01 | 25000 |
| 0003 | Holden | silver | Medium | 01/02/01 | 299000 |

Is “Date” a measure?

## Slide 21
### Example of Star Schema

[Figure: A central Sales Fact Table connects directly to the time, item, branch, and location dimension tables using their corresponding keys.]

| Table | Fields |
| --- | --- |
| Sales Fact Table | time_key; item_key; branch_key; location_key; units_sold; dollars_sold; avg_sales |
| time | time_key; day; day_of_the_week; month; quarter; year |
| item | item_key; item_name; brand; type; supplier_type |
| branch | branch_key; branch_name; branch_type |
| location | location_key; street; city; state_or_province; country |

Measures: units_sold, dollars_sold, avg_sales.

## Slide 22
### Example of Snowflake Schema

[Figure: Sales Fact Table connects to time, item, branch, and location. Item links onward to supplier; location links onward to city, normalizing the dimensional hierarchies.]

| Table | Fields |
| --- | --- |
| Sales Fact Table | time_key; item_key; branch_key; location_key; units_sold; dollars_sold; avg_sales |
| time | time_key; day; day_of_the_week; month; quarter; year |
| item | item_key; item_name; brand; type; supplier_key |
| supplier | supplier_key; supplier_type |
| branch | branch_key; branch_name; branch_type |
| location | location_key; street; city_key |
| city | city_key; city; state_or_province; country |

Measures: units_sold, dollars_sold, avg_sales.

## Slide 23
### Example of Fact Constellation

[Figure: Sales and Shipping fact tables share time, item, and location dimensions. Sales also links to branch. Shipping links to shipper and to location for both from_location and to_location. Shipper also has a location_key.]

| Table | Fields |
| --- | --- |
| Sales Fact Table | time_key; item_key; branch_key; location_key; units_sold; dollars_sold; avg_sales |
| Shipping Fact Table | time_key; item_key; shipper_key; from_location; to_location; dollars_cost; units_shipped |
| time | time_key; day; day_of_the_week; month; quarter; year |
| item | item_key; item_name; brand; type; supplier_type |
| branch | branch_key; branch_name; branch_type |
| location | location_key; street; city; province_or_state; country |
| shipper | shipper_key; shipper_name; location_key; shipper_type |

Measures shown: units_sold, dollars_sold, avg_sales; dollars_cost, units_shipped.

## Slide 24
### A Concept Hierarchy: Dimension (Location)

- A concept hierarchy defines a sequence of mappings, from a set of low-level concepts to higher-level, more general concepts.

[Figure: A hierarchy with levels all → region → country → city → office. The all root branches to Europe and North_America, with ellipses for additional concepts. Europe includes Spain and Germany; North_America includes Canada and Mexico. City examples include Frankfurt under Germany, and Vancouver and Toronto under Canada. Office examples include L. Chan and M. Wind, with ellipses for additional offices.]

## Slide 25
### A Concept Hierarchy: Dimension (Time & Location)

- A hierarchy is a way to organize data at different levels of aggregation.
- A level represents a position in the hierarchy.
- For each dimension, the set of values can be organized in a hierarchy.
  - E.g., assuming the sales table includes time and location dimension.
- The hierarchies represent different levels of details for attributes.

[Figure: Time hierarchy Year → quarter → month → day; a second path goes through week to day. Location hierarchy Region → country → state → city. The bottom is labeled “Base level (most detailed)”.]

## Slide 26
### Data Cube Measures: Three Categories

“How are measure values computed?” — by measure functions.

A data cube measure is a numeric function that can be evaluated at each point in the data cube space. The types of measure can be:

- Distributive: if the result derived by applying the function to n aggregate values is the same as that derived by applying the function on all the data without partitioning.
  - E.g., count(), sum(), min(), max().
- Algebraic: if it can be computed by an algebraic function with M arguments (where M is a bounded integer), each of which is obtained by applying a distributive aggregate function.
  - E.g., avg(), min_N(), standard_deviation().
- Holistic: if there is no constant bound on the storage size needed to describe a subaggregate.
  - E.g., median(), mode(), rank().

## Slide 27
### Typical OLAP Operations

“How are concept hierarchies useful in OLAP?”

- In the multidimensional model, data are organized into multiple dimensions (e.g. time, item, location, supplier), and each dimension contains multiple levels of abstraction defined by concept hierarchies. This organization provides users with the flexibility to view data from different perspectives.
- A number of OLAP data cube operations exist to materialize these different views, allowing interactive query and analysis of the data at hand. Hence, OLAP provides a user-friendly environment for interactive data analysis.
- Operations include:
  - Roll up (drill-up).
  - Drill down (roll down).
  - Slice and dice.
  - Pivot (rotate).
  - And more.

## Slide 28
### Typical OLAP Operations – Roll-up

- Roll-up performs aggregation on a data cube
  - By climbing up a concept hierarchy for a dimension.
  - Or by dimension reduction.
- Example: Roll-up is performed by climbing up a concept hierarchy for the dimension location.
- Initially, the concept hierarchy was defined as the total order “street < city < state < country”.
- The data is grouped into cities rather than countries.
- On rolling up, the data is aggregated by ascending the location hierarchy from the level of city to the level of country.
- When roll-up is performed, one or more dimensions from the data cube can be removed.

[Figure: Roll-up on location from cities (Chicago, New York, Toronto, Vancouver) to countries (USA, Canada). Other axes are item (types: Mobile, Modem, Phone, Security) and time (quarters Q1–Q4). Small cell values in the perspective cubes are not reliably recoverable by OCR.]

Legible Q1/Mobile values in the illustration:

| City | Before roll-up | Country | After roll-up |
| --- | --- | --- | --- |
| Chicago | 440 | USA | 2000 |
| New York | 1560 | | |
| Toronto | 395 | Canada | 1000 |
| Vancouver | 605 | | |

The visible Vancouver/Q1 row is Mobile 605, Modem 825, Phone 14, Security 400.

## Slide 29
### Typical OLAP Operations – Drill-down

- Drill-down is the reverse operation of roll-up. It is performed by
  - By stepping down a concept hierarchy for a dimension.
  - Or by introducing a new dimension.
- Example: Drill-down is performed by stepping down a concept hierarchy for the dimension time.
- Initially, the concept hierarchy was defined as “day < month < quarter < year.”
- On drilling down, the time dimension is descended from the level of quarter to the level of month.
- When drill-down is performed, one or more dimensions from the data cube are added.
- It navigates the data from less detailed data to highly detailed data.

[Figure: Drill-down on time from quarters to months. Location labels: Chicago, New York, Toronto, Vancouver. Item labels: Mobile, Modem, Phone, Security. Time changes from Q1–Q4 to individual months. Small perspective-cube cell values are not reliably recoverable by OCR.]

Month labels: January, February, March, April, May, June, July, August, September, October, November, December. The visible Vancouver/Q1 row before drill-down is Mobile 605, Modem 825, Phone 14, Security 400.

## Slide 30
### Typical OLAP Operations – Slice

- The slice operation selects one particular dimension from a given cube and provides a new sub-cube.
- Here Slice is performed for the dimension time using the criterion time = “Q1”.
- It will form a new sub-cube by selecting one dimension.

[Figure: A time–item–location cube is sliced at Q1, yielding a two-dimensional item/location plane. Location labels: Chicago, New York, Toronto, Vancouver. Item labels: Mobile, Modem, Phone, Security. The source cube has quarters Q1–Q4. Small cell values are not reliably recoverable by OCR.]

## Slide 31
### Typical OLAP Operations – Dice

- Dice selects two or more dimensions from a given cube and provides a new sub-cube.
- Example: The dice operation on the cube based on the following selection criteria involves three dimensions.
  - (location = “Toronto” or “Vancouver”).
  - (time = “Q1” or “Q2”).
  - (item = “Mobile” or “Modem”).

[Figure: Dice for (location = “Toronto” or “Vancouver”) and (time = “Q1” or “Q2”) and (item = “Mobile” or “Modem”). A smaller cube retains those two values on each axis. The original cube additionally includes Chicago, New York, Q3, Q4, Phone, and Security. Small cell values are not reliably recoverable by OCR.]

## Slide 32
### Typical OLAP Operations – Pivot

- The pivot operation is also known as rotation. It rotates the data axes in view in order to provide an alternative presentation of data.

[Figure: Pivot exchanges the item and location axes of a two-dimensional view. Before rotation, rows are Chicago, New York, Toronto, Vancouver and columns are Mobile, Modem, Phone, Security; afterward the cities form columns. Axes are labeled Locations (cities), item (types), and Location (Cities). Small cell values are not reliably recoverable by OCR.]

The legible Vancouver values, 605, 825, 14, 400, move from the Vancouver row to the Vancouver column, aligned respectively with Mobile, Modem, Phone, and Security.

## Slide 33
### Typical OLAP Operations

- Roll up (drill-up): summarize data
  - By climbing up hierarchy or by dimension reduction.
- Drill-down (roll-down): reverse of roll-up
  - From higher level summary to lower level summary or detailed data, or introducing new dimensions.
- Slice and dice: project and select.
- Pivot (rotate):
  - Reorient the cube, visualization, transform a 3D cube to a series of 2D planes.
- Other operations
  - Drill across: involving (across) more than one fact table.
  - Drill through: through the bottom level of the cube to its back-end relational tables (using SQL).

## Slide 34
### Examples of Typical OLAP Operatiobs on Multidimensional Data

[Figure: Combined OLAP diagram illustrates roll-up, drill-down, slice, dice, and pivot on sales data. Dimensions are location (cities Chicago, New York, Toronto, Vancouver), time (quarters Q1–Q4), and item (types home entertainment, computer, phone, security). Roll-up groups cities into countries; drill-down expands quarters into months; slicing selects Q1; dicing selects (location = “Toronto” or “Vancouver”) and (time = “Q1” or “Q2”) and (item = “home entertainment” or “computer”); pivot reorients the item/location view. Fine numeric cell labels are not reliably recoverable by OCR.]

Country labels: USA, Canada. Month labels: January, February, March, April, May, June, July, August, September, October, November, December.

## Slide 35
### Data Warehousing and On-line Analytical Processing

- Data Warehouse: Basic Concepts.
- Data Warehouse Modeling: Data Cube and OLAP.
- Data Warehouse Implementation.
- Data Generalization by Attribute-Oriented Induction.
- Summary.

## Slide 36
### Efficient Data Cube Computation

- Data cube can be viewed as a lattice of cuboids.
  - The bottom-most cuboid is the base cuboid.
  - The top-most cuboid (apex) contains only one cell.
  - How many cuboids in an n-dimensional cube with L levels?

$$T=\prod_{i=1}^{n}(L_i+1).$$

Where $L_i$ is the number of levels associated with dimension i. One is added to include the virtual top level, all.

  - If the cube has 10 dimensions, each of which has 5 levels (including all, the virtual top level), total number of cuboids can be $5^{10}\approx9.8\times10^6$.
- Materialization of data cube
  - Materialize every (cuboid) (full materialization), none (no materialization), or some (partial materialization).
  - Selection of which cuboids to materialize
    - Based on size, sharing, access frequency, etc.

## Slide 37
### Indexing OLAP Data: Bitmap Index

To facilitate efficient data accessing, most data warehouse systems support index structures and materialized views (using cuboids).

- Index on a particular column.
- Each value in the column has a bit vector: bit-op is fast.
- The length of the bit vector: # of records in the base table.
- The i-th bit is set to 1, if the i-th row of the base table has the value for the indexed column.

Base table:

| Cust | Region | Type |
| --- | --- | --- |
| C1 | Asia | Retail |
| C2 | Europe | Dealer |
| C3 | Asia | Dealer |
| C4 | America | Retail |
| C5 | Europe | Dealer |

Index on Region:

| RecID | Asia | Europe | America |
| --- | --- | --- | --- |
| 1 | 1 | 0 | 0 |
| 2 | 0 | 1 | 0 |
| 3 | 1 | 0 | 0 |
| 4 | 0 | 0 | 1 |
| 5 | 0 | 1 | 0 |

Index on Type:

| RecID | Retail | Dealer |
| --- | --- | --- |
| 1 | 1 | 0 |
| 2 | 0 | 1 |
| 3 | 0 | 1 |
| 4 | 1 | 0 |
| 5 | 0 | 1 |

## Slide 38
### OLAP Server Architectures

- Relational OLAP (ROLAP)
  - Use relational or extended-relational DBMS to store and manage warehouse data and OLAP middle ware.
  - Include optimization of DBMS backend, implementation of aggregation navigation logic, and additional tools and services.
  - Greater scalability.
- Multidimensional OLAP (MOLAP)
  - Sparse array-based multidimensional storage engine.
  - Fast indexing to pre-computed summarized data.
- Hybrid OLAP (HOLAP) (e.g., Microsoft SQLServer)
  - Flexibility, e.g., low level: relational, high-level: array.

## Slide 39
### ROLAP VS MOLAP

| # | MOLAP | ROLAP |
| --- | --- | --- |
| 1 | Information retrieval is fast. | Information retrieval is comparatively slow. |
| 2 | Uses sparse array to store datasets. | Uses relational table. |
| 3 | Easy to use for beginners. | Comparatively difficult to use for beginners. |
| 4 | Maintains a separate database for data cubes. | It may not require space other than available in the Data warehouse. |

## Slide 40
### Data Warehousing and On-line Analytical Processing

- Data Warehouse: Basic Concepts.
- Data Warehouse Modeling: Data Cube and OLAP.
- Data Warehouse Implementation.
- Data Generalization by Attribute-Oriented Induction.
- Summary.

## Slide 41
### Attribute-Oriented Induction

- The attribute-oriented induction (AOI) approach on concept description was proposed in 1989 (KDD ’89 workshop).
- Not confined to categorical data nor particular measures.
- How is it done?
  - Collect the task-relevant data (initial relation) using a relational database query.
  - Perform generalization by attribute removal or attribute generalization.
  - Apply aggregation by merging identical, generalized tuples and accumulating their respective counts.
  - Interact with users for knowledge presentation by mapping generalized relation into different forms (e.g. charts or rules).

## Slide 42
### Basic Principles of Attribute-Oriented Induction

- Data focusing: task-relevant data, including dimensions, and the result is the initial relation.
- Attribute-removal: remove attribute A if there is a large set of distinct values for A but (1) there is no generalization operator on A, or (2) A’s higher-level concepts are expressed in terms of other attributes.
- Attribute-generalization: If there is a large set of distinct values for A, and there exists a set of generalization operators on A, then select an operator and generalize A.
- Attribute-threshold control: typical 2–8, specified/default.
- Generalized relation threshold control: control the final relation/rule size.

## Slide 43
### Attribute-Oriented Induction: An Example

Example: Describe the general characteristics of graduate students in the University database.

- Step 1. Fetch relevant set of data using an SQL statement, e.g.,

```sql
Select * (i.e., name, gender, major, birth_place, birth_date,
          residence, phone#, gpa)
from student
where student_status in {“Msc”, “MBA”, “PhD”}
```

- Step 2. Perform attribute-oriented induction.
- Step 3. Present results in generalized relation, cross-tab, or rule forms.

## Slide 44
### Class Characterization: An Example

Initial Relation:

| Name | Gender | Major | Birth-Place | Birth_date | Residence | Phone # | GPA |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Jim Woodman | M | CS | Vancouver, BC, Canada | 8-12-76 | 3511 Main St., Richmond | 687-4598 | 3.67 |
| Scott Lachance | M | CS | Montreal, Que, Canada | 28-7-75 | 345 1st Ave., Richmond | 253-9106 | 3.70 |
| Laura Lee | F | Physics | Seattle, WA, USA | 25-8-70 | 125 Austin Ave., Burnaby | 420-5232 | 3.83 |
| … | … | … | … | … | … | … | … |

[Figure: Attribute-oriented induction transforms the initial relation into the prime generalized relation. Per-column transformations are listed below.]

| Initial attribute | Transformation |
| --- | --- |
| Name | Removed |
| Gender | Retained |
| Major | Sci, Eng, Bus |
| Birth-Place | Country |
| Birth_date | Age range |
| Residence | City |
| Phone # | Removed |
| GPA | Excl, VG, … |

Prime Generalized Relation:

| Gender | Major | Birth_region | Age_range | Residence | GPA | Count |
| --- | --- | --- | --- | --- | --- | --- |
| M | Science | Canada | 20–25 | Richmond | Very-good | 16 |
| F | Science | Foreign | 25–30 | Burnaby | Excellent | 22 |
| … | … | … | … | … | … | … |

Cross-tabulation:

| Gender / Birth_Region | Canada | Foreign | Total |
| --- | --- | --- | --- |
| M | 16 | 14 | 30 |
| F | 10 | 22 | 32 |
| Total | 26 | 36 | 62 |

## Slide 45
### Summary

- Data warehousing: A multi-dimensional model of a data warehouse
  - A data cube consists of dimensions & measures.
  - Star schema, snowflake schema, fact constellations.
  - OLAP operations: drilling, rolling, slicing, dicing and pivoting.
- Data Warehouse Architecture
  - Multi-tiered architecture.
- Implementation: Efficient computation of data cubes
  - Indexing OLAP data: Bitmap index and join index.
  - OLAP servers: ROLAP, MOLAP, HOLAP.
- Data generalization: Attribute-oriented induction.

## Slide 46
### Have a question?
