## Slide 1
### World-Wide-Web Mining

3031ICT: Applied Data Mining  
3804ICT: Data Mining  
Lecture 10  
Dr Can Wang (Gold Coast)  
School of Information and Communication Technology

## Slide 2
### World-Wide-Web Mining

- Web Usage Mining
  - Types of Data
  - Web Usage Data Pre-Processing
  - Web Usage Mining: Modelling
- Recommender Systems and Collaborative Filtering
  - Collaborative Filtering
  - Finding “Similar” Users
  - Rating Predictions
  - Item-Item Collaborative Filtering
  - Item-Item vs. User-User
  - Pros/Cons of Collaborative Filtering

## Slide 3
### Web Usage Mining: Background

- A large amount of clickstream, transaction data, and user profile data are collected by Web-based organizations (e-commerce) in their daily operations.
- Analyzing such data can help these organizations:
  - Determine the life-time value of clients.
  - Design cross-marketing strategies across products and services.
  - Evaluate the effectiveness of promotional campaigns.
  - Optimize the functionality of Web-based applications.
  - Provide more personalized content to visitors.
  - And find the most effective logical structure for their Web space.

This type of analysis involves the automatic discovery of meaningful patterns and relationships from a large collection of primarily semi-structured data, often stored in Web and applications server access logs, as well as in related operational data sources.

## Slide 4
### Web Usage Mining

- Web usage mining refers to the automatic discovery and analysis of patterns in clickstreams, user transactions and other associated data collected or generated, as a result of user interactions with Web resources on one or more Web sites.
- The goal is to capture, model, and analyze the behavioral patterns and profiles of users interacting with a Web site.
- The discovered patterns are usually represented as collections of pages, objects, or resources that are frequently accessed or used by groups of users with common needs or interests.

## Slide 5
### Web Usage Mining

The overall Web usage mining process can be divided into three inter-dependent stages:

- Data collection and pre-processing
  - The clickstream data is cleaned and partitioned into a set of user transactions representing the activities of each user during different visits to the site.
  - Other sources of knowledge such as the site content or structure, as well as semantic domain knowledge from site ontologies (such as product catalogs or concept hierarchies), may also be used in pre-processing, or to enhance user transaction data.
- Pattern discovery
  - Statistical, database, and machine learning operations are performed to obtain hidden patterns reflecting the typical behavior of users, as well as summary statistics on Web resources, sessions, and users.
- Pattern analysis
  - The discovered patterns and statistics are further processed, filtered, possibly resulting in aggregate user models that can be used as input to applications, such as recommendation engines, visualization tools, and Web analytics and report generation tools.

## Slide 6
### Web Usage Mining

[Figure: Process architecture divided into “Data Preparation Phase” and “Pattern Discovery Phase.” Inputs “Web & Application Server Logs,” “Site Content & Structure” and “Domain Knowledge” feed “Data Preprocessing,” comprising Data Cleaning, Pageview Identification, Sessionization, Data Integration and Data Transformation. The resulting “User Transaction Database” feeds “Usage Mining”: Transaction Clustering, Pageview Clustering, Correlation Analysis, Association Rule Mining and Sequential Pattern Mining. Discovered “Patterns” feed “Pattern Analysis,” comprising Pattern Filtering, Aggregation and Characterization, producing “Aggregate User models.” Arrows connect these stages and show supporting knowledge flowing into preparation and discovery.]

## Slide 7
### Web Usage Mining

- An important task in any data mining application is the creation of a suitable target data set to which data mining and statistical algorithms can be applied.
- This is particularly important in Web usage mining due to the characteristics of clickstream data and its relationship to other related data collected from multiple sources and across multiple channels.
- The process may involve pre-processing the original data, integrating data from multiple sources, and transforming the integrated data into a form suitable for input into specific data mining operations.

## Slide 8
### Web Usage Data Pre-Processing

**Data Fusion and Cleaning**

