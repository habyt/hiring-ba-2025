# Business Analyst Take-Home Test: Stripe Invoice Analysis

## Overview

This take-home test evaluates your SQL and Python skills in the context of analyzing Stripe invoice data. At Habyt, we deal extensively with Stripe invoices and contract data across our property management business.

This exercise simulates real-world business scenarios you might encounter as a Business Analyst at Habyt. You'll be analyzing a dataset containing contracts, invoices, and related entities to extract meaningful insights that could drive business decisions.

## Getting Started

### Prerequisites

- Python 3.8 or higher
- Knowledge of SQL
- Experience with pandas, matplotlib, and other data analysis libraries
- Git (to clone this repository)

### Setup

1. Install the required dependencies:

```bash
pip install -r requirements.txt
```

2. The provided SQLite database (`analyst_test_data.db`) contains the following tables:
   - Customers
   - Contracts
   - ContractItems
   - Invoices
   - InvoiceLineItems

## Task Description

Your task is to analyze the provided data and deliver insights about our contracts, invoices, and payment patterns. Please complete the following deliverables:

### 1. Data Exploration (SQL)
Write SQL queries to find the following:
   - Total revenue by month for the past year
   - Contracts with the highest number of invoices
   - Average invoice amount by contract type
   - Invoices that are overdue (past dueDate but not paid)
   - Customers with multiple contracts

### 2. Data Analysis (Python with pandas)
Calculate key metrics:
   - Monthly recurring revenue (MRR) over time
   - Customer churn rate (based on contract terminations)
   - Average days to payment from invoice creation
   - Revenue breakdown by contract type and customer location

### 3. Visualization (Python)
Create visualizations to show:
   - MRR trend over time
   - Distribution of invoice amounts
   - Payment timing analysis
   - Geographical distribution of revenue

### 4. Anomaly Detection
Identify potential anomalies in the invoice data, such as:
   - Unusually high or low invoice amounts
   - Inconsistent payment patterns
   - Contracts with missing invoices (gaps in billing)

### 5. Business Recommendations
Based on your analysis, provide 3-5 actionable recommendations to:
   - Improve revenue collection
   - Reduce customer churn
   - Optimize pricing or contract structures

## Deliverables

Please include the following in your submission:

1. A Jupyter notebook containing your analysis, SQL queries, visualizations, and business recommendations
2. A separate .py file with any utility functions you created
3. A brief summary document (PDF or Markdown) highlighting your key findings and recommendations

## Database Schema

The database follows this schema:

### Customers
- `id` (TEXT): Customer identifier (starts with "cus_")
- `email` (TEXT): Customer email address
- `firstName` (TEXT): Customer first name
- `lastName` (TEXT): Customer last name
- `country` (TEXT): Customer country
- `city` (TEXT): Customer city
- `createdAt` (INTEGER): Unix timestamp of when the customer was created

### Contracts
- `id` (TEXT): Contract identifier (starts with "con_")
- `number` (TEXT): Formatted contract number
- `type` (TEXT): Contract type (Rent, Membership)
- `status` (TEXT): Contract status (Draft, Signed, Activated, Cancelled, etc.)
- `startDate` (INTEGER): Unix timestamp of contract start date
- `endDate` (INTEGER): Unix timestamp of contract end date (can be NULL)
- `terminatedDate` (INTEGER): Unix timestamp of when contract was terminated (if applicable)
- `cancelledDate` (INTEGER): Unix timestamp of when contract was cancelled (if applicable)
- `signedDate` (INTEGER): Unix timestamp of when contract was signed
- `accountId` (TEXT): Foreign key to Customers.id

### ContractItems
- `id` (TEXT): Contract item identifier (starts with "item_")
- `contractId` (TEXT): Foreign key to Contracts.id
- `name` (TEXT): Name of the contract item
- `description` (TEXT): Description of the contract item
- `amount` (REAL): Monetary amount (in the specified currency)
- `type` (TEXT): Type of item (Deposit, Rent, Membership, OneOff, etc.)
- `currency` (TEXT): Currency code (EUR, USD, GBP)
- `timesRedeemed` (INTEGER): Number of times the item has been charged
- `numberOfMonths` (INTEGER): Duration of the item in months (can be NULL)

### Invoices
- `id` (TEXT): Invoice identifier (starts with "inv_")
- `amountDue` (REAL): Total amount due on the invoice
- `amountPaid` (REAL): Amount that has been paid
- `amountRemaining` (REAL): Amount still owed
- `billingMonth` (INTEGER): Month the invoice is for (1-12)
- `billingYear` (INTEGER): Year the invoice is for (e.g., 2023)
- `status` (TEXT): Invoice status (draft, open, paid, void, uncollectible)
- `dueDate` (INTEGER): Unix timestamp of when payment is due
- `paymentDate` (INTEGER): Unix timestamp of when payment was received
- `periodStart` (INTEGER): Unix timestamp of the billing period start
- `periodEnd` (INTEGER): Unix timestamp of the billing period end
- `total` (REAL): Total invoice amount
- `type` (TEXT): Invoice type (subscription, manual, oneoff)
- `stripeId` (TEXT): Stripe invoice ID (starts with "in_")
- `contractId` (TEXT): Foreign key to Contracts.id
- `customerId` (TEXT): Foreign key to Customers.id
- `createdAt` (INTEGER): Unix timestamp of when the invoice was created

### InvoiceLineItems
- `id` (TEXT): Line item identifier (starts with "li_")
- `invoiceId` (TEXT): Foreign key to Invoices.id
- `amount` (REAL): Line item amount
- `currency` (TEXT): Currency code
- `description` (TEXT): Description of the line item
- `periodStart` (INTEGER): Unix timestamp of the billing period start for this line item
- `periodEnd` (INTEGER): Unix timestamp of the billing period end for this line item
- `quantity` (INTEGER): Quantity of the item
- `isProrated` (BOOLEAN): Whether the amount is prorated
- `contractItemId` (TEXT): Foreign key to ContractItems.id

## Evaluation Criteria

Your submission will be evaluated based on:

1. SQL query quality and complexity
2. Python code organization and efficiency
3. Analytical thinking and insight generation
4. Data visualization clarity and effectiveness
5. Quality of business recommendations

## Time Expectation

We expect this exercise to take approximately 3-4 hours to complete. Please feel free to ask any questions if you need clarification.

## Submission Instructions

Please submit your completed analysis in a zip file or as a link to a GitHub repository.

Good luck! 