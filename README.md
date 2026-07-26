# portfolio-risk-management

# Introduction
Setting up a 5-asset portfolio (GS, MSCI, V, CRISIL.NS, HDFCBANK.NS), spanning US and Indian markets, chosen to represent investment banking, financial data/analytics, and fintech; 2019-2025 daily price data via yfinance

# Data pipeline & known limitation
Cross-market date alignment handled by dropping non-overlapping trading days (1674 clean days from original data with 340 mismatched values); explicit limitation noted — raw local-currency (INR/USD) returns used without FX adjustment, meaning correlation figures represent local-currency co-movement, not a single investor's true realized cross-currency portfolio risk.

# Covariance & correlation analysis
Covariance matrix computed on daily returns; correlation matrix derived; key finding — the three US assets (GS, MSCI, V) show notably higher correlation with each other (0.47-0.57 range) than with either Indian asset (0.08-0.23 range), consistent with shared US-market risk factors not transmitting as strongly across markets.

# Optimization
scipy.optimize.minimize (SLSQP) used to find the minimum-variance portfolio; a real bug encountered and fixed — default solver tolerance was too loose relative to the small scale of variance values, causing false early convergence at the initial equal-weight guess; fixed with an explicit tighter tolerance (tol=1e-12)

# Results
Minimum-variance portfolio weights — CRISIL 21.6%, GS 7.1%, HDFC 36.6%, MSCI 7.8%, V 26.9%; variance reduced ~12% versus equal-weight (0.0001307 vs 0.0001491); optimizer specifically underweighted GS and MSCI due to their high mutual correlation and shared correlation with Visa.

# Efficient frontier
Traced across 50 target return levels; every individual asset sits to the right of (higher risk than) the frontier at its equivalent return level, visually confirming diversification benefit; noted the lower branch of the curve (below the minimum-variance point) is the inefficient region, not shown as a rational choice.
