# Requirements — Hotel Booking Platform

## 1. Introduction

The Kojenwerk platform lets guests find available rooms, pay for bookings, and manage their reservations. Hotel owners can manage their accommodation and deal with guest-related matters. These requirements are based on the stakeholder decisions in [decision-log.md](decision-log.md).

## 2. Stakeholders and actors

- **Guest:** registers, searches for rooms, books, modifies or cancels a reservation, and can submit complaints or reports.
- **Hotel Owner:** maintains room information and prices, handles eligible cancellations and responds to complaints.
- **Payment Provider:** handles card and PayPal payments, including payment adjustments and refunds where needed.
- **CEO:** business stakeholder who defines the booking and platform rules.

For the three detailed scenarios, see [use-cases.md](use-cases.md). The three described use cases are **UC-01 Book a Room**, **UC-02 Modify a Booking** and **UC-03 Cancel a Booking**.

## 3. Functional requirements

Acceptance criteria use **Given / When / Then**. Negative cases are included to make it clear when an action must be rejected or handled differently.

| ID | Requirement | Source | Acceptance criteria |
|---|---|---|---|
| FR-01 | The platform shall require registration before a guest can book. | D-05 | **Given** a registered guest, **when** they start a booking, **then** they can proceed. **Negative:** Given an unregistered visitor, when they try to book, then registration is required before any booking can be created. |
| FR-02 | Registration shall require a first name, last name and email address. | D-06 | **Given** all required details, **when** registration is submitted, **then** it is accepted. **Negative:** If one is missing, registration is rejected and the missing field is shown. |
| FR-03 | Providing a phone number shall be optional. | D-06 | **Given** the required details are valid but no phone number is entered, **when** registration is submitted, **then** it succeeds. **Negative:** A missing phone number alone must not cause an error. |
| FR-04 | Birthday information shall only be collected with explicit consent. | D-07 | **Given** explicit consent, **when** a birthday is supplied, **then** it may be recorded. **Negative:** Without consent, no birthday is collected and registration can still proceed. |
| FR-05 | Guests shall be able to search available rooms by destination, dates and number of guests. | UC-01; D-01 | **Given** matching available rooms, **when** a search is made, **then** they are shown. **Negative:** If none match, the search reports no matching rooms. |
| FR-06 | Room searches shall include a wheelchair-accessibility filter. | D-09 | **Given** a suitable accessible room, **when** the filter is selected, **then** it appears in the results. **Negative:** Rooms not meeting the filter are excluded. |
| FR-07 | All displayed prices shall include applicable taxes. | D-17 | **Given** a taxable room price, **when** a total is displayed, **then** taxes are included. **Negative:** A price excluding applicable taxes must not be shown as the final payable amount. |
| FR-08 | Pressing **Pay** for an available room shall start a temporary hold lasting 30 minutes. | D-21 | **Given** an available room, **when** the guest presses Pay, **then** a 30-minute hold is created. **Negative:** If the room is not available, no new hold is granted. |
| FR-09 | A booking shall be confirmed immediately after successful payment while the room hold is valid, without owner approval. | D-02; D-04; D-21 | **Given** a valid hold and successful payment, **when** the payment result is received, **then** the booking is confirmed. **Negative:** Failed payment or an expired hold must not result in confirmation. |
| FR-10 | Entered booking details shall be retained for 30 minutes after a payment failure. | D-27 | **Given** a failed payment, **when** the guest retries within 30 minutes, **then** the previously entered details are available. **Negative:** After that period, the system is not required to retain them. |
| FR-11 | Guests shall be able to change booking dates or room type until 48 hours before check-in, subject to availability and the current price. | D-12; D-13 | **Given** a request 72 hours before check-in and an available replacement, **when** the guest accepts the current price, **then** the change is saved. **Negative:** A date or room-type change requested 24 hours before check-in is not accepted; the original booking remains. |
| FR-12 | Guests shall be able to cancel their own confirmed bookings. | D-08 | **Given** a guest's confirmed booking, **when** they confirm cancellation, **then** its status changes to cancelled. **Negative:** A guest cannot cancel another guest's booking. |
| FR-13 | Hotel owners shall be able to change the current selling prices of rooms they manage. | D-03 | **Given** an owner manages a room, **when** they save a new valid price, **then** the room's current price changes. **Negative:** An owner cannot edit a room belonging to another owner. |
| FR-14 | Guests shall be able to apply promotional codes during booking. | D-23 | **Given** a valid code, **when** it is applied, **then** the correct discount is included in the price. **Negative:** Invalid or expired codes do not change the price. |
| FR-15 | Guests shall be able to submit complaints through the portal. | D-24 | **Given** a completed complaint, **when** a guest submits it, **then** it is recorded. **Negative:** An incomplete complaint is not accepted and missing information is identified. |
| FR-16 | Hotel owners shall be able to submit a response to a complaint within 14 days. | D-24 | **Given** a complaint submitted 10 days earlier, **when** the owner responds, **then** the response is recorded within the deadline. **Negative:** A response submitted after day 14 is recorded as late, not as an on-time reply. |
| FR-17 | Guests shall be able to submit discrimination reports. | D-28 | **Given** a completed report, **when** it is submitted, **then** it is recorded. **Negative:** If required information is missing, the system asks for it instead of accepting an incomplete report. |
| FR-18 | Guests shall be informed if a booking cannot be completed due to a system or processing failure. | D-16 | **Given** a booking failure, **when** the failure is detected, **then** the guest is told the booking was not completed. **Negative:** If payment success has not been verified, the system must not show a confirmed booking. |
| FR-19 | The system shall calculate guest cancellation refunds using the 48-hour rule. | D-08; D-20 | **Given** cancellation 72 hours before arrival, **when** the refund is calculated, **then** it equals the full payment. **Negative:** For cancellation 24 hours before arrival, the first night's charge is retained and only the remaining amount, if any, is refundable. |
| FR-20 | A confirmed booking shall keep its agreed price when the owner later changes room prices. | D-03 | **Given** a confirmed booking, **when** the room's current price changes, **then** the booking price is unchanged. **Negative:** The updated room price must not replace the price already agreed for that booking. |
| FR-21 | Hotel owners shall be allowed to cancel directly only at least 14 days before arrival and with a valid reason. | D-11 | **Given** a valid reason 15 days before arrival, **when** the owner cancels, **then** the cancellation is allowed. **Negative:** If fewer than 14 days remain, direct cancellation is blocked and the owner is told to contact support. |
| FR-22 | Booking payment shall support card and PayPal, but not payment at the hotel. | D-04 | **Given** a successful card or PayPal payment, **when** the result is received, **then** it can complete the booking. **Negative:** Paying at the hotel is not offered as a way to confirm a booking. |
| FR-23 | A billing address shall be requested only when a guest asks for an invoice. | D-06 | **Given** an invoice request, **when** invoice details are collected, **then** a billing address may be requested. **Negative:** Without an invoice request, no billing address is required. |
| FR-24 | Marketing emails shall be sent only to guests who have explicitly agreed to receive them. | D-07 | **Given** recorded marketing consent, **when** a marketing email is prepared, **then** sending is allowed. **Negative:** Without consent, the email is not sent. |
| FR-25 | A room hold shall be released after 30 minutes if payment has not succeeded. | D-22 | **Given** an unpaid hold, **when** 30 minutes have passed, **then** the room becomes available to other guests. **Negative:** A hold that is still valid must not be released early just because another guest requests the room. |
| FR-26 | The system shall prevent overlapping confirmed bookings for the same room. | D-01; D-26 | **Given** a room with an existing confirmed booking, **when** another guest requests overlapping dates, **then** the second booking is refused. **Negative:** Competing requests must not both produce overlapping confirmed bookings. |
| FR-27 | Eligible owner-initiated cancellations shall give the guest a full refund. | D-11 | **Given** a valid owner cancellation, **when** it is processed, **then** a refund for the full amount is requested through the payment provider. **Negative:** The guest must not be charged a cancellation fee for that owner cancellation. |
| FR-28 | The guest shall be informed automatically when an owner cancels their booking. | D-11 | **Given** an eligible owner cancellation, **when** it is recorded, **then** the guest receives an automatic notification. **Negative:** The system must not leave the guest uninformed while treating the booking as cancelled. |
| FR-29 | Registration and booking shall not request nationality or copies of identity documents. | D-06 | **Given** a guest registers or books, **when** personal details are requested, **then** nationality and ID copies are not requested. **Negative:** Missing nationality or ID copies must never block registration or booking. |
| FR-30 | Guests shall be able to request a payment-method change under the same booking-change deadline. | D-12; D-13 | **Given** a change request at least 48 hours before check-in, **when** the guest selects another supported payment method, **then** the request may proceed under the modification rules. **Negative:** Given a request less than 48 hours before check-in, when the guest requests the change, then it is rejected and the existing booking is preserved. |

