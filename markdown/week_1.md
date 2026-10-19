## Slide 1
### Lecture Week 1: An Overview of Data Mining

3031ICT: Applied Data Mining  
3804ICT: Data Mining

Dr Can Wang  
School of Information and Communication Technology

## Slide 2
### Learning Outcomes

At the end of this lecture, you will be able to:

- Understand general information of this course, including
  - The structure, arrangement, timeframe, etc.
- Understand what data mining is.
- Understand why we need data mining.
- Understand what data mining can do.

## Slide 3
### Course Information

- Course Convenor: Dr Can Wang
  - I am a Senior Lecturer of Computer Science at Griffith University. My research interests include various topics of Data Analytics, Artificial Intelligence, Machine Learning, Big Data, and etc.
- Homepage: https://experts.griffith.edu.au/7760-can-wang
- Email: can.wang@griffith.edu.au
- Tel: 61-07-567 80423
- Office: G09 1.70 (make an appointment by email).

## Slide 4
### Course Information

The course has TWO major parts:

- Lectures – Introduction to the main topics
  - Academic topics at a theoretical/introductory level.
  - Hands-on examples/demos for better understanding.
- Labs/workshops – Practical exercises/topic discussions (from Week 1)
  - Practical implementations of algorithms.
  - Data mining for real-world problems.
  - Lecture topic extensions/discussions.

## Slide 5
### Course Information

The assessment has THREE major parts:

- TWO Assignments (15% + 35%):
  - In this project assignment, you will team up (min 2 students, max 3 students).
  - To apply the data mining algorithms to solve some real-world problems.
  - A project proposal (Group Work) is due by week 6 (briefly describing the project), worth 15%.
  - A final project report (Individual Work) is due by week 11, worth 35%.
  - More details on Assessment Overview page from Learning@Griffith.
- Final Exam (50%):
  - Standard 2-hour open book online exam.
  - Reading time: 10 minutes, Duration: 120 minutes.

## Slide 6
### Course Information

Course Structure:

- Module 1: Data mining, exploration and storage
  - Topic 1.1: An Overview of Data Mining (covered in Week 1).
  - Topic 1.2: Explore Data and Pre-process Data (covered in Week 2).
  - Topic 1.3: Data Warehouse and OLAP (covered in Week 3).
- Module 2: Mining frequent patterns
  - Topic 2.1: Mining Frequent Patterns I (covered in Week 4).
  - Topic 2.2: Mining Frequent Patterns II (covered in Week 5).
- Module 3: Machine learning
  - Topic 3.1: Machine Learning in Data Mining (covered in Week 6).
- Module 4: Advanced data sets
  - Topic 4.1: Outlier Detection (covered in Week 7).
  - Topic 4.2: Time Series and Sequential Data Mining (covered in Week 8).
  - Topic 4.3: Text Database Mining (covered in Week 9).
- Module 5: Network analysis
  - Topic 5.1: World-Wide-Web Mining (covered in Week 10).
  - Topic 5.2: Data Mining on Information Networks (covered in Week 11).
- Module 6: Review and assessment support.

## Slide 7
### Course Information

- Recommended Textbooks & Materials (Google or Griffith Library):
  - *Web Data Mining: Exploring Hyperlinks, Contents and Usage Data*. By Bing Liu, Second Edition, Springer, ISBN 978-3-642-19459-7.
  - *Data Mining: Concepts and Techniques*. 3rd Edition. By Jiawei Han.

[Figure: Covers of the two recommended textbooks.]

## Slide 8
### Assessment Rules

- The standard penalty for delayed assessment is the reduction of the mark allocated to the assessment item by 5% of the total weighted mark for the assessment item, for each calendar day that the item is late.
- Assessment items submitted more than seven calendar days after the due date are awarded zero mark.

## Slide 9
### What if you can’t attend an assessment?

- Project Assignments (Assessment Tasks 1 & 2): If for any valid reason (e.g. being sick), you need an extension for Assignment, you must apply for an extension by using the Griffith online system Assignment Extension (don’t forget to scan and attach your evidence, e.g. medical certificate) before the deadline and attach the extension approval letter to your assignment when you submit.

