# PropertyLoop Fund Data Chatbot

## Overview

This project implements a simple and reliable chatbot that answers questions **only** using the data provided in two CSV files:

- `holdings.csv`
- `trades.csv`

The main goal of this solution is **correctness and safety**.  
The chatbot is intentionally designed to avoid hallucinations or assumptions.  
If a question cannot be answered using the available data, it responds with:

> **Sorry can not find the answer**

This behavior is deliberate and aligns with real-world expectations for financial data systems.

---

## Design Approach

Although large language models can be useful, this problem involves **structured tabular data**.  
For this reason, the core logic is implemented using **deterministic Pandas operations**, which guarantees:

- Accurate numerical results  
- Fully explainable logic  
- Zero risk of hallucinated answers  

An LLM could optionally be added later for intent classification or user experience, but **all calculations are intentionally kept deterministic**.

---

## High-Level Architecture


``
User Question 
↓
Intent Detection
↓
Pandas-based Data Computation
↓
Answer from CSV data
OR
"Sorry can not find the answer"
``

The chatbot never uses the internet or external data sources.

---

## Supported Question Types

### 1. Holdings and Trades Count

The chatbot can answer count-based questions for a specific fund.

**Examples:**
- `Total number of holdings for fund Garfield`
- `Total number of trades for fund Heather`
- `Total number of holdings and trades for fund Garfield`

Each row in the CSV files is treated as a single holding or trade, ensuring accurate counts.

---

### 2. Fund Performance (Profit and Loss)

The chatbot can compare fund performance based on **yearly profit and loss**.

**Examples:**
- `Which funds performed better depending on the yearly Profit and Loss?`
- `Show yearly profit and loss by fund`

**Note on P&L calculation:**  
The dataset does not contain an explicit P&L column.  
Yearly P&L is therefore derived as:



Yearly P&L = Sum of trade Principal grouped by Fund and Year


This method is clearly documented and consistently applied.

---

## Unsupported Questions

Any question that cannot be answered from the provided CSV files will return the fallback response.

**Examples of unsupported questions:**
- Stock or market prices
- Fund managers or company details
- Predictions or forecasts
- Any external or internet-based information

This strict limitation prevents incorrect or speculative answers.

---

## How to Run the Project

#### 1. Install dependencies:
```bash
pip install pandas
```

#### 2. Run the chatbot:
```bash
python src/chatbot.py
```

Ask questions directly in the terminal.
Type exit to quit.

## Key Strengths of This Solution

- Uses only the provided datasets
- Deterministic and verifiable results
- No hallucination risk
- Simple and readable code
- Easy to extend with additional question types
- Suitable for financial data use cases

## Summary

This project delivers a reliable, explainable, and production-safe chatbot that meets all task requirements.