**Open detail:** D-12/D-13 confirm that payment-method changes are subject to the same rules, but do not describe exactly how an already-paid booking is adjusted. The original notes also mentioned changing the guest count; this still needs confirmation. For FR-16, recording a reply as late is a proposed way to check the 14-day deadline; the stakeholders did not decide on a penalty or escalation process.

## 4. Non-functional requirements

| ID | Category | Requirement | Metric | Target | Verification | Source |
|---|---|---|---|---|---|---|
| NFR-01 | Availability | The platform shall meet the agreed monthly uptime and maintenance rules. | Monthly availability; maintenance times | At least 99.5% per month; planned maintenance only Tuesday 02:00–04:00 | Uptime monitoring and maintenance logs | D-14; D-15 |
| NFR-02 | Performance | Search results shall load within the agreed time target. | Percentage of searches loaded within 1 second | At least 90% | Performance tests of searches | Lab 1 requirement; confirm the original decision source |
| NFR-03 | Capacity and scalability | The platform shall support peak usage and the expected user growth. | Concurrent users; total users | 3,000 concurrent users; about 3,000 users currently, increasing to about 10,000 in 1–2 years | Load test for 3,000 concurrent users; capacity check for 10,000 users | D-18; D-19 |
| NFR-04 | Accessibility | The platform shall support assistive technologies and keyboard use. | Accessibility compliance | WCAG 2.1 AA | Accessibility audit, keyboard tests, screen-reader tests | D-10 |
| NFR-05 | Privacy and retention | Accounts without bookings shall be deleted after 2 years; booked guests' personal data shall be retained for 3 years. | Age and booking history of stored records | 2 years without booking; 3 years for booked guests | Check retention rules against both account categories | D-29 |
| NFR-06 | Fairness | When guests compete for a room, requests shall be prioritized by the order received by the platform. | Order of requests | First received has priority | Concurrent request tests using server timestamps | D-26 |
| NFR-07 | Data protection | Personal data shall only be accessible to authorized users for authorized purposes. | Unauthorized access in test cases | No successful unauthorized access | Access-control and security tests | Lab 1 privacy requirement; confirm the original decision source |

