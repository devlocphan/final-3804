# Lab 5.1 Solution

Source: [Lab 5.1 Solution_UG.pdf](../Lab%205.1%20Solution_UG.pdf)

## Page 1

### 5. Jaccard Similarity

- `rA = {item 1, item 2, item 4, item 5}`
- `rB = {item 1, item 3, item 4, item 5}`
- `rA ∩ rB = {item 1, item 4, item 5}`, `|rA ∩ rB| = 3`
- `rA ∪ rB = {item 1, item 2, item 3, item 4, item 5}`, `|rA ∪ rB| = 5`
- `Jaccard similarity (A,B) = |rA ∩ rB| / |rA ∪ rB| = 3/5 = 0.6`

Similarly:

- Jaccard similarity of (A,C), (A,D), (A,E), (A,F), (B,C), (B,D), (B,E), (B,F) = 0.8.
- Jaccard similarity of (C,D), (C,E), (C,F), (D,E), (D,F), (E,F) = 1.

### Pearson Similarity

`rowA = (8 + 1 + 2 + 7) / 4 = 4.5`

`rA = {8-4.5, 1-4.5, 0, 2-4.5, 7-4.5} = {3.5, -3.5, 0, -2.5, 2.5}`

Similarly:

- `rB = {-2.75, 0, 0.25, 2.25, 0.25}`
- `rC = {1.8, -4.2, 1.8, -2.2, 2.8}`
- `rD = {-0.4, -1.4, 1.6, -1.4, 1.6}`
- `rE = {-3.6, 2.4, -0.6, 1.4, 0.4}`
- `rF = {2.2, -2.8, 2.2, -2.8, 1.2}`

`Pearson similarity (A,B) = dot(rA,rB) / (|rA| * |rB|)`

`dot(rA,rB) = 3.5*(-2.75) + (-3.5)*0 + 0*0.25 + (-2.5)*2.25 + 2.5*0.25`

`|rA| = [3.5^2 + (-3.5)^2 + 0^2 + (-2.5)^2 + 2.5^2]^(1/2)`

`|rB| = [(-2.75)^2 + 0^2 + 0.25^2 + 2.25^2 + 0.25^2]^(1/2)`

`Pearson similarity (A,B) = -0.6733`

Similarly:

| Pair | Pearson similarity |
| --- | --- |
| (A,C) | 0.9079 |
| (A,D) | 0.5962 |
| (A,E) | -0.8391 |
| (A,F) | 0.8733 |
| (B,C) | -0.4040 |
| (B,D) | -0.1154 |
| (B,E) | 0.7907 |
| (B,F) | -0.6221 |
| (C,D) | 0.8478 |
| (C,E) | -0.7017 |
| (C,F) | 0.9298 |
| (D,E) | -0.3007 |
| (D,F) | 0.7897 |
| (E,F) | -0.8139 |

## Page 2

### 6. Rating of Item 2 by User B

The Item-Item Collaborative Filtering should be used with `|N|=2`, where N is the number of nearest neighbors.

| Item | User A | User B | User C | User D | User E | User F |
| --- | --- | --- | --- | --- | --- | --- |
| Item 1 | 8 | 2 | 7 | 5 | 1 | 8 |
| Item 2 | 1 | | 1 | 4 | 7 | 3 |
| Item 3 | | 5 | 7 | 7 | 4 | 8 |
| Item 4 | 2 | 7 | 3 | 4 | 6 | 3 |
| Item 5 | 7 | 5 | 8 | 7 | 5 | 7 |

Similar to Exercise 8, here we consider items, rather than users.

- Pearson similarity of (item 2, item 1) = Pearson similarity of (item 1, item 2) = -0.7864.
- Pearson similarity of (item 2, item 3) = -0.6013.
- Pearson similarity of (item 2, item 4) = 0.6663.
- Pearson similarity of (item 2, item 5) = -0.7186.

Item 3 and item 4 have the top two Pearson similarity values with item 2.

Predict by taking weighted average: Rating of item 2 by user B is

`(-0.6013*5 + 0.6663*7) / (-0.6013 + 0.6663) = 25.5015`

Such a value of 25.5015 doesn't make any sense here, because one of the Pearson similarity values is minus. So normally in this case, if the Pearson correlation < 0, we don't use it for rating. Therefore, in the case of rating item 2 by user B, the answer will be 7, by only considering item 4.

### Rating of Item 3 by User A

- Pearson similarity of (item 3, item 1) = Pearson similarity of (item 1, item 3) = 0.8626.
- Pearson similarity of (item 3, item 2) = -0.6013.
- Pearson similarity of (item 3, item 4) = -0.7432.
- Pearson similarity of (item 3, item 5) = 0.8444.

Item 1 and item 5 have the top two Pearson similarity values with item 3.

Predict by taking weighted average: Rating of item 3 by user A is

`(0.8626*8 + 0.8444*7) / (0.8626 + 0.8444) = 7.5053`
