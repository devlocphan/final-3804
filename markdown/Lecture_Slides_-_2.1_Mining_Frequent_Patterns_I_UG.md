## Slide 1
### Lecture 4: Mining Frequent Patterns I

3031ICT: Applied Data Mining  
3804ICT: Data Mining

Dr Can Wang  
School of Information and Communication Technology

## Slide 2
### Mining Frequent Patterns I

- Basic Concepts
- Frequent Itemset Mining Method – Apriori Algorithm
- Which Patterns Are Interesting?—Pattern Evaluation Methods
- Summary

## Slide 3
### What Is Frequent Pattern Analysis?

- Frequent pattern: a pattern (a set of items, subsequences, substructures, etc.) that occurs frequently in a data set
  - A set of items (itemsets)
  - A subsequence (a frequent sequential pattern)
  - A substructure can refer to different structural forms.
- Motivation: Finding inherent regularities in data
  - What products are often purchased together?—Beer and diapers?!
  - What are the subsequent purchases after buying a PC?
  - What kinds of DNA are sensitive to this new drug?
  - Can we automatically classify web documents?
- Applications
  - Basket data analysis, cross-marketing, catalog design, sale campaign analysis, Web log (click stream) analysis, and DNA sequence analysis.

## Slide 4
### A Motivating Example of Market Basket Analysis

Managers’ Question: “Which groups or sets of items are customers likely to purchase on a given trip to the store?”

- Manager can then use the results to plan marketing or advertising strategies
  - Layout 1 (close): items that are frequently purchased together can be placed in proximity to further encourage the combined sale of such items.
  - Layout 2 (far & opposite): placing hardware and software at opposite ends of the store may force customers who purchase such items to pick up other items along the way.
- Market basket analysis can also help retailers plan which items to put on sale at reduced prices.

Market Basket Analysis process analyzes customer buying habits by finding associations between the different items that customers place in their “shopping baskets”.

[Figure: Shopping Baskets diagram asks “Which items are frequently purchased together by customers?” Customer 1 has bread, milk, cereal; Customer 2 has bread, sugar, eggs; Customer 3 has bread, butter; Customer n has sugar. A Market Analyst examines the baskets. The small decorative shopping illustrations and their layout are not reproduced.]

## Slide 5
### A Motivating Example of Market Basket Analysis

Patterns can be represented in the form of association rules.

computer ⇒ antivirus_software [support = 2%, confidence = 60%].

[Figure: Shopping Baskets diagram repeats the question “Which items are frequently purchased together by customers?” Customer 1: bread, milk, cereal; Customer 2: bread, sugar, eggs; Customer 3: bread, butter; Customer n: sugar. A Market Analyst examines the baskets.]

- Support and confidence are two measures of rule interestingness.
  - A support of 2% means that 2% of all the transactions under analysis show that computer and antivirus software are purchased together.
  - A confidence of 60% means that 60% of the customers who purchased a computer also bought the software.
- Association rules are considered interesting if they satisfy both a minimum support threshold and a minimum confidence threshold.
- Thresholds can be set by users or domain experts.

## Slide 6
### Basic Concepts: Support

| TID | Items |
| --- | --- |
| 1 | Bread, Milk |
| 2 | Bread, Diaper, Beer, Eggs |
| 3 | Milk, Diaper, Beer, Coke |
| 4 | Bread, Milk, Diaper, Beer |
| 5 | Bread, Milk, Diaper, Coke |

- Itemset
  - A collection of one or more items
    - Example: {Milk, Bread, Diaper}
  - k-itemset
    - An itemset that contains k items
    - {Milk, Bread, Diaper} is a 3-itemset.
    - {Bread, Milk} is a 2-itemset.
- Support Count (Frequency, Count)
  - Occurrence frequency of an itemset
  - E.g. $\sigma(\{\text{Milk, Bread, Diaper}\})=2$. What about $\sigma(\{\text{Bread, Milk}\})=?$
- Support
  - Fraction of transactions that contain an itemset
  - E.g. $s(\{\text{Milk, Bread, Diaper}\})=2/5$.
  - $s(\{\text{Milk, Bread}\})=?$
