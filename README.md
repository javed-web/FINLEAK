# FinLeak — FinTech Revenue & Risk Leak Detective 🔎

> **Project Status:** 🚧 Under Active Development

---

## 💡 Why I Started This Project

I wanted to build a Data Analyst project which is something closer to the kind of problem an analyst actually face in a FinTech company.

A lot of portfolio projects stop at things like:

- Total revenue
- Monthly sales
- Top customers
- Basic Power BI dashboards

Those are useful for learning, but I wanted FinLeak to go one step further.

The idea behind FinLeak is simple:

> **PayFlow's transaction volume is increasing, but the money the company actually keeps is not increasing at the same rate.**

So instead of starting with a dashboard, I started with the question:

> **Where is the money being lost?**

Possible areas include payment failures, retries, refunds, chargebacks, gateway costs, discounts, cashback, and risky merchants.

The project is designed to investigate these areas using SQL and Python, and eventually present the findings through Power BI and an AI-assisted investigation layer.

---

## 🏦 The Business Scenario

**PayFlow** is a fictional Indian payments FinTech.

The company processes transactions through multiple payment gateways and payment methods.

As transaction volume grows, management notices that the financial contribution from those transactions isn't growing at the same pace.

There could be several reasons for this:

- 💳 Payment failures
- 🔁 Repeated payment attempts
- 💰 Refunds
- ⚠️ Chargebacks
- 🏦 Gateway and processing costs
- 🏷️ Discounts
- 🎁 Cashback
- 🚨 Risky merchant activity
- 📉 Other transaction-level anomalies

The goal of FinLeak is to investigate these areas and identify where the potential financial leakage is coming from.

---

## 🎯 What I Want FinLeak to Find

### 💳 Payment Problems

I want to answer questions such as:

- Which gateways have higher failure rates?
- Are failures concentrated around particular time periods?
- Which payment methods fail more frequently?
- How often are customers retrying payments?
- Which failure reasons occur most often?
- Are there unusual changes in gateway performance?

### 💰 Financial Leakage

The project will eventually investigate:

- Refund amounts
- Chargeback amounts
- Gateway fees
- Processing fees
- Platform fees
- Discounts
- Cashback
- Leakage by merchant
- Leakage by gateway
- Leakage by customer or segment

### 🚨 Merchant Risk

I also want to identify merchants showing unusual patterns, such as:

- High transaction failure rates
- High refund rates
- High chargeback rates
- High transaction values combined with abnormal behavior
- High risk scores
- Concentrated financial leakage

The purpose isn't to automatically label a merchant as fraudulent.

The purpose is to identify **merchants or patterns that deserve further investigation.**

---

## 🔍 The Main Idea Behind the Investigation

One design decision I made early was that I don't want the AI component to simply guess the root cause.

For example, if Gateway_A suddenly has a high failure rate, the system shouldn't automatically say:

> "Gateway_A had a server outage."

We don't actually have evidence of a server outage.

Instead, the analysis should first establish what happened:

> Gateway_A's payment-attempt failure rate was 22.44% during the identified incident window compared with 7.28% outside the window.

That's evidence.

The AI can then turn that evidence into an investigation hypothesis, such as:

> This pattern warrants investigation into gateway-specific operational factors.

So the basic approach I'm following is:

```text
Data
 ↓
Analysis
 ↓
Evidence
 ↓
Investigation Hypothesis
 ↓
Business Interpretation
```

The AI should help with the **investigation**, not invent facts that aren't present in the data.

---

## 🗄️ Database Design

I decided to use **MySQL** as the main database.

The database is called:

```text
finleak
```

The current data model contains these main tables:

```text
customers
merchants
transactions
payment_attempts
refunds
chargebacks
transaction_fees
```

The basic relationship looks like this:

```text
Customer
   │
   └── Transaction
          │
          ├── Payment Attempts
          ├── Refund
          ├── Chargeback
          └── Transaction Fees
```

This structure gives me the ability to move between different levels of analysis.

For example:

```text
Transaction
    ↓
Merchant
    ↓
Gateway
    ↓
Category
    ↓
Overall business impact
```

---

## 🐍 Technology Stack

### 🐍 Data Generation

Python is being used to generate the synthetic payment ecosystem.

Libraries currently used:

- Pandas
- NumPy
- Faker
- mysql-connector-python

### 🗄️ Database

**MySQL**

Used to store and query the generated payment data.

### 📊 Data Analysis

The planned analysis layer uses:

