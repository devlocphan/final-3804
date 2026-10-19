# Lab 2.1 Solution

Source: [Lab 2.1 Solution_UG.pdf](../Lab%202.1%20Solution_UG.pdf)

## Page 1

### Solutions to Q2

1. **How many items in the dataset?** There are 5 items `{a, b, c, e, f}`.
2. **How many itemsets can be generated?** There are `2^5 - 1 = 31` possible itemsets.
3. **Please calculate the frequency count of 2-itemset {c,e}.** The frequent count of `{c,e}` is 3.
4. **Is itemset {b,c} frequent or not?** Yes, because `support({b,c}) = 3/5 = 0.6 > 0.4`.
5. **What is the confidence of the association rule: {b} → {c}?** `confidence({b}->{c}) = count{b,c}/count{b} = 3/3 = 1`.
6. **If min_conf=40%, is the rule {b} → {c} strong?** Yes, because `confidence({b}->{c}) = 1 > 0.4` and `support({b,c}) = 3/5 = 0.6 > 0.4` (two conditions are satisfied).

### Solutions to Q3

If there are 10 items, how many possible itemsets could be checked? The number of possible itemsets is `2^10 - 1 = 1023`.

### Solutions to Q4

| TID | Items in Transaction |
| --- | --- |
| 1 | Bread, eggs, milk |
| 2 | Juice, milk |
| 3 | Butter, juice |
| 4 | Bread, eggs, milk |
| 5 | Coffee, eggs |
| 6 | Coffee |
| 7 | Coffee, juice |
| 8 | Bread, cookies, eggs, milk |
| 9 | Butter, cookies |
| 10 | Bread, milk |

There are two steps to mine association rules:

1. Find frequent k-itemsets (support is no less than `minsup=0.2`).
2. Based on frequent k-itemsets found by 1, generate high confidence rules (confidence is no less than `min_conf=0.8`).

## Page 2

### Solution to Frequent Itemsets

1. Set k=1, 2, 3, and find `CI_1, 2, 3` (candidate 1, 2, 3-itemsets). Note that the total number of transactions is 10.

| CI_1 | Support |
| --- | --- |
| {Bread} | 4/10=0.4 |
| {Butter} | 2/10=0.2 |
| {Coffee} | 3/10=0.3 |
| {Cookies} | 2/10=0.2 |
| {Eggs} | 4/10=0.4 |
| {Juice} | 3/10=0.3 |
| {Milk} | 5/10=0.5 |

`FI_1`: {Bread}, {Butter}, {Coffee}, {Cookies}, {Eggs}, {Juice}, {Milk}.

| CI_2 | Support |
| --- | --- |
| {Bread, butter} | 0/10=0 |
| {Bread, coffee} | 0/10=0 |
| {Bread, cookies} | 1/10=0.1 |
| {Bread, eggs} | 3/10=0.3 |
| {Bread, juice} | 0/10=0 |
| {Bread, milk} | 4/10=0.4 |
| {Butter, coffee} | 0/10=0 |
| {Butter, cookies} | 1/10=0.1 |
| {Butter, eggs} | 0/10=0 |
| {Butter, juice} | 1/10=0.1 |
| {Butter, milk} | 0/10=0 |
| {Coffee, cookies} | 0/10=0 |
| {Coffee, eggs} | 1/10=0.1 |
| {Coffee, juice} | 1/10=0.1 |
| {Coffee, milk} | 0/10=0 |
| {Cookies, eggs} | 1/10=0.1 |
| {Cookies, juice} | 0/10=0 |
| {Cookies, milk} | 1/10=0.1 |
| {Eggs, juice} | 0/10=0 |
| {Eggs, milk} | 3/10=0.3 |
| {Juice, milk} | 1/10=0.1 |

`FI_2` continues on page 3.

## Page 3

### Solution to Frequent Itemsets (continued)

`FI_2`: {Bread, eggs}, {Bread, milk}, {Eggs, milk}.

| CI_3 | Support |
| --- | --- |
| {Bread, eggs, milk} | 3/10=0.3 |

`FI_3`: {Bread, eggs, milk}.

2. Based on `FI_3`, we need to find all candidate 4-itemsets. However, we cannot make 4-itemsets based on `FI_3` (only one 3-itemset and three items). In other words, `CI_4` is empty. Thus, algorithm stops.

   **Note that algorithm also stops when Frequent k-itemsets are empty.** (For example, we assume that the support of {Bread, butter, eggs} is less than min_sup (0.2), then we cannot find out Frequent 3-itemset. `FI_3` will be empty, which also stops algorithm.)

3. In all, we have found all frequent k-itemsets (support ≥0.2):
   - `FI_1`: {Bread}, {Butter}, {Coffee}, {Cookies}, {Eggs}, {Juice}, {Milk}.
   - `FI_2`: {Bread, eggs}, {Bread, milk}, {Eggs, milk}.
   - `FI_3`: {Bread, eggs, milk}.

### Solution to Strong Association Rules

To find out mining rules with high confidence, we shall start the rule generation from k=2 since we cannot find out any association rule when k=1. For example, {Bread} is a frequent 1-itemset, we cannot generate any meaningful association rule using only one item. So we start from k=2:

`FI_2`: {Bread, eggs}, {Bread, milk}, {Eggs, milk}.

All possible rule combinations of `FI_2` and corresponding confidence values are as follows. Note: `SC()` is support count operation.

| Rules | Confidence |
| --- | --- |
| {Bread} → {Eggs} | sc(bread, eggs)/sc(bread) = 3/4 = 0.75 |
| {Eggs} → {Bread} | sc(eggs, bread)/sc(eggs) = 3/4 = 0.75 |
| {Bread} → {Milk} | sc(bread, milk)/sc(bread) = 4/4 = 1.00 |
| {Milk} → {Bread} | sc(milk, bread)/sc(milk) = 4/5 = 0.8 |
| {Eggs} → {Milk} | sc(eggs, milk)/sc(eggs) = 3/4 = 0.75 |
| {Milk} → {Eggs} | sc(milk, eggs)/sc(milk) = 3/5 = 0.6 |

## Page 4

### Strong Association Rules (continued)

Since `min_conf=0.8`, we keep {Bread} → {Milk} and {Milk} → {Bread} when k=2.

`FI_3`: {Bread, eggs, milk}.

All possible rule combinations of `FI_3` and corresponding confidence values are as follows:

| Rules | Confidence |
| --- | --- |
| {Bread} → {Eggs, Milk} | sc(bread, eggs, milk)/sc(bread) = 3/4 = 0.75 |
| {Eggs} → {Bread, Milk} | sc(bread, eggs, milk)/sc(eggs) = 3/4 = 0.75 |
| {Milk} → {Bread, Eggs} | sc(bread, eggs, milk)/sc(milk) = 3/5 = 0.60 |
| {Bread, Eggs} → {Milk} | sc(bread, eggs, milk)/sc(bread, eggs) = 3/3 = 1.00 |
| {Bread, Milk} → {Eggs} | sc(bread, eggs, milk)/sc(bread, milk) = 3/4 = 0.75 |
| {Eggs, Milk} → {Bread} | sc(bread, eggs, milk)/sc(eggs, milk) = 3/3 = 1.00 |

Since `min_conf=0.8`, we keep {Bread, Eggs} → {Milk} and {Eggs, Milk} → {Bread} when k=3.

In all, the strong rules (support ≥minsup (0.2) and confidence ≥minconf (0.8)) are as follows:

- {Bread} → {Milk}.
- {Milk} → {Bread}.
- {Bread, Eggs} → {Milk}.
- {Eggs, Milk} → {Bread}.