- Frequent Itemset
  - An itemset whose support is greater than or equal to a threshold min_sup.
  - The set of frequent k-itemsets is denoted by $F_k$.

[Figure: Overlapping customer sets labeled “Customer buys diaper” and “Customer buys beer”; their intersection is labeled “Customer buys both”.]

## Slide 7
### Basic Concepts: Association Rule

| TID | Items |
| --- | --- |
| 1 | Bread, Milk |
| 2 | Bread, Diaper, Beer, Eggs |
| 3 | Milk, Diaper, Beer, Coke |
| 4 | Bread, Milk, Diaper, Beer |
| 5 | Bread, Milk, Diaper, Coke |

**Association Rule**

An implication expression of the form $X\to Y$, where X and Y are itemsets.

Example: {Milk, Diaper} → {Beer}  
Antecedent → Consequent

**Rule Evaluation Metrics**

- Support (s): Usefulness
  - Fraction of transactions that contain both X and Y
- Confidence (c): Certainty
  - Measures how often items in Y appear in transactions that contain X
  - $c=\dfrac{\sigma(X\cup Y)}{\sigma(X)}$

Example rule: {Milk, Diaper} → Beer

$$
s=\frac{\sigma(\{\text{Milk, Diaper, Beer}\})}{|T|}=\frac25=0.4
$$

$$
c=\frac{\sigma(\{\text{Milk, Diaper, Beer}\})}{\sigma(\{\text{Milk, Diaper}\})}=\frac23=0.67
$$

A support of 0.4 for the rule above ({Milk, Diaper} → Beer) means that 40% of all the transactions show that purchases of Milk and Diaper are with Beer.

A confidence of 0.67 means that 67% of the customers who purchased both Milk and Diaper also bought the Beer.

## Slide 8
### Basic Concepts: Association Rule

| TID | Items |
| --- | --- |
| 1 | Bread, Milk |
| 2 | Bread, Diaper, Beer, Eggs |
| 3 | Milk, Diaper, Beer, Coke |
| 4 | Bread, Milk, Diaper, Beer |
| 5 | Bread, Milk, Diaper, Coke |

**Association Rule**

An implication expression of the form $X\to Y$, where X and Y are itemsets.

Example: {Milk, Diaper} → {Beer}  
Antecedent → Consequent

Two thresholds (specified by users or experts):

- Min_sup: minimum support threshold
- Min_conf: minimum confidence threshold

Rules that satisfy both a minimum support threshold (min_sup) and a minimum confidence threshold (min_conf) are called strong.

$$
\operatorname{confidence}(A\Rightarrow B)=P(B\mid A)
=\frac{\operatorname{support}(A\cup B)}{\operatorname{support}(A)}
=\frac{\operatorname{support\_count}(A\cup B)}{\operatorname{support\_count}(A)}
$$

## Slide 9
### An Example Illustrates Basic Concepts

| TID | Items |
| --- | --- |
| 1 | {a, b, c} |
| 2 | {b, c, f, g} |
| 3 | {a, b, c, g, h} |
| 4 | {b, c} |
| 5 | {c, g, i} |
| 6 | {a, b, c, d, h} |
| 7 | {b, c, g, i, h} |
| 8 | {a, c, h} |
| 9 | {b, c, i} |
| 10 | {b, c, h} |

- Itemset: there are eight items. Any combination can be an itemset.
- K-itemset: consider 2-itemsets, e.g. {b,c}
- Frequency / support count / count / absolute support:
  - Count({b,c})=?
- Support / relative support:
  - support of {b,c}?
- Min_sup: 80% (0.8)
- Frequent itemset:
  - is itemset {b,c} frequent or not?
  - And itemset {a,c}?
- Association Rule: {b} → {c} and {b,c} → {h}
- Confidence: conf({b} → {c}) and conf({b,c} → {h})?
- Min_conf: 80%
- Strong Rule:
  - Rule {b} → {c} strong? Rule {b,c} → {h} strong?

## Slide 10
### Association Rule Mining Task

Thus, the general approach to mining association rules is:

