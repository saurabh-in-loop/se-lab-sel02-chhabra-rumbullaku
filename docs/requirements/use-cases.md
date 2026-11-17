# Use Cases

![Use case diagram](use-case-diagram.png)

These are the three detailed use cases chosen for the hotel booking platform. In the steps below, **→** means an actor action and **←** means a system or payment-provider response.

## UC-01 — Book a Room

| Field | Description |
|---|---|
| Related requirements | FR-05, FR-06, FR-07, FR-08, FR-09, FR-10, FR-14, FR-18, FR-20, FR-22, FR-23, FR-25, FR-26, FR-29; registration prerequisites FR-01–FR-04 |
| Initiating actor | Guest |
| Goal | Find an available room and complete a paid, confirmed booking. |
| Participating actor | Payment Provider |
| Preconditions | Guest is registered; platform is available. |
| Success postcondition | Payment succeeded during a valid room hold. Booking is confirmed immediately with the agreed price, and the guest is informed. |
| Failure postcondition | No booking is confirmed if payment fails, the hold expires or the room is no longer available. |

**Main success scenario**

1. → Guest searches using destination, check-in and check-out dates and number of guests. The guest may select the wheelchair-accessibility filter.
2. ← System shows matching available rooms and prices including taxes.
3. → Guest chooses a room.
4. ← System shows the room details, booking conditions and total price.
5. → Guest enters or checks booking details, optionally applies a promotion code and may request an invoice.
6. ← System checks the promotion and shows the final price. A billing address is requested only if an invoice was selected. No nationality or ID copy is required.
7. → Guest chooses card or PayPal and presses **Pay**.
8. ← System checks availability again and holds the room for 30 minutes. The hold does not count as a confirmed booking.
9. → Guest completes the payment with the Payment Provider.
10. ← Payment Provider reports that the payment succeeded before the hold expired.
11. ← System confirms the booking immediately, saves the agreed price and does not request owner approval.
12. ← System displays the confirmation and informs the guest.

**Alternate A — No matching rooms (from step 2)**

- a. ← System finds no available rooms matching the criteria.
- b. ← System shows a no-results message.
- c. → Guest may change the search and try again.

**Alternate B — Room becomes unavailable (from step 8)**

- a. ← System finds an overlapping confirmed booking or an earlier active hold.
- b. ← System does not start a second hold for the same room and dates.
- c. ← Guest is told that the room is unavailable and may choose another room.

**Alternate C — Payment fails (from step 10)**

- a. ← Payment Provider reports unsuccessful payment.
- b. ← System tells the guest that the booking is not confirmed.
- c. ← Entered booking details are kept for 30 minutes after the payment failure.
- d. → Guest may try again. Payment must succeed while a room hold is still valid; saved details do not extend an expired hold.

**Alternate D — Hold expires (after step 8, before confirmation)**

- a. ← The 30-minute hold ends without successful payment.
- b. ← System releases the room and informs the guest that the booking was not completed.
- c. → Guest may search again and start a new booking attempt.

**Alternate E — Invalid promotion code (from step 6)**

- a. ← System rejects the invalid or expired code and does not apply the discount.
- b. ← Guest may remove the code or use another one before paying.

**Alternate F — Booking cannot be completed (from steps 10–11)**

- a. ← System cannot complete processing or verify payment success.
- b. ← No confirmed booking is shown without a verified successful payment and valid hold.
- c. ← Guest is informed that the booking was not completed or confirmed.

## UC-02 — Modify a Booking

| Field | Description |
|---|---|
| Related requirements | FR-07, FR-11, FR-20, FR-26, FR-30 |
| Initiating actor | Guest |
| Goal | Change the dates or room type of an existing booking. |
| Participating actor | Payment Provider, if a payment adjustment is needed |
| Preconditions | Guest can access their own confirmed booking. |
| Success postcondition | An allowed change is saved at the current price and the guest receives confirmation. |
| Failure postcondition | If the change is rejected or not completed, the original booking and its agreed price remain unchanged. |

**Main success scenario — Change dates or room type**

1. → Guest opens a confirmed booking.
2. ← System shows the existing details and agreed price.
3. → Guest selects **Modify a Booking**.
4. ← System shows the available modification options.
5. → Guest enters new stay dates or selects a different room type.
6. ← System checks that the request is made at least 48 hours before check-in and that the requested room and dates are available without overlapping another booking.
7. ← System displays the revised booking details and current price, including taxes and any payment difference.
8. → Guest accepts the changes and revised price.
9. ← If a payment adjustment is needed, it is handled with the Payment Provider. The system saves the change only after any required adjustment has succeeded.
10. ← System confirms the modification to the guest.