- Data fusion refers to the merging of log files from several Web and application servers.
- Data cleaning is usually site-specific, and involves tasks such as, removing extraneous references to embedded objects that may not be important for the purpose of analysis, including references to style files, graphics, or sound files.

## Slide 9
### Web Usage Data Pre-Processing

**Pageview Identification**

- Each pageview can be viewed as a collection of Web objects or resources representing a specific “user event”.
- Identification of pageviews is heavily dependent on the intra-page structure of the site, as well as on the page contents and the underlying site domain knowledge.
- It may be desirable to consider pageviews at a higher level of aggregation.

## Slide 10
### Web Usage Data Pre-Processing

**User Identification**

- The analysis of Web usage does not require knowledge about a user’s identity.
- However, it is necessary to distinguish among different users.
- Since a user may visit a site more than once, the server logs record multiple sessions for each user.
- IP addresses, alone, are not generally sufficient for mapping log entries onto the set of unique visitors.
- A combination of IP addresses and other information, such as user agents and referrers.

## Slide 11
### Web Usage Data Pre-Processing

Same IP, but different Agent.

A combination of IP addresses and other information such as user agents and referrers.

**Access log**

| Time | IP | URL | Ref | Agent |
| --- | --- | --- | --- | --- |
| 0:01 | 1.2.3.4 | A | − | IE5;Win2k |
| 0:09 | 1.2.3.4 | B | A | IE5;Win2k |
| 0:10 | 2.3.4.5 | C | − | IE6;WinxP;SP1 |
| 0:12 | 2.3.4.5 | B | C | IE6;WinxP;SP1 |
| 0:15 | 2.3.4.5 | E | C | IE6;WinxP;SP1 |
| 0:19 | 1.2.3.4 | C | A | IE5;Win2k |
| 0:22 | 2.3.4.5 | D | B | IE6;WinxP;SP1 |
| 0:22 | 1.2.3.4 | A | − | IE6;WinxP;SP2 |
| 0:25 | 1.2.3.4 | E | C | IE5;Win2k |
| 0:25 | 1.2.3.4 | C | A | IE6;WinxP;SP2 |
| 0:33 | 1.2.3.4 | B | C | IE6;WinxP;SP2 |
| 0:58 | 1.2.3.4 | D | B | IE6;WinxP;SP2 |
| 1:10 | 1.2.3.4 | E | D | IE6;WinxP;SP2 |
| 1:15 | 1.2.3.4 | A | − | IE5;Win2k |
| 1:16 | 1.2.3.4 | C | A | IE5;Win2k |
| 1:17 | 1.2.3.4 | F | C | IE6;WinxP;SP2 |
| 1:26 | 1.2.3.4 | F | C | IE5;Win2k |
| 1:30 | 1.2.3.4 | B | A | IE5;Win2k |
| 1:36 | 1.2.3.4 | D | B | IE5;Win2k |

**User 1**

| Time | IP | URL | Ref |
| --- | --- | --- | --- |
| 0:01 | 1.2.3.4 | A | − |
| 0:09 | 1.2.3.4 | B | A |
| 0:19 | 1.2.3.4 | C | A |
| 0:25 | 1.2.3.4 | E | C |
| 1:15 | 1.2.3.4 | A | − |
| 1:26 | 1.2.3.4 | F | C |
| 1:30 | 1.2.3.4 | B | A |
| 1:36 | 1.2.3.4 | D | B |

**User 2**

| Time | IP | URL | Ref |
| --- | --- | --- | --- |
| 0:10 | 2.3.4.5 | C | − |
| 0:12 | 2.3.4.5 | B | C |
| 0:15 | 2.3.4.5 | E | C |
| 0:22 | 2.3.4.5 | D | B |

**User 3**

| Time | IP | URL | Ref |
| --- | --- | --- | --- |
| 0:22 | 1.2.3.4 | A | − |
| 0:25 | 1.2.3.4 | C | A |
| 0:33 | 1.2.3.4 | B | C |
| 0:58 | 1.2.3.4 | D | B |
| 1:10 | 1.2.3.4 | E | D |
| 1:17 | 1.2.3.4 | F | C |