1. Frequent Itemset Generation
   - Generate all itemsets that satisfies the min_sup threshold.
   - These itemsets are called frequent itemsets.
2. Rule Generation
   - Generate high confidence rules from each frequent itemset, these rules must satisfy minimum support and minimum confidence, where each rule is a binary partitioning of a frequent itemset.
   - These rules are called strong rules.

Frequent itemset generation is still computationally expensive!

## Slide 11
### Freq. Itemsets Generation is Pricy

- Step 1 often generates a huge number of itemsets satisfying the minimum support (min_sup) threshold, especially when min-sup is set low. This is because if an itemset is frequent, each of its subsets is frequent as well.
  - E.g. {a,b,c,d} is frequent, then {a}, {b}, {c}, {d}, {a,b}, …, {b,c,d} are frequent as well.
- A long itemset will contain a combinatorial number of shorter, frequent sub-itemsets.
  - A long pattern contains a combinatorial number of sub-patterns, e.g., $\{a_1,\ldots,a_{100}\}$ contains

$$
\binom{100}{1}+\binom{100}{2}+\cdots+\binom{100}{100}
=2^{100}-1\approx1.27\times10^{30}
$$

sub-patterns!

## Slide 12
### Frequent Itemset Generation

Given d items, there are $2^d$ possible candidate itemsets.

[Figure: Itemset lattice; edges connect each itemset to one-item extensions. All node labels by level are transcribed below.]

- null
- A, B, C, D, E
- AB, AC, AD, AE, BC, BD, BE, CD, CE, DE
- ABC, ABD, ABE, ACD, ACE, ADE, BCD, BCE, BDE, CDE
- ABCD, ABCE, ABDE, ACDE, BCDE
- ABCDE

## Slide 13
### Apriori Principle

Apriori Principle (Agrawal & Srikant @VLDB’94):

- If an itemset is frequent, then all of its subsets must also be frequent.
- Conversely, if an itemset is infrequent, then all of its supersets must also be infrequent.

Thus we do not have to consider all possible itemsets. We can do pruning using Apriori principle.

- For example, if {beer, milk} is infrequent, then we do not need to consider {beer, milk, diaper} or {beer, milk, coke} and so on.

## Slide 14
### Illustration of Apriori Principle

[Figure: Itemset lattice marks AB as “Found to be Infrequent”. Its “Pruned supersets” are ABC, ABD, ABE, ABCD, ABCE, ABDE, and ABCDE. Node labels are listed by level; graphical connecting edges are not reproduced.]

- null
- A, B, C, D, E
- AB, AC, AD, AE, BC, BD, BE, CD, CE, DE
- ABC, ABD, ABE, ACD, ACE, ADE, BCD, BCE, BDE, CDE
- ABCD, ABCE, ABDE, ACDE, BCDE
- ABCDE

## Slide 15
### Apriori Algorithm: Finding Freq. Itemsets by Confined Candidate Generation

$F_k$: frequent k-itemsets  
$C_k$: candidate k-itemsets

Algorithm:

- Let k=1
- Generate $F_1=\{\text{frequent 1-itemsets}\}$
- Repeat until $F_k$ is empty
  - Candidate Generation: Generate $C_{k+1}$ from $F_k$
  - Candidate Pruning: Prune candidate itemsets in $C_{k+1}$ containing subsets of length k that are infrequent
  - Support Counting: Count the support of each candidate in $C_{k+1}$ by scanning the DB
  - Candidate Elimination: Eliminate candidates in $C_{k+1}$ that are infrequent, leaving only those that are frequent in $F_{k+1}$

## Slide 16
### Apriori Algorithm Illustration

| TID | Items |
| --- | --- |
| 1 | Bread, Milk |
| 2 | Beer, Bread, Diaper, Eggs |
| 3 | Beer, Coke, Diaper, Milk |
| 4 | Beer, Bread, Diaper, Milk |
| 5 | Bread, Coke, Diaper, Milk |

Items (1-itemsets): $C_1$ (candidate 1-itemsets)

