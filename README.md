# Fibonacci Search for Chapter Bracketing

Fibonacci Search ensures maximum narrowing of the interval [a, b] containing the minimum, given a limited number of queries.

## Kiefer's Ratios

Based on [Sequence Minimax Search For A Maximum](https://www.ams.org/journals/proc/1953-004-03/S0002-9939-1953-0055639-3/S0002-9939-1953-0055639-3.pdf), two important ratios are used:

- $y_1 = U_{N-2}/U_N$
- $y_2 = U_{N-1}/U_N$

Example:
- $N = 6$
- Fibonacci sequence: $F = 1, 1, 2, 3, 5, 8, 13$
- $y_1 = 5/13$
- $y_2 = 8/13$

For a 13-unit line segment, we can divide it into 5 and 8 at points c and d using the two preceding Fibonacci numbers. This process continues symmetrically until we reach 1-1 segments.

## Finding n

Example:
- $\frac{b-a}{\epsilon} = F_n$
- $b-a=1$
- $\epsilon = 0.01$
- $\frac{1}{0.01} = 100$

We need to choose n such that $F_n \geq 100$:

| n | $F_n$ |
|:-:|:-----:|
| 0 | 1     |
| 1 | 1     |
| 2 | 2     |
| ... | ... |
| 10 | 89   |
| 11 | 144  |

**Johnson's observation:** With $F_{20} > 10000$, the maximum interval is always within $10^{-4}$ with 20 calculations, while Dichotomous Search requires 28.

## Binet's Formula

Fibonacci numbers can be determined using Binet's formula:

$F_n = \frac{\varphi^n - (1 - \varphi)^n}{\sqrt{5}}, \varphi = \frac{1+\sqrt5}{2} \approx 1.61803$

Where $\varphi$ is the golden ratio.

The ratio between consecutive Fibonacci values is:

$\frac{F_n}{F_{n-1}} = \varphi\frac{1 - s^{n + 1}}{1 - s^n}, s = (1-\sqrt5)/(1+\sqrt5) \approx -0.382$

## Fibonacci Search Algorithm

- $c = a + \frac{F_{n-2}}{F_n}(b - a)$
- $d = a + \frac{F_{n-1}}{F_n}(b - a)$
- If f(c) < f(d), discard the rightmost interval.
- Otherwise, discard the leftmost interval.
- Reduce the set until the stopping condition is met.

## Properties of Fibonacci Algorithm

- Optimal in providing the largest initial ratio to the final interval for a fixed number of function evaluations.
- Relationship with Golden section algorithm:

$$\lim_{N \to \infty} \frac{F_{N-1}}{F_N} = \frac{\sqrt5 - 1}{2} \approx 0.618...$$

## Example

$f(x) = -\frac{1}{(x-1)^2}(logx - 2\frac{x-1}{x+1})$

Given: minimum is in [1.5, 4.5]. Reduce the interval to 2/13 of the original.

Thus, $F_n > 3 \Rightarrow n = 5$

| i |     | $a_i$ | $c_i$ | $d_i$ | $b_i$ |
|:-:|:---:|:-----:|:-----:|:-----:|:-----:|
| 1 | x   | 1.5   | 2.64  | 3.36  | 4.5   |
|   | 100f(x) | -2.188 | -2.591 | -2.323 | -1.809 |
| 2 | x   | 1.5   |       |       | 3.36  |
|   | 100f(x) | -2.188 | -2.670 | -2.591 | -2.323 |
| 3 | x   | 1.5   |       |       | 2.64  |
|   | 100f(x) | -2.188 | -2.621 | -2.670 | -2.591 |
| 4 | x   | 1.92  |       |       | 2.64  |
|   | 100f(x) | -2.621 | -2.670 | -2.660 | -2.591 |
| 5 | x   | 1.92  |       |       | 2.34  |
|   | 100f(x) | -2.621 | -2.57  | -2.670 | -2.660 |
