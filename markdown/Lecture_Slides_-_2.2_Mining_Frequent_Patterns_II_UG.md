## Slide 1
### Lecture 5: Mining Frequent Patterns II

3804ICT: Data Mining  
3031ICT: Applied Data Mining

Dr Can Wang  
School of Information and Communication Technology

## Slide 2
### Mining Frequent Patterns II

- FP-Growth: A Frequent Pattern-Growth Approach
- Multi-level Association Rules Mining
- Multi-dimensional Association Rules Mining

## Slide 3
### Bottlenecks of Apriori Approach

- Bottlenecks of the Apriori approach
  - Need to generate candidate (k+1)-itemsets after counting the support to find out frequent k-itemsets. This candidate generation could be very EXPENSIVE.
    - E.g. $10^4$ frequent 1-itemsets → over $10^7$ candidate 2-itemsets.
  - Repeatedly scanning the transaction database for support counting dramatically slows down the Apriori algorithm.

## Slide 4
### Pattern-Growth Approach: Mining Frequent Patterns Without Candidate Generation

- Bottlenecks of the Apriori approach
  - Breadth-first (i.e., level-wise) search
  - Candidate generation and test
    - Often generates a huge number of candidates
- The FP-Growth Approach (J. Han, J. Pei, and Y. Yin, SIGMOD’00)
  - Depth-first search
  - Avoid explicit candidate generation

## Slide 5
### FP-growth: Frequent Pattern-Growth

- Adopts a divide and conquer strategy
- Compresses the database to represent frequent items into a frequent–pattern tree or FP-tree
  - Retains the itemset association information
  - Each node is represented by an item and its support count
  - Each branch is a k-itemset (or an association) with support count
- Once the FP-tree is constructed, mine the frequent itemsets from the FP-tree
  - Divide the FP-tree into different parts and perform the mining over the parts
- Divides the compressed database into a set of conditional databases, each associated with one frequent item
- Mines each such database separately

[Figure: Example node/branch sketches labeled I4:2, I4:2, and I3:1 illustrate item identifiers and support counts.]

## Slide 6
### Example: FP-growth

- The first scan of data is the same as Apriori
- Derive the set of frequent 1-itemsets
- Let min-sup-count = 2
- Generate a set of ordered items

Transactional Database:

| TID | List of item IDs |
| --- | --- |
| T100 | I1, I2, I5 |
| T200 | I2, I4 |
| T300 | I2, I3 |
| T400 | I1, I2, I4 |
| T500 | I1, I3 |
| T600 | I2, I3 |
| T700 | I1, I3 |
| T800 | I1, I2, I3, I5 |
| T900 | I1, I2, I3 |

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

## Slide 7
### Construct the FP-Tree

Transactional Database:

| TID | Items |
| --- | --- |
| T100 | I1, I2, I5 |
| T200 | I2, I4 |
| T300 | I2, I3 |
| T400 | I1, I2, I4 |
| T500 | I1, I3 |
| T600 | I2, I3 |
| T700 | I1, I3 |
| T800 | I1, I2, I3, I5 |
| T900 | I1, I2, I3 |

- Create a branch for each transaction
  - Items in each transaction are processed in order

1. Order the items T100: {I2, I1, I5}
2. Construct the first branch: ⟨I2:1⟩, ⟨I1:1⟩, ⟨I5:1⟩

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: FP-tree after T100. Parent–child relationships are represented by the nested list.]

- null
  - I2:1
    - I1:1
      - I5:1

## Slide 8
### Construct the FP-Tree

Transactional Database:

| TID | Items |
| --- | --- |
| T100 | I1, I2, I5 |
| T200 | I2, I4 |
| T300 | I2, I3 |
| T400 | I1, I2, I4 |
| T500 | I1, I3 |
| T600 | I2, I3 |
| T700 | I1, I3 |
| T800 | I1, I2, I3, I5 |
| T900 | I1, I2, I3 |

- Create a branch for each transaction
  - Items in each transaction are processed in order

