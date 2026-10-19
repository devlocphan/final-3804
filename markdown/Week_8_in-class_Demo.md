# Week 8 in-class Demo

Source: [Week 8 in-class Demo.pdf](../Week%208%20in-class%20Demo.pdf)

## Page 1

### Seasonal index and deseasonalized data

| Year | Q1 | Q2 | Q3 | Q4 |
| --- | --- | --- | --- | --- |
| 2017 | 76 | 68 | 67 | 95 |
| 2016 | 75 | 66 | 64 | 89 |
| 2015 | 72 | 64 | 63 | 75 |

- `72/[(72+64+63+75)/4] = 1.05109` (the seasonal index for 2015 Q1).
- `64/[(72+64+63+75)/4] = 0.93430` (the seasonal index for 2015 Q2).

How to calculate the deseasonalized data based on three years?

`Deseasonalized data = actual data / average seasonal index`

`Ave_SI_Q1 = (SI_2015_Q1 + SI_2016_Q1 + SI_2017_Q1)/3`

`= (1.051094891 + 1.020408163 + 0.993464052)/3 = 1.021655702`

- Deseasonalized (2015 Q1) = `72 / Ave_SI_Q1 = 70.5`.
- Deseasonalized (2016 Q1) = `75 / Ave_SI_Q1 = 73.4`.
- Deseasonalized (2017 Q1) = `76 / Ave_SI_Q1 = 74.4`.

| Quarter | Actual | Seasonal Index | Deseasonalized Data |
| --- | --- | --- | --- |
| 2015Q1 | 72 | 1.051094891 | 70.5 |
| 2015Q2 | 64 | 0.934306569 | 70.6 |
| 2015Q3 | 63 | 0.919708029 | 70.9 |
| 2015Q4 | 75 | 1.094890511 | 63.4 |
| 2016Q1 | 75 | 1.020408163 | 73.4 |
| 2016Q2 | 66 | 0.897959184 | 72.8 |
| 2016Q3 | 64 | 0.870748299 | 72.0 |
| 2016Q4 | 89 | 1.210884354 | 75.3 |
| 2017Q1 | 76 | 0.993464052 | 74.4 |
| 2017Q2 | 68 | 0.888888889 | 75.0 |
| 2017Q3 | 67 | 0.875816993 | 75.4 |
| 2017Q4 | 95 | 1.241830065 | 80.3 |
