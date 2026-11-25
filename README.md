# FoodBridge

React/Vite starter for a food-rescue network connecting surplus-food donors (hotels, restaurants, convention halls, caterers and individuals) with receivers (NGOs, ashrams, orphanages and community kitchens).

## Implemented front-end workflows

- Public landing page with separate donor, receiver and administrator entry points.
- Demo donor and receiver registration forms for business / organisation type, city and contact phone.
- Donor workspace: list surplus food with quantity, category, safe collection deadline, notes and a photo-input placeholder.
- Receiver workspace: submit requirements with quantity, unit, meal preference, city and required-by time.
- Illustrative Karnataka receiver directory: Bengaluru, Mysuru and Tumakuru.
- Quantity-aware full-coverage matching: donors choose one of their available meal listings; remaining demand subtracts confirmed meals and reserved allocations; only a listing that covers the remaining meal request can be matched.
- Matched quantities are reserved, not counted as received until an admin confirms delivery. Cancelling an allocation releases the reservation.
- Delivery lifecycle: Available → Assigned → Collected → In transit → Delivered.
- Admin operations dashboard: sample donor activity, receiver fulfilment, aggregate meals and delivery status changes.
- Responsive layout and illustrative route preview with sample coordinates.

## Run locally

Node.js 20+ recommended.

```bash
npm install
npm run dev
```

Build:

```bash
npm run build
npm run preview
```

## Production readiness — important

This is a **front-end prototype, not yet a production-publicable food service**. App data currently lives in React memory and resets on refresh. The role chooser is a demo switch, not authentication. Admin pages are hidden in the UI only and are not access-protected. Sample receiver organisations and verification labels are illustrative and are not claims of verified partnership or endorsement.

Before public launch:

1. Implement real authentication and server-side role-based access control for admin, donor, receiver and delivery partner. Protect every admin API and row; never trust a browser role value.
2. Use a persistent database such as PostgreSQL/Supabase. Store organisations, users, donor profiles, receiver profiles, listings, needs, allocations, delivery events, audit logs and consent.
3. Implement atomic allocation transactions to prevent two donations fulfilling the same remaining request. Match units, food type/diet, geography, pickup capacity and safe collection deadline. Partial fulfillment must be an explicit supported allocation.
4. Store photos in secure object storage (S3-compatible or Supabase Storage) with signed uploads, type/size validation and malware scanning.
5. Integrate a map provider and delivery-partner mobile client for opt-in location tracking. Timestamp updates server-side, restrict location access, provide consent and retention controls. Never label the current preview as live GPS.
6. Add notifications for match, pickup, transit, delay, cancellation and receiver confirmation.
7. Verify partner identity, registration, address and authorised contact. Establish food safety controls for preparation, storage, allergens, time/temperature, expiry, handoff and incident escalation. Obtain qualified food-safety/legal review before operating.
8. Add HTTPS, input validation, rate limiting, secure headers, CSRF/XSS protections, server-side secrets, backups, monitoring, audit trails, privacy policy, terms, consent and grievance contact.
9. Test permissions, matching edge cases, concurrent allocations, accessibility, mobile layouts, security and load.

## Matching example

If a receiver needs 100 meals and 20 are fulfilled, remaining demand is 80. A donor offering 45 meals is not eligible under the current full-coverage rule. A receiver with 30 meals remaining is a candidate. Production can support partial donations only with an explicit allocation record and concurrency-safe transaction.

## Karnataka receiver examples

The directory is seeded for UI demonstration only. Before public listing, independently verify each organisation's legal name, registration, authorised contact, address, beneficiary capacity, food acceptance rules and operating hours. Remove any organisation that has not agreed to participate. Do not imply endorsement from demo inclusion.

## Integrations to add

- `VITE_API_BASE_URL` for the backend.
- Authentication provider and server-side authorisation.
- PostgreSQL API and migrations.
- Object storage for photos.
- Maps provider key restricted by domain and API scope.
- Email/SMS/push credentials stored only server-side.

Never commit credentials, private keys, service-role keys or personal beneficiary data.
