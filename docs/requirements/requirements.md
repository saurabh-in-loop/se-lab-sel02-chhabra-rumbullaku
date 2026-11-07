# Requirements — Hotel Booking Platform

## 1. Introduction

The purpose of this document is to define the requirements for the Kojenwerk hotel booking platform. The platform allows guests to search for available accommodation, book rooms, manage their bookings and make payments online. It also provides hotel owners with functions to manage room prices and respond to guest-related matters. This document describes the functional and non-functional requirements agreed upon during the stakeholder session.

## 2. Stakeholders and users

The main users of the platform are guests and hotel owners. Guests can register, search for rooms, make payments, book accommodation, modify or cancel bookings, submit complaints and write reviews. Hotel owners can manage room prices, respond to complaints and manage their accommodation information. The CEO represents the business stakeholder and defines the platform's policies, including booking, payment, cancellation, accessibility and availability requirements. The platform also interacts with external payment services.

## 3. Use cases

See [use cases](use-cases.md) and the [decision log](decision-log.md).

## 4. Functional requirements

<!--
Atomic · unambiguous · free of design decisions · traceable · verifiable.
Every FR: at least one acceptance criterion (Given / When / Then), at least one NOT the happy path.
-->

Each functional requirement describes one specific system capability. The acceptance criteria use Given/When/Then scenarios to verify the expected behaviour, including situations where the operation cannot be completed.

