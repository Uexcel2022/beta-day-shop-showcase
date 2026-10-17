# Presenting the local demo

[Back to README](../README.md)

## For a visitor to this showcase

Browse the README, [visual gallery](SCREENSHOT-GALLERY.md), [Swagger pictures](API-OVERVIEW.md), and [code highlights](CODE-HIGHLIGHTS.md). Downloading this repository lets you view the images and documents offline. It does not install or run the application.

For a guided demonstration or an authorized source review, contact [the project owner](https://github.com/Uexcel2022). The [application repository](https://github.com/Uexcel2022/beta-day-shop) is private; a public visitor may see a 404.

## For the presenter with source access

Use the private repository's README and docs/DEMO.md as the authoritative setup instructions. The local toolchain is JDK 25, Maven, Docker Desktop, and Node 24.15+ with the pinned pnpm 11.25.0. The normal local stack runs PostgreSQL, Kafka, Eureka, the gateway, five business APIs and the frontend.

From the private checkout, the existing demo setup is:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File ./scripts/initialize-demo.ps1
```

Demo initialization configures/restarts the local services, creates private demo actors, and stores generated credentials/checkpoints in the ignored .local/demo directory. Keep those files in the source checkout. Follow the private frontend README to run its dev server, and sign in using the generated local credentials. Do not publish credentials or an authenticated browser session.

The private scripts/run-demo.ps1 supplies an automated walkthrough. Retain its checkpoints and follow its recovery instructions after interruption rather than repeatedly creating new orders.

## Suggested 8–10 minute walkthrough

1. **Storefront:** browse/filter products, open a product and adjust shopping-bag quantities.
2. **Customer account:** show the cropped profile picture, saved addresses, and login surviving refresh.
3. **Mixed checkout:** choose prepaid and eligible POD products. Explain the full prepaid cost plus the POD deposit before shipment.
4. **Payment and shipment:** submit a simulated payment and show tracking. In a staff session, demonstrate that underpayment blocks delivery; settle the balance before marking delivered.
5. **Return/refund:** request an eligible return; show staff receiving and approving inspection, then the simulated refund and restored quantity. Show that a non-returnable item cannot enter that process.
6. **Roles and data access:** show admin staff management and staff's restricted workflow. Explain/test with the documented second customer that another customer's order/bill data is denied.
7. **Engineering:** open local Swagger, the architecture diagram, code highlights and recorded CI evidence.

Default local URLs: storefront http://localhost:5173, gateway Swagger http://localhost:8080/swagger-ui/index.html, Eureka http://localhost:8761. These addresses work only on the computer running the application.

Stop the local stack using the private scripts/stop-local.ps1 instructions when finished. No cloud account, paid hosting or real payment provider is required for this presentation.