[Figure: Arrows partition the access log into User 1, User 2 and User 3 using IP and agent. Small shaded/overlaid portions of the original log are difficult to read after OCR; the displayed user partitions omit the 1:16 row present in the original log.]

## Slide 12
### Web Usage Data Pre-Processing

**Sessionization**

- Sessionization is the process of segmenting the user activity record of each user into sessions, each representing a single visit to the site.
- The goal of a sessionization heuristic is to reconstruct, the actual sequence of actions performed by one user during one visit to the site, from the clickstream data.
- Sessionization heuristics fall into two basic categories:
  - Time-oriented: apply either global or local time-out estimates to distinguish between consecutive sessions.
  - Structure-oriented: use either the static site structure or the implicit linkage structure captured in the referrer fields of the server logs.

## Slide 13
### Web Usage Data Pre-Processing

**User 1**

| Time | IP | URL | Ref | Assigned session |
| --- | --- | --- | --- | --- |
| 0:01 | 1.2.3.4 | A | − | Session 1 |
| 0:09 | 1.2.3.4 | B | A | Session 1 |
| 0:19 | 1.2.3.4 | C | A | Session 1 |
| 0:25 | 1.2.3.4 | E | C | Session 1 |
| 1:15 | 1.2.3.4 | A | − | Session 2 |
| 1:26 | 1.2.3.4 | F | C | Session 2 |
| 1:30 | 1.2.3.4 | B | A | Session 2 |
| 1:36 | 1.2.3.4 | D | B | Session 2 |

[Figure: The User 1 log is split into two tables labelled Session 1 and Session 2. The added assignment column above represents those two tables.]

- **h1:** Total session duration may not exceed a threshold \(\theta\). Given \(t_0\), the timestamp for the first request in a constructed session \(S\), the request with a timestamp \(t\) is assigned to \(S\), iff
  \[
  t-t_0\le\theta.
  \]
- **h2:** Total time spent on a page may not exceed a threshold \(\delta\). Given \(t_1\), the timestamp for request assigned to constructed session \(S\), the next request with timestamp \(t_2\) is assigned to \(S\), iff
  \[
  t_2-t_1\le\delta.
  \]
- Example above: \(\theta=30\) mins.
- If we apply h2 with \(\delta=10\) mins, there are three sessions for User 1: A → B → C → E, A, and F → B → D.

## Slide 14
### Web Usage Data Pre-Processing

**Path Completion**

- Another potentially important pre-processing task which is usually performed after sessionization is path completion.
- Client- or proxy-side caching can often result in missing access references to those pages or objects that have been cached.
- Missing references due to caching can be heuristically inferred through path completion, which relies on the knowledge of site structure and the referrer information from server logs.

## Slide 15
### Web Usage Data Pre-Processing

User’s actual navigation path:

A → B → D → E → D → B → C

What the server log shows:

| URL | Referrer |
| --- | --- |
| A | −− |
| B | A |
| D | B |
| E | D |
| C | B |

Path Completion is needed, because of caching.

[Figure: A site-structure/navigation diagram with nodes A, B, C, D, E and F contrasts the actual path with server-log observations. Revisits to D and B are absent from the log because of caching. Fine arrow styles in the diagram are not represented.]

## Slide 16
### Web Usage Data Pre-Processing

**Data Integration**

- In order to provide the most effective framework for pattern discovery, data from a variety of other sources must be integrated with the preprocessed clickstream data.
- For example, in e-commerce applications:
  - User data.
  - Product attributes and categories from operational databases.
  - Shopping cart changes.
  - Order and shipping information.
  - Impressions.
  - Click-throughs.

## Slide 17
### Web Usage Mining: Modelling

- Data Modelling for Web Usage Mining

**Sessions / users × Pageviews**