| ID | Requirement | Source | Acceptance criteria |
|---|---|---|---|
| FR-01 | The system shall require guests to register before making a booking. | Stakeholder Session 1 – CEO, mandatory registration (D-01). | **AC-01:** Given a user is not registered, when they attempt to book a room, then the system shall require them to register. **Negative:** Given a user has not completed registration, when they attempt to proceed with booking, then the system shall not create a booking. |
| FR-02 | The system shall require a guest's first name, last name and email address during registration. | Stakeholder Session 1 – CEO, required guest data (D-02). | **AC-02:** Given a guest completes registration, when they submit all required details, then the system shall accept the registration. **Negative:** Given one of the required fields is missing, when the guest submits the form, then the system shall display a validation message and reject the incomplete submission. |
| FR-03 | The system shall allow guests to provide a phone number as an optional registration detail. | Stakeholder Session 1 – CEO, optional phone number (D-02). | **AC-03:** Given a guest is registering, when they submit the form without a phone number, then the system shall allow registration if all mandatory fields are valid. |
| FR-04 | The system shall request explicit consent before collecting or using a guest's birthday. | Stakeholder Session 1 – CEO, explicit birthday consent (D-02). | **AC-04:** Given a guest is asked to provide their birthday, when they give explicit consent, then the system may collect the birthday. **Negative:** Given the guest does not give consent, when they complete registration, then the system shall not require or collect the birthday. |
| FR-05 | The system shall allow guests to search for rooms using accommodation search criteria and display matching available rooms. | Stakeholder Session 1 – CEO, guaranteed bookings and accessibility filters (D-03, D-08). | **AC-05:** Given rooms match the guest's search criteria and are available, when the guest searches, then the system shall display matching rooms. **Negative:** Given no available rooms match the criteria, when the guest searches, then the system shall inform the guest that no matching rooms are available. |
| FR-06 | The system shall provide wheelchair-accessibility filters for room searches. | Stakeholder Session 1 – CEO, accessibility filters (D-08). | **AC-06:** Given a guest selects a wheelchair-accessibility filter, when they perform a search, then the system shall display rooms matching that accessibility filter. **Negative:** Given no matching accessible rooms are available, when the search is performed, then the system shall indicate that no matching rooms were found. |
| FR-07 | The system shall display accommodation prices including applicable taxes. | Stakeholder Session 1 – CEO, prices including taxes (D-09). | **AC-07:** Given a guest views a room or booking price, when the price is displayed, then it shall include applicable taxes. |
| FR-08 | The system shall hold a selected room for 30 minutes when the guest initiates payment by pressing the payment button. | Stakeholder Session 1 – CEO, temporary room hold (D-10). | **AC-08:** Given a guest selects an available room and presses the payment button, when the payment process starts, then the system shall hold the room for 30 minutes. **Negative:** Given the 30-minute hold expires without successful payment, when the hold expires, then the system shall release the room for other guests to book. |
| FR-09 | The system shall confirm a booking immediately after successful payment. | Stakeholder Session 1 – CEO, instant confirmation after payment and no owner approval (D-04). | **AC-09:** Given a guest has a valid room hold, when the payment is successful, then the system shall confirm the booking and inform the guest. **Negative:** Given the payment fails, when the payment provider reports failure, then the system shall not confirm the booking. |
| FR-10 | The system shall retain the guest's entered booking information for up to 30 minutes after a payment failure so that the guest does not need to enter it again. | Stakeholder Session 1 – CEO, saved data after payment failure (D-10). | **AC-10:** Given a guest's payment fails during the 30-minute hold, when the guest retries payment within that period, then the system shall retain the previously entered information. **Negative:** Given the 30-minute period has expired, when the guest returns to the payment process, then the system shall not treat the previous room hold as active. |
| FR-11 | The system shall allow guests to modify an existing booking, subject to the applicable cancellation rules. | Stakeholder Session 1 – CEO, booking changes (D-11). | **AC-11:** Given a guest has an existing booking, when they request an allowed change to the number of guests, payment method or dates, then the system shall process the change according to the applicable booking and cancellation rules. **Negative:** Given a requested change cannot be accepted under those rules, when the guest submits it, then the system shall inform the guest and leave the booking unchanged. |
| FR-12 | The system shall allow guests to cancel a booking and apply the cancellation charges according to the 48-hour cancellation policy. | Stakeholder Session 1 – CEO, cancellation policy (D-05). | **AC-12:** Given a guest cancels at least 48 hours before arrival, when the cancellation is processed, then the system shall provide a full refund. **Negative:** Given a guest cancels less than 48 hours before arrival, when the cancellation is processed, then the system shall charge the first night's cost. |
| FR-13 | The system shall allow hotel owners to change room prices without changing the agreed price of bookings that have already been confirmed. | Stakeholder Session 1 – CEO, price changes (D-06). | **AC-13:** Given a guest has a confirmed booking, when the owner changes the room price, then the guest's confirmed booking price shall remain unchanged. |
| FR-14 | The system shall allow guests to apply promotional codes during the booking process. | Stakeholder Session 1 – CEO, promotional codes (D-12). | **AC-14:** Given a guest enters a valid promotional code, when the code is applied, then the system shall apply the promotion according to its conditions. **Negative:** Given a promotional code is invalid or expired, when the guest applies it, then the system shall inform the guest and not apply the discount. |
| FR-15 | The system shall allow guests to submit complaints through the user portal. | Stakeholder Session 1 – CEO, complaint submission (D-13). | **AC-15:** Given a guest is logged in, when they submit a complaint through the portal, then the system shall record the complaint. **Negative:** Given the complaint submission is incomplete, when the guest submits it, then the system shall identify the missing information and not accept the incomplete submission. |
| FR-16 | The system shall provide hotel owners with the ability to respond to guest complaints within 14 days. | Stakeholder Session 1 – CEO, owner complaint response period (D-13). | **AC-16:** Given a complaint has been submitted, when the owner sends a response, then the system shall record the response. The response period shall be 14 days from complaint submission. |
| FR-17 | The system shall allow guests to report suspected discrimination. | Stakeholder Session 1 – CEO, discrimination reporting (D-14). | **AC-17:** Given a guest experiences suspected discrimination, when they submit a report, then the system shall record the report for handling. |
| FR-18 | The system shall inform guests when a booking cannot be completed because the system is unavailable or an error prevents completion. | Stakeholder Session 1 – CEO, failure notification (D-15). | **AC-18:** Given a guest attempts to complete a booking but the system cannot process it, when the failure is detected, then the system shall inform the guest that the booking was not completed. **Negative:** Given the system cannot confirm payment success, then it shall not display a successful booking confirmation. |



