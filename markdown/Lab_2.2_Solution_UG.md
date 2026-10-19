# Lab 2.2 Solution

Source: [Lab 2.2 Solution_UG.pdf](../Lab%202.2%20Solution_UG.pdf)

## Page 1

### 2. Given the following transaction data set, please answer the questions below

A database has five transactions. Let min_sup=60%, min_sup=60%, and min_conf=80%.

| TID | Items |
| --- | --- |
| T100 | {M,O,N,K,E,Y} |
| T200 | {D,O,N,K,E,Y} |
| T300 | {M,A,K,E} |
| T400 | {M,U,C,K,Y} |
| T500 | {C,O,O,K,I,E} |

1. Find all frequent itemsets using Apriori and FP-growth, respectively. Compare the efficiency of the two mining processes. (24 mins)
2. List all of the strong association rules, satisfying the minimum support and confidence thresholds. (6 min)

### Answer (a): Apriori and FP-growth

Find all frequent itemsets using Apriori and FP-growth, respectively. Compare the efficiency of the two mining processes.

#### Apriori

The tables below transcribe the embedded worked example. Lowercase item labels follow the figure.

| C1 item | Count |
| --- | --- |
| m | 3 |
| o | 3 |
| n | 2 |
| k | 5 |
| e | 4 |
| y | 3 |
| d | 1 |
| a | 1 |
| u | 1 |
| c | 2 |
| i | 1 |

| L1 item | Count |
| --- | --- |
| m | 3 |
| o | 3 |
| k | 5 |
| e | 4 |
| y | 3 |

| C2 itemset | Count |
| --- | --- |
| mo | 1 |
| mk | 3 |
| me | 2 |
| my | 2 |
| ok | 3 |
| oe | 3 |
| oy | 2 |
| ke | 4 |
| ky | 3 |
| ey | 2 |

| L2 itemset | Count |
| --- | --- |
| mk | 3 |
| ok | 3 |
| oe | 3 |
| ke | 4 |
| ky | 3 |

| C3 itemset | Count | Marking in source |
| --- | --- | --- |
| oke | 3 | Retained |
| key | 2 | Crossed out |

| L3 itemset | Count |
| --- | --- |
| oke | 3 |

#### FP-growth

[Figure: FP-tree with Root → K:5. K has children E:4 and M:1. E has children M:2 and O:2. The E→M branch continues O:1→Y:1; the E→O branch continues Y:1. The K→M branch continues Y:1.]

## Page 2

### FP-Tree Table

| Item | Conditional pattern base | Conditional tree | Frequent pattern |
| --- | --- | --- | --- |
| y | {{k,e,m,o:1}, {k,e,o:1}, {k,m:1}} | k:3 | {k,y:3} |
| o | {{k,e,m:1}, {k,e:2}} | k:3,e:3 | {k,o:3}, {e,o:3}, {k,e,o:3} |
| m | {{k,e:2}, {k:1}} | k:3 | {k,m:3} |
| e | {{k:4}} | k:4 | {k,e:4} |

**Efficiency comparison:** Apriori has to do multiple scans of the database while FP-growth builds the FP-Tree with a single scan. Candidate generation in Apriori is expensive (owing to the self-join), while FP-growth does not generate any candidates.

> Transcription note: “single scan” is the source's wording; it has not been silently corrected.

### Answer (b): Strong association rules

List all of the strong association rules (with support s and confidence c) matching the following metarule, where X is a variable representing customers, and item_i denotes variables representing items (e.g., “A”, “B”, etc.).

Binary partitioning, check confidence:

`∀X ∈ transaction, buys(X,item_1) ∧ buys(X,item_2) ⇒ buys(X,item_3) [s,c]`

| Rule | [Support, confidence] |
| --- | --- |
| k,o → e | [0.6, 1] |
| e,o → k | [0.6, 1] |