## Slide 10
### Introduction to Data Mining

## Slide 11
### Why Data Mining?

There has been enormous data growth in both commercial and scientific databases due to advances in data generation and collection technologies.

[Figure: Circular infographic titled “Data We Create Online in 60 Seconds,” centered on “60.” Its category labels and quantities are transcribed below. The Texts quantity is faint and remains uncertain after full-page, enlarged-image, and contrast-enhanced OCR.]

| Category | In 60 seconds |
| --- | --- |
| Snaps | 4.3 million |
| Videos | 500 hours |
| Texts | 16 million (faint; OCR uncertain) |
| Tweets | 347,200 |
| Spent on Amazon | $443,000 |
| Photos | 66,000 |
| Google | 5.9 million |
| Emails | 231.4 million |

## Slide 12
### Why Data Mining?

Petabyte: a unit of information equal to one thousand million million ($10^{15}$) bytes.

Big Data Definition (5Vs):

- Volume – E.g. eBay uses two data warehouses at 7.5 petabytes and 40 petabytes.
- Variety – E.g. Facebook has 50 billion photos, Youtube has over 6 billion hours of video watched each month.
- Velocity – E.g. Coles handles more than 1 million customer transactions every hour (more than 2.5 petabytes of data).
- Variability – This refers to the inconsistency of data, thus hampering the process of being able to handle and manage the data effectively.
- Veracity – Accuracy of analysis depends on the veracity of the source data (Probability & Fuzzy Theories).

## Slide 13
### Why Data Mining? Commercial Viewpoint

- Lots of data is being collected and warehoused
  - Web data
    - Yahoo has petabytes of web data.
    - Facebook has billions of active users.
  - Purchases at department/grocery stores, E-commerce
    - Amazon handles millions of visits per day.
  - Bank/Credit Card transactions.
- Computers have become cheaper and more powerful.
- Competitive Pressure is Strong
  - Need to provide better, customized services for an edge (e.g. in Customer Relationship Management).

[Figure: Commercial examples illustrated by company and transaction imagery.]

## Slide 14
### Introduction

- What Is Data Mining?
- What Kind of Data Can Be Mined?
- What Kind of Patterns Can Be Mined?
- What Technologies Are Used?
- What Kind of Applications Are Targeted?
- Major Issues in Data Mining.
- Summary.

## Slide 15
### What is Data Mining?

- Data mining (knowledge discovery and data mining – KDD)
  - Extraction of interesting (non-trivial, implicit, previously unknown and potentially useful) patterns or knowledge from huge amount of data.
  - Data sources: databases, texts, web, images, videos, and etc.
- Alternative names
  - Knowledge discovery (mining) in databases (KDD), knowledge extraction, data/pattern analysis, data archeology, data dredging, information harvesting, business intelligence, etc.

Question: Is looking up “Queensland public holidays in 2026” by Google search engine a data mining problem?

## Slide 16
### Knowledge Discovery (KDD) Process

- This is a view from typical database systems and data warehousing communities.
- Data mining plays an essential role in the knowledge discovery process.

[Figure: Knowledge discovery pipeline. Databases → Data Cleaning and Data Integration → Data Warehouse → Selection → Task-relevant Data → Data Mining → Pattern Evaluation. The upper end represents discovered knowledge.]

## Slide 17
### Data Mining in Business Intelligence

[Figure: A pyramid with increasing potential to support business decisions toward its apex. The levels, from bottom to top, and the roles shown beside them are transcribed below.]

| Level (bottom to top) | Description | Role shown |
| --- | --- | --- |
| Data Sources | Paper, Files, Web documents, Scientific experiments, Database Systems | DBA |
| Data Preprocessing/Integration, Data Warehouses | | |
| Data Exploration | Statistical Summary, Querying, and Reporting | Data Analyst |
| Data Mining | Information Discovery | Data Analyst |
| Data Presentation | Visualization Techniques | Business Analyst |
| Decision Making | | End User |

