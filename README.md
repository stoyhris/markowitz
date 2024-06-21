# Modern Portfolio Theory 

## Background
Developed by Henry Markowitz, modern portfolio theory seeks to optimize portfolio allocations by minimizing risk subject to achieving a minimum return as represented in the following optimization problem:
$$\text{Minimize: } w^T \Sigma w$$ 
$$\text{Subject to: \quad{} } w^T \mu >= r, \quad{} 1^Tw = 1, \quad{} w \geq 0$$

Where $w$ represents the optimal portfolio weights, $\Sigma$ represents the covariance matrix, and $\mu$ represents the estimated returns.

This projects constructs an optimal portfolio of S&P500 stocks, estimates its performance, and evaluates it against a portfolio benchmark. 

## Data 
To gather the necessary data, we use web scraping on a Wikipedia page for each stock's ticker as well as Yahoo Finance for all returns and covariances. 

## Portfolio Construction 

### Efficient Frontier 
We first set up the above optimization problem, as well as its dual, and generate an efficient frontier to model the optimal tradeoff between risk and return by modulating the minimum acceptable return.

<p align="center">
  <img src="https://github.com/stoyhris/markowitz/assets/113132376/da01e5da-b560-4883-a086-434348ece73f" alt="Efficient Frontier"/>
</p>

### Mean Variance Optimization 
We choose an acceptable target return from the frontier, and derive optimal portfolio weights by solving the associated optimization problem. To further diversify, we specify that no single stock should make up more than 5% of the portfolio. We can also output the top stocks in our portfolio.

| Ticker	| Allocation (%)| | Ticker	| Allocation (%)| | Ticker	| Allocation (%)| | Ticker	| Allocation (%)|
|---------|---------------|-|---------|---------------|-|---------|---------------|-|---------|---------------|
| WRK	| 5.00 | | LLY	| 5.00 | | GD	| 4.88 | | CEG	| 3.44 |
| NRG	| 5.00 | | LDOS	| 5.00 | | QCOM	| 4.71 | | DECK	| 3.15 |
| MCK	| 5.00 | | PGR	| 5.00 | | NVDA	| 4.70 | | WAB	| 3.07 |
| BOE	| 5.00 | | VST	| 5.00 | | BSX	| 4.13 | | TSN	| 2.79 |
| COR	| 5.00 | | WMT	| 4.99 | | FANG	| 3.97 | | CB	| 2.25 |

### Performance Estimation 
We use a Monte Carlo simulation to estimate our portfolio's performance in the next 30 days. Results indicate that we can expect to gain at most 15% and on average 7%. Although we can expect to lose at most 2%, the worst 5% of cases have us winning on average 1%. 

<p align="center">
  <img src="https://github.com/stoyhris/markowitz/assets/113132376/a2ffa608-207d-4b78-8710-74cab1a34e9d" alt="Monte Carlo Simulation"/>
</p>

With a starting value of 100, here is the estimated performance after 30 days:

| Metric | Value ($) |
|---------|----------|
| Mean | 107.07 |
| Median | 107.03 |
| Max | 115.366 |
| Min | 98.87 |
| Lower 5% CVaR | 100.91 |

### Performance Testing 
#### Back Testing
First, we conduct a back-test of our portfolio against an equally weighted S&P500 portfolio. Results show that the optimal portfolio significantly outperforms the benchmark portfolio, which is expected because the optimal portfolio is trained on this data. 

<p align="center">
  <img src="https://github.com/stoyhris/markowitz/assets/113132376/c03ae7b8-78b1-48fb-955d-23b7525e1f72" alt="Back-test"/>
</p>


#### Forward Testing
Next, we evaluate our portfolio on data it has not yet seen. Once again, results show that the optimal portoflio outperforms the benchmark portfolio. This indicates that our portfolio is robust to future data, at least in the short-term (1 month). 

<p align="center">
  <img src="https://github.com/stoyhris/markowitz/assets/113132376/b6adba99-2d15-4f8b-9694-cf285d09abaf" alt="Forward-test"/>
</p>


#### Full Testing 
Finally, we evaluate our portfolio on the total span of data: a year which it has seen as well as a month which it has not seen. As indicated from the previous two tests, the optimal portfolio signficantly outperforms the benchmark. 

<p align="center">
  <img src="https://github.com/stoyhris/markowitz/assets/113132376/3f427987-ea09-4722-90f9-b99b347699f7" alt="Full-test"/>
</p>

## Conclusion 
Optimization methods can be fruitful in constructing optimal portfolios for a given set of stocks. Monte Carlo simulations and empirical experiments indicate that an optimal portfolio will almost always significantly out-perform the highly diversified equal-weighting portfolio. 
