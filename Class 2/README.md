## The Illusion of Growth & The Composition Effect

### Objective
Built a live economic data pipeline using the Federal Reserve API to analyze five decades of wage stagnation and identify statistical biases in standard labor market indicators. This project demonstrates how composition effects can create misleading narratives during economic crises.

### Technical Stack
- **Python** (pandas, matplotlib)
- **fredapi** - Federal Reserve Economic Data API
- **Statistical Methods** - Real wage calculation, index rebasing, composition effect correction

### Methodology

**Phase 1: Real Wage Construction**
- Ingested nominal wage series (`AHETPI`) and Consumer Price Index (`CPIAUCSL`) via FRED API
- Calculated inflation-adjusted real wages: `Real Wage = (Nominal Wage / CPI) × 100`
- Visualized 50+ years of wage trends to reveal purchasing power stagnation

**Phase 2: Anomaly Detection**
- Identified a dramatic 2020 spike in real wages during the pandemic recession
- Recognized this as a statistical paradox: wages appeared to surge during mass unemployment

**Phase 3: Composition Effect Correction**
- Fetched Employment Cost Index (`ECIWAG`) to control for workforce composition changes
- ECI methodology: Holds job mix constant, measuring wage growth for the *same types of jobs* over time
- Rebased both standard wages and ECI to 2015=100 for direct comparison

### Key Findings

**The Money Illusion (1964-Present)**
Nominal wages increased dramatically over 50 years, but real purchasing power remained nearly flat—illustrating the classic economic concept of "money illusion" where workers focus on nominal rather than real income.

**The Pandemic Paradox (2020)**
Standard wage measures showed an artificial 10%+ spike in Q2 2020, suggesting workers were thriving during the pandemic. **Reality**: Lower-wage workers (retail, hospitality) were disproportionately laid off, mechanically raising the average wage among *remaining* workers. The ECI, which controls for this composition effect, showed stable ~3% growth—revealing the "boom" was purely statistical artifact, not genuine labor market strength.

**Implication**: Policymakers and analysts must use composition-adjusted metrics (like ECI) during structural economic shocks to avoid misinterpreting labor market conditions. Standard averages can be dangerously misleading when workforce composition shifts dramatically.