## Slide 18
### Example: Medical Data Mining

- Health care & medical data mining – often adopted such a view in statistics and machine learning
  - Preprocessing of the data (including feature extraction and dimension reduction).
  - Classification or/and clustering processes.
  - Post-processing for presentation.

## Slide 19
### Introduction

- What Is Data Mining?
- What Kind of Data Can Be Mined?
- What Kind of Patterns Can Be Mined?
- What Technologies Are Used?
- What Kind of Applications Are Targeted?
- Major Issues in Data Mining.
- Summary.

## Slide 20
### Data Mining: On What Kinds of Data?

- Database-oriented data sets and applications
  - Relational database, data warehouse, transactional database.
- Advanced data sets and advanced applications
  - Data streams and sensor data.
  - Time-series data, temporal data, sequence data (incl. bio-sequences).
  - Structure data, graphs, social networks and multi-linked data.
  - Object-relational databases.
  - Heterogeneous databases and legacy databases.
  - Spatial data and spatiotemporal data.
  - Multimedia database.
  - Text databases.
  - The World-Wide Web.

## Slide 21
### Introduction

- What Is Data Mining?
- What Kind of Data Can Be Mined?
- What Kind of Patterns Can Be Mined?
- What Technologies Are Used?
- What Kind of Applications Are Targeted?
- Major Issues in Data Mining.
- Summary.

## Slide 22
### Data Mining Function (1): Concept Description: Characterization & Discrimination

- Data entries can be associated with classes or concepts.
  - E.g. concepts of customers: BigSpenders and BudgetSpenders.
  - Concept description can be useful to describe individual classes.
- Class/concept descriptions:
  - Data Characterization
    - A summarization of the general characteristics or features of a target class of data.
  - Data Discrimination
    - A comparison of the general features of the target class data objects, against the general features of objects from one or multiple contrasting classes.

## Slide 23
### Data Mining Function (2): Association and Correlation Analysis

- Frequent patterns (or frequent itemsets)
  - What items are frequently purchased together in Coles?
- Association, correlation vs. causality
  - A typical association rule
    - Nappy → Beer [0.5%, 75%] (support, confidence).
  - Are strongly associated items also strongly correlated?
- How to mine such patterns and rules efficiently in large datasets?
- How to use such patterns for classification, clustering, and other applications?

## Slide 24
### Data Mining Function (3): Classification

- Classification and label prediction
  - Construct models (functions) based on some training examples.
  - Describe and distinguish classes or concepts for future prediction.
    - E.g., classify countries based on (climate), or classify cars based on (gas mileage).
  - Predict some unknown class labels.
- Typical methods
  - Decision trees, naïve Bayesian classification, support vector machines, neural networks, rule-based classification, pattern-based classification, logistic regression, …
- Typical applications
  - Credit card fraud detection, direct marketing, classifying stars, diseases, web-pages, …

## Slide 25
### Data Mining Function (4): Cluster Analysis

- Unsupervised learning (i.e., Class label is unknown).
- Group data to form new categories (i.e., clusters), e.g., cluster houses to find distribution patterns.
- Principle: Maximizing intra-class similarity & minimizing inter-class similarity.
- Many methods and applications (k-means, hierarchy-based, spectral clustering, Fuzzy clustering, graph-based).

## Slide 26
### Data Mining Function: (5) Outlier Analysis

- Outlier analysis
  - Outlier: A data object that does not comply with the general behavior of the data.
  - Noise or exception? — One person’s garbage could be another person’s treasure.
  - Methods: the by product of clustering or regression analysis, …
  - Useful in fraud detection, rare events analysis.

## Slide 27
### (6) Time and Ordering: Sequential Pattern, Trend and Evolution Analysis

- Sequence, trend and evolution analysis
  - Trend, time-series, and deviation analysis: e.g., regression and value prediction.
  - Sequential pattern mining
    - E.g., first buy digital camera, then buy large SD memory cards.
  - Periodicity analysis.
  - Motifs and biological sequence analysis
    - Approximate and consecutive motifs.
  - Similarity-based analysis.