1. Order the items T200: {I2, I4}
2. Construct the second branch: ⟨I2:1⟩, ⟨I4:1⟩

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: T200 shares the I2 prefix, changing I2:1 to I2:2 and adding I4:1.]

- null
  - I2:2
    - I1:1
      - I5:1
    - I4:1

## Slide 9
### Construct the FP-Tree

Transactional Database:

| TID | Items |
| --- | --- |
| T100 | I1, I2, I5 |
| T200 | I2, I4 |
| T300 | I2, I3 |
| T400 | I1, I2, I4 |
| T500 | I1, I3 |
| T600 | I2, I3 |
| T700 | I1, I3 |
| T800 | I1, I2, I3, I5 |
| T900 | I1, I2, I3 |

- Create a branch for each transaction
  - Items in each transaction are processed in order

1. Order the items T300: {I2, I3}
2. Construct the third branch: ⟨I2:2⟩, ⟨I3:1⟩

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: I2:2 changes to I2:3; I3:1 is added below I2.]

- null
  - I2:3
    - I1:1
      - I5:1
    - I4:1
    - I3:1

## Slide 10
### Construct the FP-Tree

Transactional Database:

| TID | Items |
| --- | --- |
| T100 | I1, I2, I5 |
| T200 | I2, I4 |
| T300 | I2, I3 |
| T400 | I1, I2, I4 |
| T500 | I1, I3 |
| T600 | I2, I3 |
| T700 | I1, I3 |
| T800 | I1, I2, I3, I5 |
| T900 | I1, I2, I3 |

- Create a branch for each transaction
  - Items in each transaction are processed in order

1. Order the items T400: {I2, I1, I4}
2. Construct the fourth branch: ⟨I2:3⟩, ⟨I1:1⟩, ⟨I4:1⟩

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: I2:3 changes to I2:4 and its I1:1 child changes to I1:2; a new I4:1 child is added under that I1.]

- null
  - I2:4
    - I1:2
      - I5:1
      - I4:1
    - I4:1
    - I3:1

## Slide 11
### Construct the FP-Tree

Transactional Database:

| TID | Items |
| --- | --- |
| T100 | I1, I2, I5 |
| T200 | I2, I4 |
| T300 | I2, I3 |
| T400 | I1, I2, I4 |
| T500 | I1, I3 |
| T600 | I2, I3 |
| T700 | I1, I3 |
| T800 | I1, I2, I3, I5 |
| T900 | I1, I2, I3 |

- Create a branch for each transaction
  - Items in each transaction are processed in order

1. Order the items T500: {I1, I3}
2. Construct the fifth branch: ⟨I1:1⟩, ⟨I3:1⟩

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: A new branch I1:1 → I3:1 starts directly at null.]

- null
  - I2:4
    - I1:2
      - I5:1
      - I4:1
    - I4:1
    - I3:1
  - I1:1
    - I3:1

## Slide 12
### Construct the FP-Tree

Transactional Database:

| TID | Items |
| --- | --- |
| T100 | I1, I2, I5 |
| T200 | I2, I4 |
| T300 | I2, I3 |
| T400 | I1, I2, I4 |
| T500 | I1, I3 |
| T600 | I2, I3 |
| T700 | I1, I3 |
| T800 | I1, I2, I3, I5 |
| T900 | I1, I2, I3 |

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

When a branch of a transaction is added, the count for each node along a common prefix is increased by 1.

[Figure: Completed FP-tree after all nine transactions; nested items preserve branches and counts.]

- null
  - I2:7
    - I1:4
      - I5:1
      - I4:1
      - I3:2
        - I5:1
    - I4:1
    - I3:2
  - I1:2
    - I3:2

## Slide 13
### Construct the FP-Tree

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: Completed FP-tree, with header links connecting occurrences of each item; the graphical link routing is not reproduced.]

- null
  - I2:7
    - I1:4
      - I5:1
      - I4:1
      - I3:2
        - I5:1
    - I4:1
    - I3:2
  - I1:2
    - I3:2

