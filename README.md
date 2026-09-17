# portfolio-risk-management

# Introduction
Setting up a 5-asset portfolio (GS, MSCI, V, CRISIL.NS, HDFCBANK.NS), spanning US and Indian markets, chosen to represent investment banking, financial data/analytics, and fintech; 2019-2025 daily price data via yfinance

# Data pipeline & known limitation
Cross-market date alignment handled by dropping non-overlapping trading days (1674 clean days from original data with 340 mismatched values); explicit limitation noted — raw local-currency (INR/USD) returns used without FX adjustment, meaning correlation figures represent local-currency co-movement, not a single investor's true realized cross-currency portfolio risk.

# Covariance & correlation analysis
Covariance matrix computed on daily returns; correlation matrix derived; key finding — the three US assets (GS, MSCI, V) show notably higher correlation with each other (0.47-0.57 range) than with either Indian asset (0.08-0.23 range), consistent with shared US-market risk factors not transmitting as strongly across markets.

# Results
- Minimum-variance portfolio weights — CRISIL 21.6%, GS 7.1%, HDFC 36.6%, MSCI 7.8%, V 26.9%; variance reduced ~12% versus equal-weight (0.0001307 vs 0.0001491); optimizer specifically underweighted GS and MSCI due to their high mutual correlation and shared correlation with Visa.
- Real GS options chain pulled via yfinance, call/put payoff diagrams built from live market data ($1040 strike, $78.00 premium); put-call parity verified against real bid/ask data (~1.5% gap, attributed to lastPrice staleness and assumed 5% risk-free rate rather than genuine arbitrage, given GS options' high liquidity).
- Black-Scholes implemented; all four Greeks (Delta 0.562, Gamma 0.0022, Theta -0.498, Vega 1.956) computed and interpreted on the real contract.
- 10,000-path GBM simulation of GS price at expiration, option payoffs averaged and discounted; converged to $78.01 vs. Black-Scholes' $78.00, confirming two independent pricing methods agree.


#Author
Snehil Kejriwal — Economics + B.Tech CSE, BITS Pilani Hyderabad github.com/snehilkejriwal-exp19