| Item | Count |
| --- | --- |
| Bread | 4 |
| Coke | 2 |
| Milk | 4 |
| Beer | 3 |
| Diaper | 4 |
| Eggs | 1 |

Minimum Support Count = 3 or 3/5 (Support)

## Slide 17
### Apriori Algorithm Illustration

Items (1-itemsets): $C_1$ (candidate 1-itemsets)

| Item | Count |
| --- | --- |
| Bread | 4 |
| Coke | 2 |
| Milk | 4 |
| Beer | 3 |
| Diaper | 4 |
| Eggs | 1 |

Items (1-itemsets): $F_1$ (frequent 1-itemsets)

| Item | Count |
| --- | --- |
| Bread | 4 |
| Milk | 4 |
| Beer | 3 |
| Diaper | 4 |

[Figure: Coke (2) and Eggs (1) are crossed out in the displayed table to leave the frequent 1-itemsets.]

Minimum Support Count = 3

## Slide 18
### Apriori Algorithm Illustration

Items (1-itemsets)

| Item | Count |
| --- | --- |
| Bread | 4 |
| Coke | 2 |
| Milk | 4 |
| Beer | 3 |
| Diaper | 4 |
| Eggs | 1 |

Pairs (2-itemsets) using joining. No need to generate candidates involving Coke or Eggs.

Items (2-itemsets): Candidate 2-itemsets

| Itemset |
| --- |
| {Bread, Milk} |
| {Bread, Beer} |
| {Bread, Diaper} |
| {Beer, Milk} |
| {Diaper, Milk} |
| {Beer, Diaper} |

Minimum Support Count = 3

## Slide 19
### Apriori Algorithm Illustration

Items (2-itemsets): Candidate 2-itemsets

| Itemset |
| --- |
| {Bread, Milk} |
| {Bread, Beer} |
| {Bread, Diaper} |
| {Beer, Milk} |
| {Diaper, Milk} |
| {Beer, Diaper} |

Items (2-itemsets): Frequent 2-itemsets

| Itemset | Count |
| --- | --- |
| {Bread, Milk} | 3 |
| {Beer, Bread} | 2 |
| {Bread, Diaper} | 3 |
| {Beer, Milk} | 2 |
| {Diaper, Milk} | 3 |
| {Beer, Diaper} | 3 |

[Figure: The rows {Beer, Bread} and {Beer, Milk}, each with count 2, are crossed out; the other four rows are frequent.]

Minimum Support Count = 3

## Slide 20
### Apriori Algorithm Illustration

Items (2-itemsets): Frequent 2-itemsets

| Itemset | Count |
| --- | --- |
| {Bread, Milk} | 3 |
| {Beer, Bread} | 2 |
| {Bread, Diaper} | 3 |
| {Beer, Milk} | 2 |
| {Diaper, Milk} | 3 |
| {Beer, Diaper} | 3 |

Joining → Items (3-itemsets): Candidate 3-itemsets

| Itemset |
| --- |
| {Beer, Diaper, Milk} |
| {Beer, Bread, Diaper} |
| {Bread, Diaper, Milk} |
| {Beer, Bread, Milk} |

[Figure: The two infrequent pairs remain crossed out; a joining arrow leads to four candidate triples.]

## Slide 21
### Apriori Algorithm Illustration

Items (3-itemsets): Candidate 3-itemsets

| Itemset |
| --- |
| {Beer, Diaper, Milk} |
| {Beer, Bread, Diaper} |
| {Bread, Diaper, Milk} |
| {Beer, Bread, Milk} |

Pruning → Items (3-itemsets): Three 3-itemsets are removed & pruned.

| Itemset | Count |
| --- | --- |
| {Beer, Diaper, Milk} | 2 |
| {Beer, Bread, Diaper} | 2 |
| {Bread, Diaper, Milk} | 2 |
| {Beer, Bread, Milk} | 1 |

| Itemset | Count |
| --- | --- |
| {Bread, Milk} | 3 |
| {Beer, Bread} | 2 |
| {Bread, Diaper} | 3 |
| {Beer, Milk} | 2 |
| {Diaper, Milk} | 3 |
| {Beer, Diaper} | 3 |

