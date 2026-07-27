# Personal AI Assistant

A personal AI assistant ecosystem combining Telegram bots, financial tooling, and a local dashboard, built through iterative scripting rather than a traditional dev workflow.

## What it does

This system runs continuously and handles a mix of financial monitoring and criteria based recommendations, news aggregation, email and calendar management, and general purpose conversation through multiple coordinated Telegram bots.

**Financial tools**

* Portfolio tracker covering holdings, pulling data from Finnhub and yfinance into SQLite
* Stress testing against portfolio positions
* Watchlist of defined tickers with sentiment scoring
* Flask dashboard for visualizing portfolio and market data

**News \& research**

* News pipeline using GNews and NewsAPI 
* SerpAPI based travel search
* Flight monitoring: variable and fixed routes SQLite watchlist with price drop alerts on a cron schedule

## Architecture

* **Language:** Python 3.11 (isolated in a dedicated virtual environment)
* **Bots:** Telegram bots running as separate processes
* **Dashboard:** Flask app, served locally
* **Storage:** SQLite
* **Scheduling \& uptime:** LaunchAgents keep the bots running continuously; crontab handles scheduled notifications

## Why it exists

This project started as a way to set up bots, which led to refreshing my skills with terminal and file editing workflows, then expanded step by step into stock data, financial modeling, and email/reporting capabilities. Every module here was built through direct, iterative scripting.

I think of this as a working demonstration of staying curious and maintaining the delivery approach I bring to project and program management, applied to building real results.

## Technical skills reflected in this project

**Data \& APIs**

* Third party API integration (Finnhub, yfinance, GNews, NewsAPI, SerpAPI, Tavily)
* SQLite for persistent local data
* Fallback design for reliability (GNews primary, NewsAPI fallback)

**Application patterns**

* Flask for dashboards and web apps
* Multi process bot architecture
* Scheduled/background automation via LaunchAgents and cron

**Automated delivery**

* Prompt and scripting as a repeatable process for shipping working output
* Applying AI to structured, data driven decision problems

## Status

Actively expanding. Recent exploration includes Alpaca as an API friendly broker for rules based trading strategies, and Claude Cowork for scheduled automation and reporting.

## Disclaimer

This is a personal project run for individual use, not a production system. Financial data and any portfolio insights it generates are for personal reference only.

