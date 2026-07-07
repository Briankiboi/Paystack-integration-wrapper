# PyPaystack

A lightweight, developer-friendly Python wrapper for the Paystack API.

PyPaystack makes it easier to integrate Paystack payments into Python applications with a simple and intuitive interface for transactions, customers, and subscription plans.

---

## Features

- Charge customers using authorization codes
- Verify transactions
- Create and manage customers
- Create and manage subscription plans
- Retrieve a single transaction or all transactions
- Retrieve a single customer or all customers
- Use environment variables for secure API key management
- Simple, Pythonic interface

---

## Installation

Install the latest version from PyPI:

```bash
pip install -U pypaystack
```

---

## Authentication

Generate your **Secret Key** from your Paystack Dashboard.

You can authenticate in two ways:

### Option 1: Environment variable

Recommended for local development and production.

```bash
export PAYSTACK_AUTHORIZATION_KEY=sk_test_xxxxxxxxxxxxxxxxx
```

On Windows PowerShell:

```powershell
set PAYSTACK_AUTHORIZATION_KEY=sk_test_xxxxxxxxxxxxxxxxx
```

Then instantiate the classes without passing the key manually.

### Option 2: Pass the key directly

```python
from pypaystack import Transaction

transaction = Transaction(
    authorization_key="sk_test_xxxxxxxxxxxxxxxxx"
)
```

---

## Usage

### Transactions

```python
from pypaystack import Transaction

transaction = Transaction(
    authorization_key="sk_test_xxxxxxxxxxxxxxxxx"
)

# Charge a customer
response = transaction.charge(
    "customer@example.com",
    "AUTH_xxxxxxxxx",
    10000
)

# Verify a transaction
response = transaction.verify("reference_code")
```

### Customers

```python
from pypaystack import Customer

customer = Customer()

# Create customer
response = customer.create(
    email="customer@example.com",
    firstname="John",
    lastname="Doe",
    phone="080123456789"
)

# Get one customer
response = customer.getone("CUS_xxxxxxxx")

# Get all customers
response = customer.getall()
```

### Subscription Plans

```python
from pypaystack import Plan

plan = Plan()

# Create a plan
response = plan.create(
    "Weekly Plan",
    150000,
    "Weekly"
)

# Get one plan
response = plan.getone(240)

# Get all plans
response = plan.getall()
```

---

## Response Format

Every API call returns a tuple in this format:

```python
(
    status_code,
    status,
    message,
    data
)
```

Example:

```python
status_code, status, message, data = transaction.verify(reference)

if status:
    print("Payment successful!")
    print(data)
else:
    print(message)
```

---

## Supported Operations

### Transactions

- Charge customer
- Verify transaction
- Retrieve transaction
- Retrieve all transactions

### Customers

- Create customer
- Retrieve customer
- Retrieve all customers

### Plans

- Create plan
- Retrieve plan
- Retrieve all plans

---

## Security

Never commit your Paystack Secret Key to source control.

Use environment variables or a secrets manager instead.

```bash
PAYSTACK_AUTHORIZATION_KEY=sk_live_xxxxxxxxxxxxxxxxx
```

---

## Requirements

- Python 3.8+
- Paystack account
- Paystack Secret Key

---

## Roadmap

Planned future support may include:

- Transaction initialization
- Refunds
- Transfers
- Transfer recipients
- Dedicated virtual accounts
- Webhook verification
- Settlements
- Subscriptions
- Bulk charges
- Payment pages
- Apple Pay
- Terminal API
- Async support
- Type hints
- Improved error handling

---

## Contributing

Contributions are welcome.

Feel free to submit issues, feature requests, or pull requests to help improve PyPaystack.

---

## License

MIT License

---

## Paystack Documentation

Official API documentation:

[Paystack API Docs](https://paystack.com/docs/api)

---

Made with ❤️ for Python developers using Paystack.
