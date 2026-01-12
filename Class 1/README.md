# Global Purchasing Power Parity Analysis via the Big Mac Index

## Objective

This project tests the **Law of One Price** by analyzing implied purchasing power parity (PPP) exchange rates derived from The Economist's Big Mac Index (January 2015).

## Methodology

- Ingested raw Big Mac price data across 20+ countries using Python dictionaries
- Calculated implied PPP exchange rates by comparing local Big Mac prices to the U.S. benchmark ($4.79)
- Computed percentage currency misalignment relative to market exchange rates
- Visualized valuation disparities to identify potential arbitrage opportunities

## Key Findings

The analysis reveals significant deviations from purchasing power parity across global currencies:

**Most Undervalued Currencies:**
- Russian Ruble: ~69% undervalued (largest deviation)
- South African Rand: ~52% undervalued
- Indonesian Rupiah & Egyptian Pound: ~48% undervalued

**Most Overvalued Currencies:**
- Norwegian Krone: ~32% overvalued (only significant premium)
- Brazilian Real: ~6% overvalued

**Near Parity:**
- British Pound, Australian Dollar, and Euro showed modest undervaluation (~5-10%)
- U.S. Dollar serves as the baseline (0% deviation by definition)

## Economic Interpretation

The persistent undervaluation of emerging market currencies suggests structural barriers to arbitrage—including trade costs, non-tradable inputs (labor, rent), and capital controls—that prevent the Law of One Price from holding in practice. Norway's overvaluation reflects its high-cost economy driven by oil wealth and elevated wages.