[Figure: Infrequent pairs {Beer, Bread} and {Beer, Milk} trigger pruning of {Beer, Diaper, Milk}, {Beer, Bread, Diaper}, and {Beer, Bread, Milk}; {Bread, Diaper, Milk} remains for support counting. Cross-outs and arrows show these dependencies.]

## Slide 22
### Apriori Algorithm Illustration

Items (One Candidate 3-itemsets Left after Pruning)

| Itemset | Count |
| --- | --- |
| {Beer, Diaper, Milk} | 2 |
| {Beer, Bread, Diaper} | 2 |
| {Bread, Diaper, Milk} | 2 |
| {Beer, Bread, Milk} | 1 |

[Figure: The three previously pruned triples are crossed out. The remaining candidate {Bread, Diaper, Milk} has count 2, below the threshold.]

NO Freq. 3-itemsets  
Apriori Stops

Minimum Support Count = 3

## Slide 23
### Apriori Algorithm Illustration

- If we use Brute-force method, how many matchings?

  $$\binom61+\binom62+\binom63=6+15+20=41$$

- How many matchings with pruning in this Apriori algorithm example?
  - $6+6+1=13$
- How many matchings without pruning in this Apriori algorithm example? (the worst case)
  - $6+6+4=16$

## Slide 24
### Generating Association Rules from Freq. Itemsets

- Once the frequent itemsets from transactions in a database D have been found, it is straightforward to generate strong association rules from them (satisfy both minimum support and minimum confidence).

$$
\operatorname{confidence}(A\to B)=P(B\mid A)
=\frac{\operatorname{support\_count}(A\cup B)}{\operatorname{support\_count}(A)}
$$

- The conditional probability is expressed in terms of itemset support count, where $\operatorname{support\_count}(A\cup B)$ is the number of transactions containing the itemsets $A\cup B$, and $\operatorname{support\_count}(A)$ is the number of transactions containing the itemset A.

## Slide 25
### Generating Association Rules from Freq. Itemsets

- Based on this equation, association rules can be generated as follows:
  - For each frequent itemset I, generate all nonempty subsets of I.
  - For every nonempty subset s of I, output the rule “$s\to(I-s)$” if

    $$\frac{\operatorname{support\_count}(I)}{\operatorname{support\_count}(s)}\ge\text{min\_conf},$$

    where min_conf is the minimum confidence threshold.

Example: If {A,B,C,D} is a frequent itemset, candidate rules:

- ABC → D, ABD → C, ACD → B, BCD → A
- AB → CD, AC → BD, AD → BC, BC → AD, BD → AC, CD → AB
- A → BCD, B → ACD, C → ABD, D → ABC

Note: If $|I|=k$, then there are $2^k-2$ candidate association rules (without considering $I\to\varnothing$ and $\varnothing\to I$).

## Slide 26
### Generating Association Rules from Freq. Itemsets

- If we have a frequent itemset $X=\{I_1,I_2,I_5\}$. What are the association rules that can be generated from X?
- The nonempty subsets of X are $\{I_1,I_2\}$, $\{I_1,I_5\}$, $\{I_2,I_5\}$, $\{I_1\}$, $\{I_2\}$, and $\{I_5\}$.
- The resulting association rules can be as follows:

| Rule | Confidence |
| --- | --- |
| $\{I_1,I_2\}\to\{I_5\}$ ($X-\{I_1,I_2\}$) | 2/4 = 0.5 or 50% |
| $\{I_1,I_5\}\to\{I_2\}$ | 2/2 = 100% |
| $\{I_2,I_5\}\to\{I_1\}$ | 2/2 = 100% |
| $\{I_1\}\to\{I_2,I_5\}$ | 2/6 = 33% |
| $\{I_2\}\to\{I_1,I_5\}$ | 2/7 = 29% |
| $\{I_5\}\to\{I_1,I_2\}$ | 2/2 = 100% |

If the minimum confidence is set to 70%, which rules are output as strong rules?

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

## Slide 27
### Rule Generation

Confidence of rules generated from the same itemset has an anti-monotone property.

