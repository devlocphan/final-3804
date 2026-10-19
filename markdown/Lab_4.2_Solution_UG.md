# Lab 4.2 Solution

Source: [Lab 4.2 Solution_UG.pdf](../Lab%204.2%20Solution_UG.pdf)

## Page 1

### 1. Seasonal index and deseasonalized data

Given the sales data of each quarter in three years, please calculate the seasonal index in the table and the corresponding deseasonalized data.

**Solution:**

| Quarter | Actual | Seasonal Index | Deseasonalized Data |
| --- | --- | --- | --- |
| 2015Q1 | 154 | 1.075044 | 141.6 |
| 2015Q2 | 126 | 0.879581 | 141.4 |
| 2015Q3 | 108 | 0.753927 | 145.5 |
| 2015Q4 | 185 | 1.291449 | 144.6 |
| 2016Q1 | 158 | 1.110721 | 145.3 |
| 2016Q2 | 137 | 0.963093 | 153.7 |
| 2016Q3 | 105 | 0.738137 | 141.5 |
| 2016Q4 | 169 | 1.188049 | 132.1 |
| 2017Q1 | 145 | 1.076067 | 133.4 |
| 2017Q2 | 112 | 0.831169 | 125.7 |
| 2017Q3 | 99 | 0.734694 | 133.4 |
| 2017Q4 | 183 | 1.358071 | 143.1 |

**What is the sum of the seasonal indices and the average of the seasonal indices, respectively?**

Solution: The sum of the seasonal indices is “the number of seasons”, while the average of the seasonal indices is always 1.

**What would the seasonal indices for Q2 2016 and Q3 2016 be if they are the same?**

Solution: 1.3.

> Transcription note: this answer is retained as printed, despite its apparent inconsistency with the table.

### 2. Given the sequence data below, calculate the support of 1-sequences

The sequence table continues on page 2.

## Page 2

### Sequence data

| ID | Sequences |
| --- | --- |
| Seq 1 | `{a,b}{c}{f}{g}{e}` |
| Seq 2 | `{a,d}{c}{b}{a,b,e,f}` |
| Seq 3 | `{a}{b}{f}{e}` |
| Seq 4 | `{b}{f,g}` |

**Solution:**

| 1-Sequence | Support Count |
| --- | --- |
| {a} | 3 |
| {b} | 4 |
| {c} | 2 |
| {d} | 1 |
| {e} | 3 |
| {f} | 4 |
| {g} | 2 |

Given min_support = 50% (minimum support count=2), find out all frequent 1-sequential patterns. Based on the frequent 1-sequential patterns, how many candidate 2-sequences can be generated? Please write down all candidate 2-sequences.

**Solution:** Given min_support_count=2, then {d} is infrequent. The remaining frequent 1-sequences can generate 51 candidate 2-sequences and they are as follows:

| First item / second item | a | b | c | e | f | g |
| --- | --- | --- | --- | --- | --- | --- |
| a | `<{a}{a}>` | `<{a}{b}>`, `<{ab}>` | `<{a}{c}>`, `<{ac}>` | `<{a}{e}>`, `<{ae}>` | `<{a}{f}>`, `<{af}>` | `<{a}{g}>`, `<{ag}>` |
| b | `<{b}{a}>` | `<{b}{b}>` | `<{b}{c}>`, `<{bc}>` | `<{b}{e}>`, `<{be}>` | `<{b}{f}>`, `<{bf}>` | `<{b}{g}>`, `<{bg}>` |
| c | `<{c}{a}>` | `<{c}{b}>` | `<{c}{c}>` | `<{c}{e}>`, `<{ce}>` | `<{c}{f}>`, `<{cf}>` | `<{c}{g}>`, `<{cg}>` |
| e | `<{e}{a}>` | `<{e}{b}>` | `<{e}{c}>` | `<{e}{e}>` | `<{e}{f}>`, `<{ef}>` | `<{e}{g}>`, `<{eg}>` |
| f | `<{f}{a}>` | `<{f}{b}>` | `<{f}{c}>` | `<{f}{e}>` | `<{f}{f}>` | `<{f}{g}>`, `<{fg}>` |

The final row is on page 3.

## Page 3

### Candidate 2-sequences (continued)

| First item / second item | a | b | c | e | f | g |
| --- | --- | --- | --- | --- | --- | --- |
| g | `<{g}{a}>` | `<{g}{b}>` | `<{g}{c}>` | `<{g}{e}>` | `<{g}{f}>` | `<{g}{g}>` |

### 3. Subsequences

List all the 4-subsequences contained in the following data sequence: `<{1,3}{2}{2,3}{4}>`.

**Solution (14 subsequences):**

1. `<{1,3}{2}{2}>`
2. `<{1,3}{2}{4}>`
3. `<{1,3}{3}{4}>`
4. `<{1}{2}{2}{4}>`
5. `<{1}{2,3}{4}>`
6. `<{3}{2}{2}{4}>`
7. `<{3}{2,3}{4}>`
8. `<{1,3}{2}{3}>`
9. `<{1,3}{2,3}>`
10. `<{1}{2}{2,3}>`
11. `<{1}{2}{3}{4}>`
12. `<{3}{2}{2,3}>`
13. `<{3}{2}{3}{4}>`
14. `<{2}{2,3}{4}>`

List all the 3-element subsequences contained in the data sequence: `<{1,3}{2}{2,3}{4}>`.

**Solution (21 subsequences):**

1. `<{1,3}{2}{2,3}>`
2. `<{1,3}{3}{4}>`
3. `<{1,3}{2}{3}>`
4. `<{1}{2}{2,3}>`
5. `<{1}{3}{4}>`
6. `<{1}{2}{3}>`
7. `<{3}{2}{2,3}>`
8. `<{3}{3}{4}>`
9. `<{3}{2}{3}>`
10. `<{1,3}{2}{4}>`
11. `<{1,3}{2}{2}>`
12. `<{1,3}{2,3}{4}>`
13. `<{1}{2}{4}>`
14. `<{1}{2}{2}>`
15. `<{1}{2,3}{4}>`
16. `<{3}{2}{4}>`
17. `<{3}{2}{2}>`
18. `<{3}{2,3}{4}>`
19. `<{2}{2,3}{4}>`
20. `<{2}{2}{4}>`
21. `<{2}{3}{4}>`