| | A | B | C | D | E | F |
| --- | --- | --- | --- | --- | --- | --- |
| user0 | 15 | 5 | 0 | 0 | 0 | 185 |
| user1 | 0 | 0 | 32 | 4 | 0 | 0 |
| user2 | 12 | 0 | 0 | 56 | 236 | 0 |
| user3 | 9 | 47 | 0 | 0 | 0 | 134 |
| user4 | 0 | 0 | 23 | 15 | 0 | 0 |
| user5 | 17 | 0 | 0 | 157 | 69 | 0 |
| user6 | 24 | 89 | 0 | 0 | 0 | 354 |
| user7 | 0 | 0 | 78 | 27 | 0 | 0 |
| user8 | 7 | 0 | 45 | 20 | 127 | 0 |
| user9 | 0 | 38 | 57 | 0 | 0 | 15 |

**User-pageview matrix \(Y\)**

| | A.html | B.html | C.html | D.html | E.html |
| --- | --- | --- | --- | --- | --- |
| user1 | 1 | 0 | 1 | 0 | 1 |
| user2 | 1 | 1 | 0 | 0 | 1 |
| user3 | 0 | 1 | 1 | 1 | 0 |
| user4 | 1 | 0 | 1 | 1 | 1 |
| user5 | 1 | 1 | 0 | 0 | 1 |
| user6 | 1 | 0 | 1 | 1 | 1 |

**Term-pageview matrix \(Z\)**

| | A.html | B.html | C.html | D.html | E.html |
| --- | --- | --- | --- | --- | --- |
| web | 0 | 0 | 1 | 1 | 1 |
| data | 0 | 1 | 1 | 1 | 0 |
| mining | 0 | 1 | 1 | 1 | 0 |
| business | 1 | 1 | 0 | 0 | 0 |
| intelligence | 1 | 1 | 0 | 0 | 1 |
| marketing | 1 | 1 | 0 | 0 | 1 |
| ecommerce | 0 | 1 | 1 | 0 | 0 |
| search | 1 | 0 | 1 | 0 | 0 |
| information | 1 | 0 | 1 | 1 | 1 |
| retrieval | 1 | 0 | 1 | 1 | 1 |

**Content-enhanced transaction matrix \(X=Y*Z^T\)**

| | web | data | mining | business | intelligence | marketing | ecommerce | search | information | retrieval |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| user1 | 2 | 1 | 1 | 1 | 2 | 2 | 1 | 2 | 3 | 3 |
| user2 | 1 | 1 | 1 | 2 | 3 | 3 | 1 | 1 | 2 | 2 |
| user3 | 2 | 3 | 3 | 1 | 1 | 1 | 2 | 1 | 2 | 2 |
| user4 | 3 | 2 | 2 | 1 | 2 | 2 | 1 | 2 | 4 | 4 |
| user5 | 1 | 1 | 1 | 2 | 3 | 3 | 1 | 1 | 2 | 2 |
| user6 | 3 | 2 | 2 | 1 | 2 | 2 | 1 | 2 | 4 | 4 |

[Figure: A numeric session–pageview example is accompanied by the user–pageview, term–pageview and content-enhanced transaction matrices, illustrating \(X=YZ^T\).]

## Slide 18
### World-Wide-Web Mining

- Web Usage Mining
  - Types of Data
  - Web Usage Data Pre-Processing
  - Web Usage Mining: Modelling
- Recommender Systems and Collaborative Filtering
  - Collaborative Filtering
  - Finding “Similar” Users
  - Rating Predictions
  - Item-Item Collaborative Filtering
  - Item-Item vs. User-User
  - Pros/Cons of Collaborative Filtering

## Slide 19
### Recommender Systems and Collaborative Filtering

- Recommender systems are widely used on the Web for recommending products and services to users. Most e-commerce Web sites have such systems.
- Two important functions:
  - Help users deal with the information overload by giving them personalized recommendations.
  - Help businesses make more profits.
- Example: Movie recommendation based on users’ preferences and historical records.

## Slide 20
### Collaborative Filtering