- E.g., Suppose {A,B,C,D} is a frequent 4-itemset:

  $$c(ABC\to D)\ge c(AB\to CD)\ge c(A\to BCD)$$

- Confidence is anti-monotone w.r.t. number of items on the RHS of the rule.

## Slide 28
### Rule Generation for Apriori Algorithm

Lattice of rules:

- ABCD → {}
- BCD → A, ACD → B, ABD → C, ABC → D
- BC → AD, BD → AC, CD → AB, AD → BC, AC → BD, AB → CD
- D → ABC, C → ABD, B → ACD, A → BCD

[Figure: The rule lattice is overlaid with confidence-based pruning. BCD → A is the “Low Confidence Rule”. The shaded “Pruned Rules” are BC → AD, BD → AC, CD → AB, D → ABC, C → ABD, and B → ACD. Enlarging the consequent cannot increase confidence. All rule labels are transcribed above; graphical edges are not reproduced.]

## Slide 29
### Mining Frequent Patterns I

- Basic Concepts
- Frequent Itemset Mining Methods
- Which Patterns Are Interesting?—Pattern Evaluation Methods
- Summary

## Slide 30
### Limitation of Thresholds

- A support–confidence framework (Most association rule mining algorithms).
  - Minimum support and confidence thresholds help weed out or exclude the exploration of a good number of uninteresting rules.
  - Many of the rules generated are still not interesting to the users. Especially true when mining at low support thresholds, or mining for long patterns.
- This has been a major bottleneck for successful application of association rule mining.

“How can we tell which strong association rules are really interesting?”

## Slide 31
### A misleading “strong” association rule

- In an electronic device retailer data set, 10,000 transactions are analyzed, the data show that 6000 of the customer transactions included computer games, while 7500 included videos, and 4000 included both computer games and videos.
- Suppose minimum support = 30% and minimum confidence = 60%. The following association rule is discovered:

  Rule: Buys(X, “computer games”) → buys(X, “videos”)  
  [support = 40%, confidence = 66%]

- It IS a strong rule, but this rule is misleading because the probability of purchasing videos is 75%, which is even larger than 66%.

## Slide 32
### From Association Analysis to Correlation Analysis

A correlation measure can be used to augment the support–confidence framework for association rules.

Assumption: The occurrence of itemset A is independent of the occurrence of itemset B, if $P(A\cup B)=P(A)P(B)$. Otherwise, itemsets A and B are dependent and correlated events.

Lift is a simple correlation measure that is given as follows.

$$
\operatorname{lift}(A,B)=\frac{P(A\cup B)}{P(A)P(B)}
=\frac{\operatorname{conf}(A\to B)}{\operatorname{sup}(B)}
$$

- If the lift is less than 1, A is negatively correlated with B.
- If the lift value is greater than 1, A and B are positively correlated.
- If the lift value is equal to 1, A and B are independent and there is no correlation between them.

## Slide 33
### Correlation Analysis Using Lift

In an electronic device retailer data set, 10,000 transactions are analyzed, the data show that 6000 of the customer transactions included computer games, while 7500 included videos, and 4000 included both computer games and videos.

- According to the lift equation:

  $$\operatorname{lift}(A,B)=\frac{P(A\cup B)}{P(A)P(B)}=\frac{\operatorname{conf}(A\to B)}{\operatorname{sup}(B)}$$

- The corresponding $\operatorname{lift}(\text{game},\text{video})=\dfrac{P(\{\text{game, video}\})}{P(\{\text{game}\})P(\{\text{video}\})}=\dfrac{0.4}{0.6\times0.75}=0.89<1$.
- Thus, even the rule is strong according to the min_sup & min_conf, it is still not an interesting rule for decision making.

## Slide 34
### Summary

- Basic concepts:
  - Itemset & k-itemset
  - Support count/frequency
  - Frequent itemset
  - association rules, support-confident framework
  - Strong rule
- Apriori (Candidate generation & test)
  - Frequent Itemsets Generation
  - Rule Generation
- Which patterns are interesting?
  - Lift

## Slide 35
### Have a question?