The problem of mining frequent patterns in databases is transformed to that of mining the FP-tree.

## Slide 14
### Mining FP-Tree for Frequent Patterns

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: Full FP-tree, with the I5 occurrences highlighted. Graphical header links and highlighting are represented by the branch list and prefix-path explanation.]

- null
  - I2:7
    - I1:4
      - I5:1
      - I4:1
      - I3:2
        - I5:1
    - I4:1
    - I3:2
  - I1:2
    - I3:2

- Occurrences of I5: ⟨I2, I1, I5⟩ and ⟨I2, I1, I3, I5⟩
  - Two prefix Paths ⟨I2, I1:1⟩ and ⟨I2, I1, I3:1⟩
  - Conditional FP tree contains only ⟨I2:2, I1:2⟩, I3 is not considered because its support count of 1 is less than the minimum support count.
  - Frequent patterns {I2, I5:2}, {I1, I5:2}, {I2, I1, I5:2}

[Figure: Conditional FP tree: null → I2:2 → I1:2; I3:1 is shown as the removed, infrequent continuation.]

## Slide 15
### Mining FP-Tree for Frequent Patterns

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: Full FP-tree, highlighting I4 occurrences.]

- null
  - I2:7
    - I1:4
      - I5:1
      - I4:1
      - I3:2
        - I5:1
    - I4:1
    - I3:2
  - I1:2
    - I3:2

- Occurrences of I4: ⟨I2, I1, I4⟩ and ⟨I2, I4⟩
  - Two prefix Paths ⟨I2, I1:1⟩ and ⟨I2:1⟩
  - Conditional FP tree contains only ⟨I2:2⟩, I1 is not considered because its support count of 1 is less than the minimum support count.
  - Frequent patterns {I2, I4:2}

[Figure: Conditional FP tree: null → I2:2; the I1:1 continuation is removed.]

## Slide 16
### Mining FP-Tree for Frequent Patterns

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: Full FP-tree, highlighting I3 occurrences.]

- null
  - I2:7
    - I1:4
      - I5:1
      - I4:1
      - I3:2
        - I5:1
    - I4:1
    - I3:2
  - I1:2
    - I3:2

- Occurrences of I3: ⟨I2, I1, I3⟩, ⟨I2, I3⟩, and ⟨I1, I3⟩
  - Three prefix Paths ⟨I2, I1:2⟩, ⟨I2:2⟩, and ⟨I1:2⟩
  - Frequent patterns {I2, I3:4}, {I1, I3:4}, {I2, I1, I3:2}

Conditional FP tree:

- null
  - I2:4 (2+2)
    - I1:2
  - I1:2

## Slide 17
### Mining FP-Tree for Frequent Patterns

| Item ID | Support count |
| --- | --- |
| I2 | 7 |
| I1 | 6 |
| I3 | 6 |
| I4 | 2 |
| I5 | 2 |

[Figure: Full FP-tree, highlighting I1 occurrences.]

- null
  - I2:7
    - I1:4
      - I5:1
      - I4:1
      - I3:2
        - I5:1
    - I4:1
    - I3:2
  - I1:2
    - I3:2

- Occurrences of I1: ⟨I2, I1⟩
  - One prefix Path ⟨I2:4⟩
  - Conditional FP tree contains only ⟨I2:4⟩, I1 is not considered because there is only one item I2 as a prefix.
  - Frequent patterns {I2, I1:4}

[Figure: Conditional FP tree: null → I2:4.]

## Slide 18
### Summary of FP-Growth

| TID | Conditional FP-tree | Frequent Patterns Generated |
| --- | --- | --- |
| I5 | ⟨I2:2, I1:2⟩ | {I2,I5:2}, {I1,I5:2}, {I2,I1,I5:2} |
| I4 | ⟨I2:2⟩ | {I2,I4:2} |
| I3 | ⟨I2:4, I1:2⟩, ⟨I1:2⟩ | {I2,I3:4}, {I1,I3:4}, {I2,I1,I3:2} |
| I1 | ⟨I2:4⟩ | {I2,I1:4} |