- Consider user \(x\).
- Find set \(N\) of other users whose ratings are “similar” to \(x\)’s ratings.
- Estimate \(x\)’s ratings based on ratings of users in \(N\).

[Figure: User \(x\) and neighborhood \(N\) illustrate collaborative filtering. The illustrated process is labelled “show Mr. A’s preference to the system,” “database search,” and “get recommendation”; other labels include “similar,” “recommended items,” “search” and “database.” Preferences are compared with database users to identify similar users and recommend items. Some small decorative labels remain unclear after OCR.]

## Slide 21
### Finding “Similar” Users

Blank cells denote missing ratings.

| User | HP1 | HP2 | HP3 | TW | SW1 | SW2 | SW3 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A | 4 | | | 5 | 1 | | |
| B | 5 | 5 | 4 | | | | |
| C | | | | 2 | 4 | 5 | |
| D | | 3 | | | | | 3 |

- Consider Users A and B with ratings above.
- We need a similarity metric \(\operatorname{sim}(A,B)\).
- Capture intuition that \(\operatorname{sim}(A,B)>\operatorname{sim}(A,C)\).

## Slide 22
### Option 1: Jaccard Similarity

| User | HP1 | HP2 | HP3 | TW | SW1 | SW2 | SW3 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A | 4 | | | 5 | 1 | | |
| B | 5 | 5 | 4 | | | | |
| C | | | | 2 | 4 | 5 | |
| D | | 3 | | | | | 3 |

- \(\operatorname{Sim}(A,B)=\dfrac{|r_A\cap r_B|}{|r_A\cup r_B|}\).

  \[
  r_A=\{4,0,0,5,1,0,0\},\quad
  r_B=\{5,5,4,0,0,0,0\},\quad
  r_C=\{0,0,0,2,4,5,0\}.
  \]

- \(\operatorname{Sim}(A,B)=1/5;\ \operatorname{sim}(A,C)=2/4\).
- \(\operatorname{Sim}(A,B)<\operatorname{Sim}(A,C)\).
- Problem: Ignores the value of the rating.

## Slide 23
### Option 2: Cosine Similarity

| User | HP1 | HP2 | HP3 | TW | SW1 | SW2 | SW3 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A | 4 | | | 5 | 1 | | |
| B | 5 | 5 | 4 | | | | |
| C | | | | 2 | 4 | 5 | |
| D | | 3 | | | | | 3 |

- \[
  \operatorname{Sim}(A,B)=\cos(A,B)
  =\frac{\operatorname{dot}(r_A,r_B)}{\|r_A\|\|r_B\|}.
  \]

  \[
  r_A=\{4,0,0,5,1,0,0\},\quad
  r_B=\{5,5,4,0,0,0,0\},\quad
  r_C=\{0,0,0,2,4,5,0\}.
  \]

- \(\operatorname{Sim}(A,B)=0.38;\ \operatorname{sim}(A,C)=0.32\).
- \(\operatorname{Sim}(A,B)>\operatorname{Sim}(A,C)\), but not by much.

## Slide 24
### Option 3: Centered Cosine Similarity

- Normalize ratings by subtracting row mean.

| User | HP1 | HP2 | HP3 | TW | SW1 | SW2 | SW3 | Row mean |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A | 4 | | | 5 | 1 | | | 10/3 |
| B | 5 | 5 | 4 | | | | | 14/3 |
| C | | | | 2 | 4 | 5 | | 11/3 |
| D | | 3 | | | | | 3 | 6/2 = 3 |

- \[
  \operatorname{Sim}(A,B)=\cos(A,B)
  =\frac{\operatorname{dot}(r_A,r_B)}{\|A\|\|B\|}.
  \]
- \(\operatorname{Sim}(A,B)=0.09;\ \operatorname{sim}(A,C)=-0.56\).
- \(\operatorname{Sim}(A,B)>\operatorname{Sim}(A,C)\).

  \[
  r_A=\{2/3,0,0,5/3,-7/3,0,0\},
  \]
  \[
  r_B=\{1/3,1/3,-2/3,0,0,0,0\},
  \]
  \[
  r_C=\{0,0,0,-5/3,1/3,4/3,0\}.
  \]

