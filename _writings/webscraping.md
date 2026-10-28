---
title: "Gathering Data You Don't Have — How to Effectively Webscrape Anything"
subtitle: "External data collection strategies for analysts, engineers, and scientists"
category: Python
tags: [python, webscraping, selenium, beautifulsoup, data-collection]
order: 2
---

## Why Webscraping?

Often, the data needed for informed decisions isn't readily available within organizations. This is particularly true for startups lacking historical data and established companies tracking competitors.

My personal experience: I was at a startup competing in a crowded industry. Facing data scarcity, I initiated web scraping across food review and ordering platforms to gather sales acquisition insights necessary for strategic decision-making.

## Ethical Considerations

**Before you scrape anything**, check the website's scraping policies by appending `/robots.txt` to any domain (e.g., `amazon.com/robots.txt`). Respect terms of service and privacy policies. This isn't just courtesy — it's a legal consideration.

## Three Approaches to Webscraping

These sit on a spectrum from easiest to most customizable:

### 1. API

Pre-built data extraction interfaces provided by the platform itself.

- **Pros:** Highly structured, easily manipulated data formats
- **Cons:** Throttling limitations, rate limits

### 2. Network Console

Access "unpublished" data processing funnels via browser dev tools.

- **Pros:** Structured, processed data
- **Cons:** Not universally available; data may be encrypted

### 3. Python Libraries (BeautifulSoup / Selenium)

HTML-based web UI scraping — the most flexible option.

- **Pros:** Highly customizable for any webpage
- **Cons:** Dependent on UI syntax; unsustainable long-term as sites change their HTML

## Real-World Application: Singapore Supermarkets

For a checkout-optimization startup, I used Selenium to scrape product data from Giant and Sheng Shiong supermarkets. This enabled side-by-side price comparisons for product demonstrations.

## Key Challenges

- **Security barriers:** Major tech platforms (Facebook, Google) prevent scraping via traditional methods
- **Compliance:** Always verify `robots.txt` policies
- **Server load:** Excessive requests risk being classified as synthetic DDoS
- **Alternative tools:** BluePrism and UIPath can bypass enterprise security for RPA use cases

## Resources

- [Selenium](https://pypi.org/project/selenium/)
- [BeautifulSoup](https://pypi.org/project/beautifulsoup4/)
- BluePrism, UIPath for enterprise RPA
