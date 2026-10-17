# Verification evidence

[Back to README](../README.md)

## Recorded application checks

The project's saved CI status records successful runs for **5376bed5e8130698a943c1dfad0d18910f81e516**, completed **13 October 2026**. These are recorded results, not a new live GitHub status check. The linked runs belong to the private source repository and require access.

| Recorded workflow | Result | Evidence |
| --- | --- | --- |
| Maven verification | Success | [Windows/Linux Java 25 and PostgreSQL/Kafka integration](https://github.com/Uexcel2022/beta-day-shop/actions/runs/38446554915) |
| Full-stack browser verification | Success | [Real PostgreSQL, Kafka and application services](https://github.com/Uexcel2022/beta-day-shop/actions/runs/38446554910) |
| Docker deployment verification | Success | [Deployment and operational checks](https://github.com/Uexcel2022/beta-day-shop/actions/runs/38446554859) |

Recorded deployment verification includes **203 frontend tests across 17 files**, TypeScript validation and a production build. The recorded live browser report contains **11 passing checks**, including transaction recovery, mixed-payment checkout, underpaid delivery denial, inspected return/refund, cancellation approval/replay, stock restoration and cross-customer access denial. Browser/CI/deployment guard checks also exercise test isolation and cleanup.

Account/profile/session and staff-first-login behavior have additional frontend and service test coverage. A screenshot of a form is not treated as evidence that its backend workflow passed.

## What this packaging session checked

- Captured 14 frontend views from the real built application using synthetic, read-only presentation data.
- Captured generated Swagger UI for the five business APIs from the local gateway.
- Temporarily started all seven Java apps; authenticated readiness passed for the gateway and five APIs, and all five gateway documentation routes returned HTTP 200.
- Created code pictures directly from selected source lines at the documented source snapshot.
- Reviewed representative desktop, mobile, API, code and architecture images.
- Checked local document/image links and the publication file list; excluded runtime credentials, private data, logs and full application source.

The full Maven/frontend/live transaction suites were not rerun solely to create this showcase. No load-test capacity, public availability or production security certification is claimed. Simulated payment outcomes do not validate real payment-provider integration.

## Reproducing with authorized source access

The private repository contains its Maven reactor, frontend test commands, PostgreSQL/Kafka integration jobs, isolated browser harness and CI workflow definitions. Use its documented environment and disposable test infrastructure. The public presentation repository deliberately has no runnable application or credentials.