- Mine data streams
  - Ordered, time-varying, potentially infinite, data streams.

## Slide 28
### (7) Structure and Network Analysis

- Graph mining
  - Finding frequent subgraphs (e.g., chemical compounds), trees (XML), substructures (web fragments).
- Information network analysis
  - Social networks: actors (objects, nodes) and relationships (edges).
    - E.g., author networks in CS, terrorist networks.
  - Multiple heterogeneous networks
    - A person could be in multiple information networks: friends, family, classmates, …
  - Links carry a lot of semantic information: Link mining.
- Web mining
  - Web is a big information network: from PageRank to Google.
  - Analyse Web information networks.
    - Web community discovery, opinion mining, usage mining, …

## Slide 29
### Evaluation of Knowledge

- Q1: Are all mined knowledge interesting? (Y/N)
- Q2: What makes a pattern interesting?
- Many objective measures of pattern interestingness exist.
  - Based on the structure of discovered patterns and the statistics underlying them.
- Subjective interestingness measures:
  - Based on user beliefs in the data.
  - Patterns are interesting if the patterns are unexpected.
  - Offer strategic information on which the user can act.

## Slide 30
### Introduction

- What Is Data Mining?
- What Kind of Data Can Be Mined?
- What Kind of Patterns Can Be Mined?
- What Technologies Are Used?
- What Kind of Applications Are Targeted?
- Major Issues in Data Mining.
- Summary.

## Slide 31
### Data Mining: Confluence of Multiple Disciplines

[Figure: Data Mining is at the center of a diagram connecting the disciplines listed below.]

- Machine Learning.
- Pattern Recognition.
- Statistics.
- Visualization.
- Applications.
- Algorithm.
- High-Performance Computing.
- Database Technology.

## Slide 32
### Why Confluence of Multiple Disciplines?

- Tremendous amount of data
  - Algorithms must be highly scalable to handle such as terabytes ($10^{12}$), petabyte ($10^{15}$) of data.
- High-dimensionality of data
  - Micro-array may have tens of thousands of dimensions.
- High complexity of data
  - Data streams, sensor data, time-series data, temporal data, sequence data, …

## Slide 33
### Introduction

- What Is Data Mining?
- What Kind of Data Can Be Mined?
- What Kind of Patterns Can Be Mined?
- What Technologies Are Used?
- What Kind of Applications Are Targeted?
- Major Issues in Data Mining.
- Summary.

## Slide 34
### Applications of Data Mining

- Web page analysis: from web page classification, clustering, to PageRank & HITS algorithms.
- Collaborative analysis & recommender systems
  - E.g. “matrix (1999)” … & “aliens (1986)” → “Avengers: Infinity War (2018)”.
- Basket data analysis to targeted marketing.
- Biological and medical data analysis: classification, cluster analysis (microarray data analysis), biological sequence analysis, biological network analysis.
- Data mining and software engineering (e.g., IEEE Computer, Aug. 2009 issue).
- From major dedicated data mining systems/tools (e.g., SAS, MS SQL-Server Analysis Manager, Oracle Data Mining Tools) to invisible data mining.

## Slide 35
### Introduction

- What Is Data Mining?
- What Kind of Data Can Be Mined?
- What Kind of Patterns Can Be Mined?
- What Technologies Are Used?
- What Kind of Applications Are Targeted?
- Major Issues in Data Mining.
- Summary.

## Slide 36
### Major Issues in Data Mining (1)

- Mining Methodology
  - Mining various and new kinds of knowledge.
  - Mining knowledge in multi-dimensional space.
  - Data mining: An interdisciplinary effort.
  - Boosting the power of discovery in a networked environment.
  - Handling noise, uncertainty, and incompleteness of data.
  - Pattern evaluation and pattern- or constraint-guided mining.
- User Interaction
  - Interactive mining.
  - Incorporation of background knowledge.
  - Presentation and visualization of data mining results.

## Slide 37
### Major Issues in Data Mining (2)