- Missing ratings treated as “average”.
- Also known as Pearson Correlation.

## Slide 25
### Rating Predictions: User-User

From similarity metric to recommendations:

- Let \(r_x\) be the vector of user \(x\)’s ratings.
- Let \(N\) be the set of \(k\) users most similar to \(x\) who have rated item \(i\).
- Prediction for item \(i\) of user \(x\):
  - Option 1:
    \[
    r_{xi}=\frac{1}{k}\sum_{y\in N}r_{yi}\qquad(k\text{-NN}).
    \]
  - Option 2:
    \[
    r_{xi}=\frac{\sum_{y\in N}s_{xy}\cdot r_{yi}}
                 {\sum_{y\in N}s_{xy}}.
    \]

Shorthand: \(s_{xy}=\operatorname{sim}(x,y)\).

## Slide 26
### Item-Item Collaborative Filtering

- So far: User-user collaborative filtering.
- Another view: Item-item.
  - For item \(i\), find other similar items (items in neighborhood).
  - Estimate rating for item \(i\) based on ratings for similar items.
  - Use the same similarity metrics and prediction functions as in user-user model.

\[
r_{xi}=
\frac{\sum_{j\in N(i;x)}s_{ij}\cdot r_{xj}}
     {\sum_{j\in N(i;x)}s_{ij}}.
\]

- \(s_{ij}\): similarity of items \(i\) and \(j\).
- \(r_{xj}\): rating of user \(u\) on item \(j\) (the slide uses \(u\) in this description).
- \(N(i;x)\): set of items rated by \(x\) similar to \(i\).

## Slide 27
### Item-Item CF (\(|N|=2\))

Columns are users; rows are movies. Blank cells indicate unknown ratings; values are ratings between 1 and 5.

| Movie \ User | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | | 3 | | | 5 | | | 5 | | 4 | |
| 2 | | | 5 | 4 | | | 4 | | | 2 | 1 | 3 |
| 3 | 2 | 4 | | 1 | 2 | | 3 | | 4 | 3 | 5 | |
| 4 | | 2 | 4 | | 5 | | | 4 | | | 2 | |
| 5 | | | 4 | 3 | 4 | 2 | | | | | 2 | 5 |
| 6 | 1 | | 3 | | 3 | | | 2 | | | 4 | |

## Slide 28
### Item-Item CF (\(|N|=2\))

Estimate rating of movie 1 by user 5.

| Movie \ User | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | | 3 | | ? | 5 | | | 5 | | 4 | |
| 2 | | | 5 | 4 | | | 4 | | | 2 | 1 | 3 |
| 3 | 2 | 4 | | 1 | 2 | | 3 | | 4 | 3 | 5 | |
| 4 | | 2 | 4 | | 5 | | | 4 | | | 2 | |
| 5 | | | 4 | 3 | 4 | 2 | | | | | 2 | 5 |
| 6 | 1 | | 3 | | 3 | | | 2 | | | 4 | |

[Figure: The unknown cell for movie 1, user 5 is highlighted with a question mark.]

## Slide 29
### Item-Item CF (\(|N|=2\))

| Movie \ User | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | sim(1,m) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | | 3 | | ? | 5 | | | 5 | | 4 | | 1.00 |
| 2 | | | 5 | 4 | | | 4 | | | 2 | 1 | 3 | −0.18 |
| 3 | 2 | 4 | | 1 | 2 | | 3 | | 4 | 3 | 5 | | 0.41 |
| 4 | | 2 | 4 | | 5 | | | 4 | | | 2 | | −0.10 |
| 5 | | | 4 | 3 | 4 | 2 | | | | | 2 | 5 | −0.31 |
| 6 | 1 | | 3 | | 3 | | | 2 | | | 4 | | 0.59 |

**Neighbor selection:** Identify movies similar to movie 1, rated by user 5.