## 5. Non-functional requirements

<!--
No metric, no target or no measurement method → not a requirement.
Every NFR names its source: a decision (D-__), the domain brief, or a regulation.
Required: at least one NFR each on personal data, fairness and accessibility
(category "Responsibility to users and community").
-->

| ID | Category | Requirement | Metric | Target | How it is measured | Source |
|---|---|---|---|---|---|---|
| NFR-01 | Availability | The booking platform shall remain available to users, except during permitted planned maintenance. | Monthly availability percentage | At least 99.5% per month | Monitor service uptime and calculate monthly availability, excluding agreed maintenance windows. | Stakeholder session 1 – CEO |
| NFR-02 | Performance | The system shall display search results quickly after a user submits a room search. | Page-load time for search results | 90% of searches shall load within 1 second. | Measure search-result page-load times and calculate the percentage completed within one second. | Stakeholder session 1 – CEO |
| NFR-03 | Capacity and scalability | The platform shall support simultaneous users during peak usage and accommodate expected user growth. | Number of concurrent users supported | At least 3,000 concurrent users; the system should accommodate expected growth from 10,000 users to approximately 20,000 users next year. | Conduct load and stress tests with the expected number of concurrent users. | Stakeholder session 1 – CEO |
| NFR-04 | Accessibility | The platform shall be accessible to users with disabilities, including users who rely on screen readers and keyboard navigation. | WCAG conformance and accessibility test results | WCAG 2.1 Level AA | Perform accessibility audits and test keyboard navigation and screen-reader compatibility. | Stakeholder session 1 – CEO |
| NFR-05 | Privacy and data retention | The system shall retain user data only for the specified retention period. Birthday information shall only be collected or used with explicit user consent. | Data retention period and consent compliance | User data retention: maximum 2 years. Explicit consent required for birthday information. | Review data-retention settings and verify that birthday information is processed only when consent is recorded. | Stakeholder session 1 – CEO |
| NFR-06 | Fairness | The system shall process competing booking requests fairly, giving priority to the first request received by the system. | Ordering of competing booking requests | Requests shall be processed in order of server receipt. | Test concurrent booking requests and verify their processing order using server timestamps. | Stakeholder session 1 – CEO |
| NFR-07 | Privacy and data protection | The system shall protect users' personal data against unauthorised access, disclosure, modification and loss. Access to personal information shall be restricted to authorised users and purposes. | Access-control compliance and number of unauthorised access incidents | Only authorised users can access personal data; no unauthorised access is permitted. | Review access permissions, perform security tests and monitor access logs for unauthorised activity. | Stakeholder session 1 – CEO; privacy and data-protection requirement |

## 6. Traceability matrix

| Use case | FR-01 | FR-02 | FR-03 | FR-04 | FR-05 | FR-06 | FR-07 | FR-08 | FR-09 | FR-10 | FR-11 | FR-12 | FR-13 | FR-14 | FR-15 | FR-16 | FR-17 | FR-18 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| UC-01 Book a Room | X | X | X | X | X | X | X | X | X | X | | | | X | | | | X |
| UC-02 Modify a Booking | | | | | | X | | | | | X | X | | | | | | |
| UC-03 Cancel a Booking | | | | | | X | | | | | | X | X | | | | | |

**Gaps found and how we addressed them:**

- FR-15, FR-16 and FR-17 are not covered by the three selected use cases. Additional use cases for submitting complaints, submitting reviews and reporting discrimination may be required.
- FR-14 (wheelchair accessibility filter) is included in the booking requirements but is not yet explicitly described in the UC-01 scenario. The search scenario should be extended to include this filter.
- FR-18 (preserving the confirmed booking price) should be added to the booking confirmation scenario and considered when modifying a booking.
- Owner-initiated cancellation is included as an alternate flow in UC-03, but its detailed refund rules still need clarification.


## 7. Decision log

See [decision log](decision-log.md).