- Efficiency and Scalability
  - Efficiency and scalability of data mining algorithms.
  - Parallel, distributed, stream, and incremental mining methods.
- Diversity of data types
  - Handling complex types of data.
  - Mining dynamic, networked, and global data repositories.
- Data mining and society
  - Social impacts of data mining.
  - Privacy-preserving data mining (Cyber Security related).
  - Invisible data mining.

## Slide 38
### Introduction

- What Is Data Mining?
- What Kind of Data Can Be Mined?
- What Kind of Patterns Can Be Mined?
- What Technologies Are Used?
- What Kind of Applications Are Targeted?
- Major Issues in Data Mining.
- Summary.

## Slide 39
### Summary

- Data mining: Discovering interesting patterns and knowledge from massive amount of data.
- A natural evolution of database technology, in great demand, with wide applications.
- A KDD process includes data cleaning, data integration, data selection, transformation, data mining, pattern evaluation, and knowledge presentation.
- Mining can be performed on a variety of data.
- Data mining functionalities: characterization, discrimination, association, classification, clustering, outlier and trend analysis, etc.
- Data mining technologies and applications.
- Major issues in data mining.

## Slide 40
### Key Dates

| Date | To Remember |
| --- | --- |
| Week 1 | Check all assessment/assignment due dates |
| Week 2 — Sunday, 26 July | Last day to add a course |
| Student Vacation Week — Monday, 10 August | CENSUS DATE — Last day to pay your fees or to drop a course without financial liability |
| Week 8 — Sunday, 13 September | Last day to drop a course without academic failure |

## Slide 41
### Join Griffith Coding Club

Build AI-ready developer skills and sharpen your problem-solving.

- Starts Week 2.
- Every Friday | 2:00 pm – 4:00 pm.
- 5 Week Workshops.
- What we’ll cover:
  - AI tools for software developers.
  - 5 hands-on sessions with practical demos.
  - Competitive programming for contests and coding interviews.
  - Train for ICPC and other programming competitions.
- Workshop structure:
  - Hour 1: AI tools for software developers.
  - Hour 2: Competitive programming.
- Special highlight: ICPC Preliminary at Griffith – 30 August 2026.
  - Brisbane students planning to compete are warmly welcome to join.
- All skill levels welcome.
- To join or inquire, please email:
  - Kevin: x.yin@griffith.edu.au (GC).
  - Larry: l.wen@griffith.edu.au (Nathan).

[Figure: Coding Club promotional poster with programming-themed illustrations.]

## Slide 42
### Cyber Studio Presents: An Industry Meet-up

- Tuesday 21/07/2026.
- 4pm – 6pm.
- Griffith Southbank Campus S05_2.04.
- LIMITED SPOTS AVAILABLE — REGISTER NOW.

Fortinet is a cybersecurity company providing network security, firewall, secure access, cloud protection, threat intelligence, endpoint security, zero trust solutions, intrusion prevention, VPN services, security operations, AI-driven defense, scalable platforms, enterprise protection, risk management, and comprehensive digital infrastructure security worldwide.

James Calder is Fortinet’s Practice Lead for Higher Education and an experienced cybersecurity leader. Having led major cybersecurity and digital transformation initiatives across Australia and Southeast Asia, he provides expertise in emerging threats, artificial intelligence, cyber resilience, and future cybersecurity workforce skills.

Data#3: An Australian technology solutions provider that helps organisations modernise operations through cloud, cybersecurity, data, AI, networking, and managed services. By aligning technology with business goals, it enables greater productivity, security, efficiency, and digital transformation across multiple industries.

Kerry Minon is the Talent Attraction Lead at Data#3, bringing expertise in talent acquisition, executive search, human resources, organisational development, and career coaching. She leads national talent attraction strategies for the technology sector and offers valuable insights into recruitment, personal branding, career pathways, and employer expectations for emerging talent.

[Figure: Industry meetup poster with speaker portraits, company logos, and a registration QR code. QR destination is not transcribed; small poster text was recovered with OCR.]

## Slide 43
### Have a question?