- FP-growth transforms the problem of finding long frequent patterns to searching for shorter ones recursively and concatenating the suffix.
- It uses the least frequent suffix offering a good selectivity.
- It reduces the search cost.
- If the tree does not fit into main memory, partition the database into a set of projected databases to mine FP-tree there.
- Efficient and scalable for mining both long and short frequent patterns.

## Slide 19
### Mining Frequent Patterns II

- FP-Growth: A Frequent Pattern-Growth Approach
- Multi-level Association Rules Mining
- Multi-dimensional Association Rules Mining

## Slide 20
### Mining Multi-level Associations

- Strong associations discovered at high abstraction levels, though with high support, could be common sense knowledge.
- Finding novel patterns at more detailed levels (like Drill-down) could be interesting.
- Mining patterns at higher levels (like Drill-up) can avoid too many scattered patterns at low or primitive abstraction levels.
- Therefore, it is important to develop effective methods for mining patterns at multiple abstraction levels (Drill-up and Drill-down).

## Slide 21
### Mining Multi-level Associations

Task-relevant set of transactional data — **Task-Relevant Data, D**:

| TID | Items Purchased |
| --- | --- |
| T100 | Apple 17” MacBook Pro Notebook, HP Photosmart Pro b9180 |
| T200 | Microsoft Office Professional 2010, Microsoft Wireless Optical Mouse 5000 |
| T300 | Logitech VX Nano Cordless Laser Mouse, Fellowes GEL Wrist Rest |
| T400 | Dell Studio XPS 16 Notebook, Canon PowerShot SD1400 |
| T500 | Lenovo ThinkPad X200 Tablet PC, Symantec Norton Antivirus 2010 |

[Figure: Concept hierarchy for AllElectronics computer items. The diagram spans Level 0, Level 1, Level 2, Level 3, and “Lowest level”, branching from general categories to brands and individual products. Raster labels were OCR-checked; tiny product-level leaves and some connecting lines are not legible enough to reproduce exactly.]

- Level 0: all
- Level 1:
  - Computer
  - Software
  - Printer and Camera
  - Computer Accessory
- Level 2 labels:
  - Laptop, Desktop
  - Office, Antivirus
  - Printer, Digital Camera
  - Wrist Pad, Mouse
- Level 3 visible labels:
  - Dell, Microsoft, HP, Canon, Fellowes, Logitech
- Lowest level: individual products represented by branching leaves.

## Slide 22
### Mining Multi-level Associations

- Association rules generated from mining data at multiple abstraction levels are called multiple-level or multi-level association rules. Multi-level association rules can be mined efficiently using concept hierarchies under a support-confidence framework.
- In general, a top-down strategy is employed, where counts are accumulated for the calculation of frequent itemsets at each concept level, starting at concept level 1 and working downward in the hierarchy toward the more specific concept levels, until no more frequent itemsets can be found.

## Slide 23
### Mining Multi-level Associations

- Using uniform minimum support for all levels (referred to as uniform support)
  - The same minimum support threshold is used when mining at each abstraction level.
  - For example, a minimum support threshold of 5% is ONLY used throughout (e.g., for mining from “computer” downward to “laptop computer”).
  - Both “computer” and “laptop computer” are found to be frequent, whereas “desktop computer” is not.
  - Setting minimum support threshold is very crucial, as too high or too low will have different results at low/high abstraction levels.

[Figure: Multilevel mining with uniform support. Computer at Level 1 branches to laptop computer and desktop computer at Level 2.]

| Level | min_sup | Item | Support |
| --- | --- | --- | --- |
| 1 | 5% | computer | 10% |
| 2 | 5% | laptop computer | 6% |
| 2 | 5% | desktop computer | 4% |

## Slide 24
### Mining Multi-level Associations

