# Random Variables

## Random Variable aka RV
Use upper case letters to denote random variables.
Use lower case letters to denote their observed values

Can summarize the probabilites of RV X as a table:
(where x is the expected amount of heads)
| x | 0 | 1 | 2 |
|-----|----|--------| -----|
| P(X = x) | 1/4 | 1/2 | 1/4 |

## Probabilty Distributions
**Discrete** and **Continuous**

Denote by X the RV, and its range by R<sub>X</sub>
- **Discrete:** the number of values in R<sub>X</sub> us finite or countable.
- **Continuous:** R<sub>X</sub> is an interval or a collection of intervals.
`
### Probability Distribution Function
- To check if a function f(x) is a p.d.f,  it suffices to check 2 things
1) f(x) >= 0 for all x subset of R<sub>X</sub>; anf f(x) = 0 for x not a subset of R<sub>X</sub>
2) summation of the range of the integral of f(x) = 1

### Cumulative Distribution Function
- If X is a continuous RV,
F(x) = integral of f(t) dt

To get CDF, integrate PDF,
To get PDF, differentiate CDF

The ranges of F(x) and f(x) satisfy:
- 0 <= F(x) <= 1;
- for discrete distribution, 0 <= f(x) <= 1;
- for continuous distribution, f(x) >= 0, but no need that f(x) <=1

## Expectation and Variance of a RV

