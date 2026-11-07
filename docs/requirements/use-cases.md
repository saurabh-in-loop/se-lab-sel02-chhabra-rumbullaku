# Use Cases

![Use case diagram](use-case-diagram.png)

<!--
Save your use case diagram as docs/requirements/use-case-diagram.png — then it shows up above.
Describe your THREE most complex use cases below. Copy the UC-01 block for each.
Use → for actor actions and ← for system responses.
Every use case needs at least two alternate flows.
-->


## UC-01 – Book a Room

| Field | Description |
|---|---|
| Related requirements | FR-01, FR-02, FR-03, FR-04, FR-05, FR-06, FR-07, FR-08, FR-09, FR-10, FR-14, FR-18 |
| Initiating actor | Guest |
| Actor's goal | Find an available room and complete a guaranteed booking. |
| Participating actors | Payment provider |
| Preconditions | The guest is registered and the booking platform is available. |
| Postconditions | If payment succeeds, the booking is confirmed and the guest receives confirmation. If payment fails or the 30-minute hold expires, no booking is confirmed. |

**Main success scenario**

1. → Guest opens the booking platform and searches for accommodation using destination, dates and number of guests.
2. ← System displays available rooms matching the search criteria, including prices with applicable taxes.
3. → Guest selects a suitable room.
4. ← System displays room details, availability, total price and applicable conditions.
5. → Guest enters or confirms the required booking information.
6. → Guest presses the payment button and selects a payment method.
7. ← System temporarily holds the selected room for 30 minutes and starts the payment process.
8. → Guest completes the payment.
9. ← Payment provider confirms successful payment.
10. ← System confirms the booking immediately without requiring hotel-owner approval.
11. ← System displays the booking confirmation and sends confirmation information to the guest.

**Alternate flow A – No rooms match the search criteria (branches at step 2)**

- a. System cannot find available rooms matching the guest's search criteria.
- b. System informs the guest that no matching rooms are available.
- c. Guest may change the search criteria and search again.

**Alternate flow B – Payment fails (branches at step 9)**

- a. Payment provider reports that the payment has failed.
- b. System informs the guest that payment was unsuccessful.
- c. System retains the previously entered booking information during the remaining 30-minute period.
- d. Guest may try the payment again without entering the information again.
- e. If payment succeeds within the hold period, the main success scenario continues at step 10.

**Alternate flow C – The 30-minute hold expires (branches at step 7)**

- a. Guest does not complete a successful payment within 30 minutes.
- b. System releases the temporarily held room.
- c. System informs the guest that the hold has expired and the booking was not completed.
- d. The room may become available for another guest to book.
- e. Guest may search again and start a new booking.

## UC-02 – Modify a Booking

| Field | Description |
|---|---|
| Related requirements | FR-11, FR-07, FR-13 |
| Initiating actor | Guest |
| Actor's goal | Change details of an existing booking. |
| Participating actors | Payment provider, if a payment adjustment is required |
| Preconditions | Guest has an existing confirmed booking and is logged in. |
| Postconditions | The booking is updated if the requested changes are permitted. Otherwise, the original booking remains unchanged. |

**Main success scenario**

1. → Guest logs into the platform and opens their existing booking.
2. ← System displays the booking details and available modification options.
3. → Guest chooses to modify the booking.
4. ← System allows the guest to select changes to the number of guests, payment method or booking dates.
5. → Guest enters the requested changes.
6. ← System checks the availability of the requested dates and applies the applicable booking and cancellation rules.
7. ← System displays the updated booking details and any applicable price or payment changes.
8. → Guest reviews and confirms the changes.
9. ← System saves the updated booking.
10. ← System informs the guest that the booking has been modified.

**Alternate flow A – Requested dates are unavailable (branches at step 6)**

- a. System determines that the requested dates are unavailable.
- b. System informs the guest that the requested modification cannot be completed.
- c. The original booking remains unchanged.
- d. Guest may choose different dates or cancel the modification.

**Alternate flow B – Modification is not permitted under the applicable rules (branches at step 6)**

- a. System determines that the requested change cannot be accepted under the applicable cancellation rules.
- b. System informs the guest about the applicable restrictions.
- c. The original booking remains unchanged.
- d. Guest may keep the existing booking or follow the cancellation process.

**Alternate flow C – Guest does not confirm the changes (branches at step 8)**

- a. Guest decides not to proceed with the modification.
- b. System discards the unconfirmed changes.
- c. The original booking remains unchanged.

## UC-03 – Cancel a Booking

| Field | Description |
|---|---|
| Related requirements | FR-12, FR-13 |
| Initiating actor | Guest |
| Actor's goal | Cancel an existing booking according to the cancellation policy. |
| Participating actors | Payment provider |
| Preconditions | Guest has an existing confirmed booking and can access its details. |
| Postconditions | The booking is cancelled and the applicable refund or cancellation charge is processed or communicated to the guest. |

**Main success scenario – Guest cancellation**

1. → Guest logs into the platform and opens their confirmed booking.
2. ← System displays the booking details and cancellation option.
3. → Guest selects the cancellation option.
4. ← System displays the applicable cancellation conditions.
5. → Guest confirms the cancellation.
6. ← System checks the time remaining until the scheduled arrival.
7. ← System determines the applicable cancellation charge:
   - Cancellation at least 48 hours before arrival: full refund.
   - Cancellation less than 48 hours before arrival: charge for the first night.
8. ← System records the cancellation and updates the booking status.
9. ← System processes or initiates the applicable refund or charge through the payment provider.
10. ← System informs the guest about the cancellation and the applicable refund or charge.

**Alternate flow A – Guest cancels less than 48 hours before arrival (branches at step 7)**

- a. System determines that less than 48 hours remain before arrival.
- b. System informs the guest that the first night's cost will be charged.
- c. Guest confirms the cancellation.
- d. System records the cancellation and applies the first-night charge.

**Alternate flow B – Cancellation cannot be processed (branches at step 9)**

- a. Payment provider or system reports that the refund or charge cannot currently be processed.
- b. System informs the guest that the cancellation has been recorded but the payment transaction could not be completed.
- c. System records the payment issue for further processing.

**Alternate flow C – Guest does not confirm cancellation (branches at step 5)**

- a. Guest decides not to cancel the booking.
- b. System returns to the booking details.
- c. The booking remains unchanged.

**Alternate flow D – Hotel owner requests cancellation**

- a. Hotel owner requests cancellation of an existing booking at least 14 days before arrival.
- b. System requires the owner to provide a valid reason.
- c. System records the cancellation request and reason.
- d. If fewer than 14 days remain before arrival, the owner must contact support instead of cancelling directly.