- Each abstraction level has its own minimum support threshold
  - The deeper the abstraction level, the smaller the corresponding threshold. For example, the minimum support thresholds for levels 1 and 2 are 5% and 3%, respectively. In this way, “computer,” “laptop computer,” and “desktop computer” are all considered frequent.

[Figure: Multilevel mining with reduced support. Computer at Level 1 branches to laptop computer and desktop computer at Level 2.]

| Level | min_sup | Item | Support |
| --- | --- | --- | --- |
| 1 | 5% | computer | 10% |
| 2 | 3% | laptop computer | 6% |
| 2 | 3% | desktop computer | 4% |

## Slide 25
### Mining Multi-level Associations

- Flexible min-support thresholds: Some items are more valuable but less frequent
  - Use non-uniform, group-based min-support
  - E.g., {diamond, watch, camera}: 0.05%; {bread, milk}: 5%; …
- Redundancy Filtering: Some rules may be redundant due to “ancestor” relationships between items
  - milk → wheat bread [support = 8%, confidence = 70%] (one year)
  - milk → wheat bread [support = 2%, confidence = 72%] (one quarter)
  - The first rule is an ancestor of the second rule ($2\%=8\%\times\frac14$).
  - A rule is redundant if its support is close to the “expected” value, based on the rule’s ancestor.

## Slide 26
### Mining Frequent Patterns II

- FP-Growth: A Frequent Pattern-Growth Approach
- Multi-level Association Rules Mining
- Multi-dimensional Association Rules Mining

## Slide 27
### Mining Multi-dimensional Associations

- So far, we have studied association rules that imply a single predicate, that is, the predicate buys. For instance, in mining our AllElectronics database, we may discover the Boolean association rule

  $$\operatorname{buys}(X,\text{“digital camera”})\Rightarrow\operatorname{buys}(X,\text{“HP printer”}).$$

- We can refer to this rule as a single dimensional or intradimensional association rule, because it contains a single distinct predicate (e.g., buys) with multiple occurrences (i.e., the predicate occurs more than once within the rule).

## Slide 28
### Mining Multi-dimensional Associations

- Instead of considering transactional data only, sales and related information are often linked with relational data or integrated into a data warehouse. Such data stores are multidimensional in nature.
- Considering each database attribute or warehouse dimension as a predicate, we can mine association rules containing multiple predicates:

  $$\operatorname{age}(X,\text{“20…29”})\land\operatorname{occupation}(X,\text{“student”})\Rightarrow\operatorname{buys}(X,\text{“laptop”}).$$

- Association rules that involve two or more dimensions or predicates can be referred to as multidimensional association rules.

## Slide 29
### Mining Multi-dimensional Associations

- We can also mine multidimensional association rules with repeated predicates, which contain multiple occurrences of some predicates. These rules are called hybrid-dimensional association rules. An example of such a rule is the following, where the predicate buys is repeated:

  $$\operatorname{age}(X,\text{“20…29”})\land\operatorname{buys}(X,\text{“laptop”})\Rightarrow\operatorname{buys}(X,\text{“HP printer”}).$$

## Slide 30
### Mining Multi-Dimensional Associations

- Single-dimensional rules:
  - buys(X, “milk”) ⇒ buys(X, “bread”)
- Multi-dimensional rules: ≥ 2 dimensions or predicates
  - Inter-dimension assoc. rules (no repeated predicates)
    - age(X, “19-25”) ∧ occupation(X, “student”) ⇒ buys(X, “coke”)
  - hybrid-dimension assoc. rules (repeated predicates)
    - age(X, “19-25”) ∧ buys(X, “popcorn”) ⇒ buys(X, “coke”)
- Categorical Attributes: finite number of possible values, no ordering among values—data cube approach
- Quantitative Attributes: Numeric, implicit ordering among values—discretization and clustering approaches

## Slide 31
### Mining Frequent Patterns II

- FP-Growth: A Frequent Pattern-Growth Approach
- Multi-level Association Rules Mining
- Multi-dimensional Association Rules Mining

## Slide 32
### Have a question?
