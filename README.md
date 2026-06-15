# 📦 Greenweez Quality Products Analysis

> **Goal:** Curate a selective catalog that's relied upon — by identifying refund patterns and understanding what drives product returns.

![Dashboard Preview](Greenweez%20Quality%20Products.png)

---

## 🧩 Project Overview

Greenweez's quality team needed to understand why customers return products. This project analyzes sales and refund data to identify the most common return reasons, measure their financial impact, and help the team make better catalog decisions.

---

## 📁 Data Sources

Two raw datasets were imported into Google Sheets using `IMPORTRANGE()`:

| Sheet | Contents |
|---|---|
| **Sales** | `date_date`, `orders_id`, `products_id`, `promo_name`, `code`, `turnover_before_promo`, `turnover`, `qty` |
| **Refund_reason** | `year`, `month`, `day`, `orders_id`, `ref_turnover`, `ref_ship`, `ref_coupon`, `ref_reason` |

---

## 🔧 Data Preparation & Enrichment

In the **Explo_refund_reason** sheet, refund data was enriched with:

- `turnover_per_order` — total revenue per order pulled from Sales sheet using `SUMIF(Sales!B:B, D2, Sales!G:G)`

This cross-sheet lookup connects each refund record to its original order value, enabling financial impact analysis per return reason.

---

## 📊 Analysis

### Global Quality Vision (Pivot Table)
Refund data was summarized by `ref_reason` with:

| Metric | Description |
|---|---|
| SUM of ref_turnover | Total refunded revenue per reason |
| SUM of ref_ship | Total refunded shipping per reason |
| SUM of ref_coupon | Total refunded coupon value per reason |
| Weight of Refund | Each reason's share of total refund value |

### Refund Breakdown
Total of **686 refund transactions** analyzed:

| Reason | Count | Share |
|---|---|---|
| Return | 351 | 51.2% |
| Damage | 175 | 25.5% |
| Wrong product | 160 | 23.3% |

### Financial Impact by Reason

| Reason | Refunded Revenue | Refunded Shipping | Refunded Coupon |
|---|---|---|---|
| Damage | £731.06 | £37.16 | £75.00 |
| Return | £1,648.94 | £332.22 | £966.12 |
| Wrong product | £695.85 | £75.31 | £110.00 |
| **Grand Total** | **£3,075.85** | **£444.69** | **£1,151.12** |

Weight of Refund: **65.84%** of refund value comes from turnover, **9.52%** from shipping, **24.64%** from coupons.

---

## 💡 Key Findings

- **Returns dominate** — over half of all refunds (51.2%) are simple returns, suggesting potential issues with product descriptions or customer expectations
- **Damage accounts for 25.5%** — points to logistics or packaging quality issues
- **Wrong product at 23.3%** — indicates fulfillment or catalog accuracy problems
- **Coupon refunds are disproportionately high** — £1,151 refunded in coupons vs £444 in shipping, meaning promotions are tied to a large share of returned orders

---

## 🛠️ Tools & Functions Used

| Function/Technique | Usage |
|---|---|
| `IMPORTRANGE()` | Import Sales and Refund data from external Google Sheets |
| `SUMIF()` | Calculate total turnover per order by matching orders_id across sheets |
| Pivot Table | Summarize refund reasons with SUM and custom Weight of Refund metric |
| Pie Chart | Visualize distribution of refund reasons (Return / Damage / Wrong product) |

---