Here we use Pearson correlation as similarity:

1. Subtract mean rating \(m_i\) from each movie \(i\).
   \[
   m_1=(1+3+5+5+4)/5=3.6.
   \]
   Row 1: `[-2.6, 0, -0.6, 0, 0, 1.4, 0, 0, 1.4, 0, 0.4, 0]`.
2. Compute cosine similarities between rows.

[Figure: Neighbor selection highlights movies 3 and 6 and their ratings by user 5.]

## Slide 30
### Item-Item CF (\(|N|=2\))

| Movie \ User | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | sim(1,m) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | | 3 | | ? | 5 | | | 5 | | 4 | | 1.00 |
| 2 | | | 5 | 4 | | | 4 | | | 2 | 1 | 3 | −0.18 |
| 3 | 2 | 4 | | 1 | 2 | | 3 | | 4 | 3 | 5 | | 0.41 |
| 4 | | 2 | 4 | | 5 | | | 4 | | | 2 | | −0.10 |
| 5 | | | 4 | 3 | 4 | 2 | | | | | 2 | 5 | −0.31 |
| 6 | 1 | | 3 | | 3 | | | 2 | | | 4 | | 0.59 |

Compute similarity weights:

\[
s_{1,3}=0.41,\qquad s_{1,6}=0.59.
\]

[Figure: The chosen neighborhood contains movies 3 and 6.]

## Slide 31
### Item-Item CF (\(|N|=2\))

| Movie \ User | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | | 3 | | 2.6 | 5 | | | 5 | | 4 | |
| 2 | | | 5 | 4 | | | 4 | | | 2 | 1 | 3 |
| 3 | 2 | 4 | | 1 | 2 | | 3 | | 4 | 3 | 5 | |
| 4 | | 2 | 4 | | 5 | | | 4 | | | 2 | |
| 5 | | | 4 | 3 | 4 | 2 | | | | | 2 | 5 |
| 6 | 1 | | 3 | | 3 | | | 2 | | | 4 | |

Predict by taking weighted average:

\[
r_{ix}=
\frac{\sum_{j\in N(i;x)}s_{ij}\cdot r_{jx}}
     {\sum_{j\in N(i;x)}s_{ij}}.
\]

\[
r_{1,5}=\frac{0.41*2+0.59*3}{0.41+0.59}=2.6.
\]

[Figure: The formerly unknown rating at movie 1, user 5 is now filled with 2.6.]

## Slide 32
### Item-Item vs. User-User

- In theory, user-user and item-item are dual approaches.
- In practice, item-item outperforms user-user in many use cases.
- Why? Items are simpler, users have multiple tastes.
  - Items belong to a small set of “genres”, but users have varied tastes.
  - Item Similarity is more meaningful than User Similarity.

**References**

Yehuda Koren, Robert Bell, Chris Volinsky. Matrix Factorization Techniques for Recommender Systems. *IEEE Computer* 42 (8), pp. 30–37, 2009.

## Slide 33
### Pros/Cons of Collaborative Filtering

- **+ Works for any kind of item**
  - No feature selection needed.
- **− Cold Start**
  - Need enough users in the system to find a match.
- **− Sparsity**
  - The user/ratings matrix is sparse.
  - Hard to find users that have rated the same items.
- **− First rater**
  - Cannot recommend an item that has not been previously rated.
  - New items, Esoteric items.
- **− Popularity bias**
  - Cannot recommend items to someone with unique taste.
  - Tends to recommend popular items.

## Slide 34
### Summary

- Web Usage Mining
  - Types of Data
  - Web Usage Data Pre-Processing
  - Web Usage Mining: Modelling
- Recommender Systems and Collaborative Filtering
  - Collaborative Filtering
  - Finding “Similar” Users
  - Rating Predictions
  - Item-Item Collaborative Filtering
  - Item-Item vs. User-User
  - Pros/Cons of Collaborative Filtering

## Slide 35
### Have a question?

[Figure: Closing-slide question illustration.]
