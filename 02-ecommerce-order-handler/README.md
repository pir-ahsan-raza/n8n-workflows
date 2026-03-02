# 🛒 E-commerce Order Handler — Loyalty Email Automation

When a new order comes in, this workflow automatically checks the customer's history and sends a personalized email based on their loyalty tier. No more same email for every customer.

---

## 🖼️ How it looks

![Workflow](workflow-prev.png)

---

## 🔀 What It Does

```
New Order (Webhook)
    → Fetch Customer Data (HTTP Request → dummyjson / Shopify API)
    → Calculate Loyalty Tier (Code Node)
    → Is VIP?
        ✅ true  → VIP Email (20% discount)
        ❌ false → Is Returning?
                      ✅ true  → Returning Email (10% discount)
                      ❌ false → First Timer Email (5% discount)
```

| Tier | Condition | Discount Code |
|---|---|---|
| First Timer | 1st order | `WELCOME5` |
| Returning | 2–4 orders | `RETURN10` |
| VIP | 5+ orders | `VIP20` |

---

## 🛠️ Setup

**1. Import** `workflow.json` into n8n

**2. Connect Gmail** on all 3 email nodes (same Google account)

**3. Activate** the workflow — copy the production webhook URL

**4. Point your store** to POST orders to that webhook URL

---

## 📋 Expected Payload

```json
{
  "userId": "12345",
  "orderId": "ORD-001",
  "product": "Wireless Headphones",
  "amount": 89.99
}
```

> In production, replace the dummyjson API call in the HTTP Request node with your actual Shopify/WooCommerce customer endpoint.
