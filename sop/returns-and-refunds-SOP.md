# SOP: Handling Order Status, Return and Refund Requests

**Owner:** ThinkCart Customer Operations
**Applies to:** Order Ops team (human or AI agent)
**Version:** 1.0 — October 2026

## Purpose
Resolve customer requests about order status, cancellations, returns and refunds quickly, accurately and according to store policy.

## Inputs
- Customer message
- Order ID (format: `TC` followed by 5 digits, e.g. TC10234)
- Customer email on the order
- Order record from the Orders system (fields: order_id, customer_name, customer_email, product, sku, category, amount_inr, payment_method, order_date, status, delivered_date, courier, tracking_id)

## Procedure

### Step 1 — Identify the order
1. If the customer has not provided an order ID, ask for it. Do not guess.
2. Look up the order in the Orders system.
3. If no order is found, ask the customer to re-check the ID. After 2 failed attempts, hand off to a human.
4. **Verify identity**: the email the customer provides must match `customer_email` on the order. If it does not match, do not share any order details.

### Step 2 — Order status requests
1. Share the current `status`, courier and tracking ID.
2. If status is **Delayed**, apologise and give the latest information.
3. If the order is more than 5 days past the promised delivery date, offer: (a) full refund, or (b) ₹100 store credit and continued delivery.

### Step 3 — Cancellation requests
1. If status is **Placed** or **Packed** → cancel the order, confirm refund timeline (3–5 business days for prepaid; nothing to refund for COD).
2. If status is **Shipped** / **Out for delivery** → explain it can't be cancelled; customer can refuse delivery or return after delivery.

### Step 4 — Return requests
Check ALL of these, in order:
1. Status must be **Delivered**. Otherwise explain why a return isn't possible yet.
2. Today's date must be within **7 days of `delivered_date`**.
   - Exception: damaged/wrong item reported within 48 hours → always eligible (photo required).
3. Item category must be returnable. **Not returnable**: innerwear (AP-303), gift cards (GC-401), personal care with broken seal (PC-501), Final Sale items.
4. If all checks pass → create a return request and tell the customer pickup will be scheduled within 2 business days.
5. If any check fails → politely explain which rule applies. Do not make exceptions; offer a human handoff if the customer insists.

### Step 5 — Refund decision
| Condition | Action |
|-----------|--------|
| Refund amount **≤ ₹2,000** | Approve automatically |
| Refund amount **> ₹2,000** | **Send to human approval** before confirming to the customer. Tell the customer: "Your refund request has been submitted for approval; you'll hear from us within 24 hours." |
| Damaged/wrong item | Full refund including any shipping/pickup fees |
| Order < ₹499 (not damaged) | Deduct ₹49 pickup fee |
| COD order | Refund via secure refund link to bank/UPI, or instant store credit |

### Step 6 — Close the request
1. Summarise what was done in one or two sentences.
2. Record: order_id, request_type, decision, refund_amount, needs_approval (yes/no).

## Escalate to a human immediately if
- Customer is abusive, very angry, or mentions legal action, consumer court or social media complaints
- Suspected fraud (e.g. multiple returns, email mismatch with pressure to share details)
- Any request outside this SOP

## Never
- Ask for card number, CVV, OTP, UPI PIN or passwords
- Promise refunds before the checks in Step 4 and approval in Step 5
- Share one customer's order details with another person
