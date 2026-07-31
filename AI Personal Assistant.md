# Personal AI Assistant

A personal AI assistant ecosystem combining Telegram bots, financial tooling, and a local dashboard, built through scripting.

## What it does

This system runs continuously and handles a mix of financial monitoring, news aggregation, and general purpose conversation through two coordinated Telegram bots.

**Financial tools**

- Portfolio tracker covering variety of holdings, pulling data from Finnhub and yfinance into SQLite  
- Stress testing against portfolio positions  
- Watchlist of tickers with sentiment scoring  
- Flask dashboard for visualizing portfolio and market data

**News & research**

- News pipeline using GNews as the primary source with NewsAPI as fallback  
- SerpAPIvbased travel search  
- Flight monitoring: a fixed route SQLite watchlist with price drop alerts on a cron schedule

**Conversation**

- A second bot, Hermes, runs as an independent process for general conversation and web search (via Tavily), separate from the bot that handles financial and personal data

## Architecture

- **Language:** Python 3.11 (isolated in a dedicated virtual environment)  
- **Bots:** Two Telegram bots running as separate processes  
- **Dashboard:** Flask app, served locally  
- **Storage:** SQLite for portfolio, watchlist, and flight tracking data  
- **Scheduling & uptime:** LaunchAgents keep the bots running continuously; crontab handles scheduled digests and price-drop checks

## Why it exists

I'm not a professional developer, this project started as a way to set up a bot, which led to refreshing my terminal and file editing workflows from scratch, then expanded step by step into stock data, financial modeling, and email/reporting capabilities. Every module here was built through iterative scripting, in part with AI and in part with human intervention.

I think of this as a working demonstration of the delivery approach I bring to leading initiatives, applied to building real software.

## Technical skills reflected in this project

**Data & APIs**

- Third party API integration (Finnhub, yfinance, GNews, NewsAPI, SerpAPI, Tavily)  
- SQLite for persistent local data  
- Fallback design for reliability (GNews primary, NewsAPI fallback)

**Application patterns**

- Flask for dashboards and web apps  
- Multi process bot architecture   
- Scheduled/background automation via LaunchAgents and cron

**Automated delivery**

- Scripting driven repeatable process for shipping working software  
- Applying AI to structured, data driven decision problems

## Status

Actively expanding. Recent exploration includes Alpaca as an API friendly broker for rules based trading strategies, and Claude Cowork for scheduled automation and reporting.

## Disclaimer

This is a personal project run for individual use, not a production system. Financial data and any portfolio insights it generates are for personal reference only.  
