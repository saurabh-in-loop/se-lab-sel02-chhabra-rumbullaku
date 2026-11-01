# Use Cases

![Use case diagram](use-case-diagram.png)

<!--
Save your use case diagram as docs/requirements/use-case-diagram.png — then it shows up above.
Describe your THREE most complex use cases below. Copy the UC-01 block for each.
Use → for actor actions and ← for system responses.
Every use case needs at least two alternate flows.
-->

## UC-01 — Book a Room

| Field | |
|---|---|
| Related requirements | *(filled in the Lab 1 report)* |
| Initiating actor | Guest |
| Actor's goal |Find a suitable room and submit a booking request |
| Participating actors |Hotel owner|
| Preconditions |The booking platform is available, and the guests has selected desired dates and a room that appears available |
| Postconditions |A booking request has been recorded. Its final decision depends on the owner policy which is still unresolved |

**Main success scenario**

1. → Guest searches for a room that match the search criteria and their prices.
2. ← System displays rooms that match their search criteria and their prices.
3. → Guest selects a suitable room.
4. ← System displays the room details, price and applicable taxes or fees.
5. → Guest enters the required booking information and submits the booking request.
6. ← System checks availability and validates the submitted information.
7. ← System records the booking request and acknowledges receipt to the guest.
8. ← System makes the request available for the hotel owner to review.

**Alternate flow A — Room becomes unavailable (branches at step 6)

- a. The system discovers that the selected room is no longer available for the requested dates.
- b. The system informs the guest that the room cannot be booked for those dates.
- c. The guest may search again for another room or different dates.


**Alternate flow B — No rooms match the search criteria (branches at step 1)

- a. The guest enters the destination, dates and number of guests. 
- b. The system cannot find any rooms matching the search criteria.
- c. The system informs the guest that no suitable rooms were found.
- d. The guest may change the search criteria and search again.

## UC-02 — Review a booking request

| Field | |
|---|---|
| Related requirements | *(filled in the Lab 1 report)* |
| Initiating actor | Hotel Owner |
| Actor's goal |Review a guest's booking request and decide whether to approve or decline it. |
| Participating actors |Guest|
| Preconditions |A booking request has been submitted by a guest and is available for the hotel owner to review. |
| Postconditions |The owner's decision is recorded, and the booking request has an updated status. |

**Main success scenario**

1. → Hotel Owner opens the list of booking requests awaiting a decision.
2. ← System displays the pending requsts and relevant booking details.
3. → Hotel Owner selects a booking request.
4. ← System displays the details of the requested stay, including the room, dates and price.
5. → Hotel Owner reviews the request and chooses to approve it.
6. ← System records the owner's decision and updates the request status.
7. ← System informs the guest of the decision.

**Alternate flow A — Hotel Owner declines the request (branches at step 5)

- a. Hotel Owner decides that the request cannot be accepted.
- b. Hotel Owner chooses to decline the request.
- c. System records the decision and updates the request status.
- d. System informs the guest that the request was declined.

**Alternate flow B — Request is no longer available for review (branches at step 3)

- a. The selected request has already been processed or is no longer available.
- b. System informs the hotel owner that the request cannot be processed in its current state.
- c. System refreshes the request list or returns the owner to the list of pending requests.

## UC-03 — Cancel a Booking

| Field | |
|---|---|
| Related requirements | *(filled in the Lab 1 report)* |
| Initiating actor | Guest |
| Actor's goal |Cancel an existing booking.|
| Participating actors |Hotel owner|
| Preconditions |An existing booking is recorded in the system and can be identified.|
| Postconditions |The cancellation request is processed according to the applicable cancellation rules, and the booking status is updated if cancellation is permitted.|

**Main success scenario**

1. → Guest opens their existing booking.
2. ← System displays the booking details and the available cancellation option.
3. → Guest chooses to cancel the booking.
4. ← System displays the cancellation conditions applicable to the booking, if these have been defined.
5. → Guest confirms the cancellation.
6. ← System checks whether cancellation is permitted under the applicable policy.
7. ← System records the cancellation and updates the booking status.
8. ← System informs the guest that the booking has been cancelled and displays any applicable charge or refund information.

**Alternate flow A — Cancellation is not permitted (branches at step 6)

- a. The applicable cancellation policy does not permit cancellation under the current conditions.
- b. System informs the guest that the booking cannot be cancelled under the applicable policy.
- c. The booking remains unchanged, and the guest may return to the booking details.

**Alternate flow B — Cancellation cannot be processed (branches at step 6)

- a. System cannot complete the cancellation because of a processing error or because the booking status has changed. 
- b. System informs the guest that the cancellation could not be completed.
- c. System leaves the booking unchanged unless the cancellation has already been successfully recorded.
- d. Guest may retry or contact support.