**Alternate A — Requested dates or room type not available (from step 6)**

- a. ← System finds no available room for the requested change.
- b. ← System explains that the modification cannot be made.
- c. ← The existing booking remains unchanged.

**Alternate B — Too close to check-in (from step 6)**

- a. ← The request is made fewer than 48 hours before check-in.
- b. ← System rejects the date or room-type change and shows the deadline.
- c. ← The existing booking remains unchanged.

**Alternate C — Guest does not accept the new price (from step 8)**

- a. → Guest declines or leaves the modification process.
- b. ← No change is saved; the original agreed price still applies.

**Alternate D — Payment adjustment fails (from step 9, if needed)**

- a. ← Payment Provider reports a failed adjustment.
- b. ← System informs the guest that the change was not completed.
- c. ← The original booking is kept.

**Alternate E — Change payment method (from step 4)**

- a. → Guest requests a different payment method.
- b. ← System applies the same booking-change deadline and offers the supported payment methods (card or PayPal).
- c. ← If the change is permitted, the system handles any payment adjustment needed before saving it. The exact adjustment process still needs to be specified.
- d. ← If the request is too late or cannot be completed, the existing booking and payment details remain unchanged.

**Open question:** Guest-count changes were mentioned in an earlier draft but need checking against the stakeholder notes.

## UC-03 — Cancel a Booking

| Field | Description |
|---|---|
| Related requirements | FR-12, FR-19, FR-21, FR-27, FR-28 |
| Initiating actor | Guest (main scenario); Hotel Owner (alternate D) |
| Goal | Cancel a confirmed booking in accordance with the cancellation policy. |
| Participating actor | Payment Provider |
| Preconditions | The guest owns the confirmed booking, or the owner manages the hotel concerned. |
| Success postcondition | Booking is cancelled; the required refund is initiated and the guest is informed. |
| Failure postcondition | If the request is not allowed or is abandoned, the booking stays unchanged. |

**Main success scenario — Guest cancels at least 48 hours before arrival**

1. → Guest opens their confirmed booking.
2. ← System displays the booking details and cancellation option.
3. → Guest requests cancellation.
4. ← System checks the time before arrival and shows the cancellation terms and full refund.
5. → Guest confirms cancellation.
6. ← System cancels the booking and updates room availability.
7. ← System requests a full refund from the Payment Provider.
8. ← System informs the guest that the booking was cancelled and shows the refund status.

**Alternate A — Cancellation less than 48 hours before arrival (from step 4)**

- a. ← System calculates a first-night charge and any remaining refundable amount.
- b. ← System shows the charge to the guest before confirmation.
- c. → If the guest confirms, the booking is cancelled, the first-night charge is retained and any remaining refund is requested.

**Alternate B — Refund processing fails (from step 7)**

- a. ← Payment Provider cannot process the refund immediately.
- b. ← System records the issue and does not claim that the refund was completed.
- c. ← Guest is told that the cancellation was recorded but the refund is still unresolved.

**Alternate C — Guest abandons cancellation (from step 5)**

- a. → Guest decides not to cancel.
- b. ← No cancellation or refund is processed. The booking stays confirmed.

**Alternate D — Hotel Owner cancels (branches at step 1: owner starts instead of guest)**

- a. → Hotel Owner selects a confirmed booking for a hotel they manage and requests cancellation.
- b. ← System checks the arrival date and requires a valid cancellation reason.
- c. → If at least 14 days remain and the reason is valid, the owner confirms cancellation.
- d. ← System cancels the booking directly, requests a **full refund** and **automatically informs the guest**.
- e. ← If fewer than 14 days remain, direct cancellation is blocked and the owner is told to contact support. The support process has not been specified.
- f. ← If no valid reason is supplied, the system does not complete the cancellation.

## Use-case coverage

The detailed descriptions above cover the three selected use cases. Other functions from the requirements still need separate scenarios if they are to be documented in full: owner room-price and availability management, guest complaints, discrimination reports, marketing consent and reviews. The use-case diagram includes owner management but does not describe every one of these processes in detail.
