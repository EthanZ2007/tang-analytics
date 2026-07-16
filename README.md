# Tang Analytics

Data-driven analysis of Tang Asian Fusion's sales performance, aimed at identifying the drivers behind the restaurant's revenue decline and mapping a path back to its ~$70k/month peak (last sustained in 2022-2024). Built as both a working decision-support tool for the restaurant and a portfolio piece demonstrating end-to-end data analysis: cleaning raw POS exports, exploratory analysis, and translating findings into concrete business recommendations.

## Tech Stack

- Python (pandas, numpy)
- Jupyter Notebook
- matplotlib / seaborn
- SQL Server
- Docker

## Analysis Index

| Analysis | Key Finding | Docs | Notebook |
|---|---|---|---|
| Data Cleaning | Real customer-ID reliability is 71.8%, not ~86% | [docs/01-data-cleaning.md](docs/01-data-cleaning.md) | [notebooks/01_data_cleaning.ipynb](notebooks/01_data_cleaning.ipynb) |
| Customer Analysis | Top 10% of customers drive 56% of revenue, but frequent customers don't spend more per visit — just more often | [docs/02-customer-analysis.md](docs/02-customer-analysis.md) | [notebooks/02_customer_analysis.ipynb](notebooks/02_customer_analysis.ipynb) |
| Menu Analysis | Bottom 50% of menu items by order count generate only 3.4% of revenue | [docs/03-menu-analysis.md](docs/03-menu-analysis.md) | [notebooks/03_menu_analysis.ipynb](notebooks/03_menu_analysis.ipynb) |