NFR-05 states the agreed retention periods; the event from which each period starts still needs clarification. The treatment of planned maintenance when calculating NFR-01's uptime is also not explicit in the decision log.

## 5. Traceability

The direction in this table is **UC → FR**: it shows which requirements appear in each documented use case. Looking at the same mapping from **FR → UC** also identifies which requirements still have no detailed scenario. Registration requirements are listed separately as prerequisites, not as steps performed inside a booking.

| Use case | FR-01 | FR-02 | FR-03 | FR-04 | FR-05 | FR-06 | FR-07 | FR-08 | FR-09 | FR-10 | FR-11 | FR-12 | FR-13 | FR-14 | FR-15 | FR-16 | FR-17 | FR-18 | FR-19 | FR-20 | FR-21 | FR-22 | FR-23 | FR-24 | FR-25 | FR-26 | FR-27 | FR-28 | FR-29 | FR-30 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| UC-01 — Book a Room |  |  |  |  | X | X | X | X | X | X |  |  |  | X |  |  |  | X |  | X |  | X | X |  | X | X |  |  | X |  |
| UC-02 — Modify a Booking |  |  |  |  |  |  | X |  |  |  | X |  |  |  |  |  |  |  |  | X |  |  |  |  |  | X |  |  |  | X |
| UC-03 — Cancel a Booking |  |  |  |  |  |  |  |  |  |  |  | X |  |  |  |  |  |  | X |  | X |  |  |  |  |  | X | X |  |  |
| Registration prerequisite to UC-01 | X | X | X | X |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Owner room-price management (diagram only) |  |  |  |  |  |  |  |  |  |  |  |  | X |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

The remaining uncovered requirements in the three written scenarios are **FR-15, FR-16, FR-17 and FR-24**. Complaint handling, discrimination reports and marketing consent need separate use-case coverage if required by the final scope. The owner availability-management use case and guest reviews should also be checked against the agreed scope; we have not treated them as covered just because they appear in general descriptions.

### Corrections and outstanding gaps

| Item | Status |
|---|---|
| Old decision numbers attached to functional requirements | Corrected using D-01–D-29. |
| FR-06 and FR-12 wrongly linked to UC-02 | Corrected. Accessibility search belongs to UC-01; cancellation belongs to UC-03. |
| Gap notes describing FR-14 as accessibility and FR-18 as price protection | Corrected. These are FR-06 and FR-20, respectively. |
| Two behaviors combined in the old FR-12 and FR-13 | Split into FR-12/FR-19 (cancel/refund) and FR-13/FR-20 (price change/price protection). |
| Hold expiry and prevention of double-booking | Made explicit as FR-25 and FR-26. |
| Owner cancellation obligations and invoice/privacy rules | Separate requirements added as FR-27–FR-29. |
| Payment-method changes | Covered by FR-30; the exact payment adjustment procedure still needs clarification. |
| Complaints, discrimination, marketing, reviews and owner availability management | Not covered by the three detailed use cases; additional scope work is still required. |

## 6. Related files

- [Decision log](decision-log.md)
- [Use cases](use-cases.md)
