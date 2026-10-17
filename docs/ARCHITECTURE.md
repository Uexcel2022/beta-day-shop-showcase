# Architecture and design decisions

[Back to README](../README.md)

![System overview](../assets/architecture/system-overview.png)

## Components

| Component | Responsibility | Default local port |
| --- | --- | --- |
| React frontend | Customer storefront, account screens, admin and staff portals | 5173 |
| API Gateway | Explicit public routes, bearer-token validation, role gates, shared request budget and documentation proxy | 8080 |
| Eureka | Service discovery for gateway and service clients | 8761 |
| Identity | Customers/staff/admin, credentials, JWT issuance, current account state, profile pictures and addresses | 8081 |
| Product | Product catalogue, stock/reservations, product pictures and product outbox | 8082 |
| Order | Orders, product snapshots, order bills, cancellations and refund requests | 8083 |
| Payment | Confirmed simulated payment ledger and simulated refund payout | 8084 |
| Shipment | Shipment progression and return receipt/inspection workflows | 8086 |

Identity, Product, Order, Payment and Shipment own separate logical PostgreSQL databases. In the local setup they share one PostgreSQL server, not one shared business schema. Gateway and Eureka have no application database.

## One purchase, end to end

1. The customer signs in through the gateway. Identity issues a JWT; the gateway and downstream services verify credentials and current account permissions.
2. Checkout saves a user-scoped intent and idempotency key before submitting the order. Order uses its product snapshot and coordinates reservation/billing work through protected internal calls.
3. Product records catalogue/stock events in its database outbox. The dispatcher publishes stable events to Kafka; Order applies events using durable receipts to avoid duplicate stock adjustments.
4. The customer submits a simulated payment. Confirmed funds determine shipment eligibility: full prepayment for non-POD items plus the required deposit on eligible POD items.
5. Staff advances shipment. Marking delivered requires verified full payment, including the remaining POD balance.
6. After delivery, an eligible return can be received and approved by staff. Approval drives simulated refund settlement and stock restoration. Non-returnable items are rejected.

## Security boundaries

- Identity is an account service, not the routing gateway. Shared security code is provided by the Common module, and each service still checks its own data access.
- Customer identifiers in URLs do not substitute for ownership. Idempotent replay also runs authorization.
- Admin creates staff; temporary-password sign-in is restricted until replacement. Customer, staff and admin browser sessions are separated by portal/tab scope.
- Internal callbacks and stock/fulfilment operations are not exposed as public gateway routes. Internal credentials are distinct from human JWT credentials.
- The Docker deployment stack keeps backend and infrastructure access on private networks; the native developer setup exposes local diagnostic ports.

## Reliability choices and limits

Flyway versions schema changes; JPA validates the resulting schema. Transactional outboxes retain work after dependency failures. Kafka consumers use durable event receipts; delivery is not described as magical end-to-end exactly-once processing. Resilience4j bounds dependency failures, while uncertain writes recover through saved operations instead of blind HTTP retries.

The gateway enforces a shared human request budget across routed APIs. The present limiter is in memory per process. Multiple replicas require shared enforcement, and public deployment needs its own operational verification.

HTTP request correlation and structured errors support investigation. Kafka/outbox background-event correlation remains future work. See [verification evidence](TESTING.md).