- SQL
- Python
- Pandas
- NumPy
- Scikit-learn

### 📈 Visualization

**Microsoft Power BI**

Power BI will be used to turn the analytical results into business-facing dashboards.

### 🤖 Investigation & AI

After the core data and analytics layers are complete, I plan to build:

- A Python-based investigation engine
- Evidence collection logic
- An AI-assisted investigation component

---

## 📅 Data Period

The transaction data covers:

**January 1, 2025 → June 30, 2026**

I chose this period so that the dataset contains enough history for things like:

- Monthly trends
- Gateway comparisons
- Merchant comparisons
- Failure analysis
- Time-based analysis
- Anomaly detection
- Incident investigation

---

## 🧪 Synthetic Data Approach

Since real payment-company data isn't available for this project, I'm using synthetic data.

However, I didn't want to generate completely random rows.

The goal is to create data with:

- Realistic distributions
- Relationships between tables
- Different customer and merchant segments
- Different payment methods
- Multiple gateways
- Normal operational variation
- Controlled abnormal scenarios

This gives the later SQL and Python analysis something meaningful to investigate.

---

## 🚨 Ground-Truth Scenarios

One of the more important parts of the data-generation process is intentionally creating a few known scenarios.

The reason is simple:

If I introduce an anomaly whose existence I already know, I can later test whether my analytical pipeline is actually capable of finding it.

One scenario already implemented involves **Gateway_A**.

The controlled incident window is:

**May 12, 2026 23:00 → May 13, 2026 01:00**

The expected behavior is that Gateway_A should show noticeably worse payment-attempt performance during this period.

The ground-truth information is kept separately from the main analytical data.

That means I can later compare:

```text
What the analysis discovered
             VS
What was intentionally injected
```

This gives me a way to test the investigation logic instead of simply assuming that it works.

---

## 🏗️ How I'm Building FinLeak

I'm building the project in stages rather than generating everything at once.

Current progress:

| Stage | Component | Status |
|---|---|---|
| 1 | Project Foundation | ✅ Completed |
| 2 | Customers & Merchants | ✅ Completed |
| 3 | Transactions | ✅ Completed |
| 4 | Payment Attempts | ✅ Completed |
| 5 | Refunds & Chargebacks | ⏳ Next |
| 6 | Transaction Fees | ⏳ Pending |
| 7 | SQL Investigation Layer | ⏳ Pending |
| 8 | Python Analytics | ⏳ Pending |
| 9 | Power BI Dashboard | ⏳ Pending |
| 10 | Investigation Engine | ⏳ Pending |
| 11 | AI Investigation Assistant | ⏳ Pending |
| 12 | Final Documentation | ⏳ Pending |

---

## 🧪 Validation Approach

I'm not treating a stage as complete just because the Python script runs successfully.

For each stage, I'm following:

```text
Build
  ↓
Validate
  ↓
Document
  ↓
Lock 🔒
  ↓
Move to next stage
```

Validation includes things such as:

- Row counts
- Duplicate checks
- Foreign-key relationships
- Null checks
- Value ranges
- Distribution checks
- Business-rule checks
- Ground-truth validation

This is particularly important because an error in an early data layer can produce incorrect results in every layer built after it.

---

## 📊 Current Progress

So far, the core customer, merchant, transaction, and payment-attempt layers have been generated and validated.

Current volumes:

| Data | Records |
|---|---:|
| Customers | **100,000** |
| Merchants | **10,000** |
| Transactions | **1,000,000** |
| Payment Attempts | **1,038,060** |

The payment-attempt layer also contains the controlled Gateway_A incident.

During the incident:

| Period | Attempts | Failed Attempts | Failure Rate |
|---|---:|---:|---:|
| Outside Incident | 311,040 | 22,655 | 7.28% |
| Incident | 1,493 | 335 | **22.44%** |

The incident-period failure rate is approximately **3.1×** the rate outside the incident window.

This is one of the first signals that I expect the later investigation layer to discover.

---

## 📂 Planned Project Structure

The project is being organized roughly like this:

```text
FINLEAK/
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── ground_truth/
│
├── database/
│
├── python/
│
├── sql/
│
├── powerbi/
│
├── ai/
│
├── docs/
│
├── .gitignore
└── README.md
```

## 🔒 Project Principle

The main idea I want to maintain throughout this project is:

> **Don't just report what happened. Find the evidence, understand where the problem is concentrated, and identify what should be investigated next.**

That's ultimately what I want FinLeak to demonstrate as a Data Analyst project.
