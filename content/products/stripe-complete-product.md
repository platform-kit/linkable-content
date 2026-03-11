---
name: "Pro SaaS Subscription"
description: "A full-featured SaaS product with monthly and annual plans, metered usage, and variants."
images:
  - "/uploads/saas-main.png"
  - "/uploads/saas-variant1.png"
shippable: false
attributes:
  - name: "Plan"
    values: ["Basic", "Pro", "Enterprise"]
  - name: "Region"
    values: ["US", "EU", "APAC"]
variants:
  - sku: "pro-us"
    attributes: { Plan: "Pro", Region: "US" }
    inventory: 1000
  - sku: "ent-eu"
    attributes: { Plan: "Enterprise", Region: "EU" }
    inventory: 100
metadata:
  category: "SaaS"
  feature: "Metered, Subscription"
prices:
  - currency: "usd"
    unit_amount: 5000
    active: true
    type: "recurring"
    recurring:
      interval: "month"
      interval_count: 1
      usage_type_metered: false
      trial_period_days: 14
    metadata:
      plan: "Pro"
  - currency: "usd"
    unit_amount: 12000
    active: true
    type: "recurring"
    recurring:
      interval: "year"
      interval_count: 1
      usage_type_metered: false
      trial_period_days: 30
    metadata:
      plan: "Pro"
  - currency: "usd"
    unit_amount: 0
    active: true
    type: "recurring"
    recurring:
      interval: "month"
      interval_count: 1
      usage_type_metered: true
      trial_period_days: 0
    tiers:
      - up_to: 1000
        unit_amount: 0
      - up_to: 10000
        unit_amount: 10
      - up_to: null
        unit_amount: 5
    metadata:
      plan: "Enterprise"
stripe_product_id: "prod_stripecomplete123"
extra:
  statement_descriptor: "PRO SAAS SUBSCRIPTION"
  tax_code: "txcd_10000000"
---

A Stripe-complete SaaS product with multiple plans, metered usage, and variants. All Stripe product and price fields are represented.