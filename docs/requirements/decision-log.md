# Decision Log

The decisions below were made during the first stakeholder session and clarified afterwards. The decision IDs are kept the same so that requirements and use cases can refer to them.

| ID | Topic | Decision | Source |
|---|---|---|---|
| D-01 | Booking guarantee | Confirmed bookings are guaranteed. Overbooking is not allowed. | Stakeholder session 1 |
| D-02 | Confirmation | A booking is confirmed immediately after successful payment. The hotel owner does not need to approve it. | Stakeholder session 1 |
| D-03 | Price changes | Owners may change room prices. Changes do not affect the agreed price of an existing confirmed booking. | Stakeholder session 1 |
| D-04 | Payment | Guests must pay before a booking can be created and confirmed. Card and PayPal are accepted; paying at the hotel is not an option. | Stakeholder session 1; clarification |
| D-05 | Registration | A guest must be registered before booking a room. | Stakeholder session 1 |
| D-06 | Personal details | First name, last name and email are required. Phone number is optional. A billing address is requested only for an invoice. Nationality and copies of identity documents are not collected. | Stakeholder session 1; clarification |
| D-07 | Consent | Birthday information and marketing emails each require the guest's explicit consent. | Stakeholder session 1; clarification |
| D-08 | Guest cancellation | Cancelling at least 48 hours before arrival is free. A later cancellation incurs the first night's charge. | Stakeholder session 1; clarification |
| D-09 | Accessible rooms | Room search must include a wheelchair-accessibility filter. | Stakeholder session 1 |
| D-10 | Software accessibility | The platform must support keyboard navigation and screen readers and meet WCAG 2.1 AA. | Stakeholder session 1 |
| D-11 | Owner cancellation | An owner may cancel directly at least 14 days before arrival if there is a valid reason. The guest receives a full refund and is informed automatically. With fewer than 14 days remaining, the owner must contact support instead. | Stakeholder session 1; clarification |
| D-12 | Booking changes | Booking changes follow the applicable cancellation rules, including changes to the payment method. | Stakeholder session 1; clarification |
| D-13 | Changeable details | Guests can change dates or room type until 48 hours before check-in. The current price applies to the changed booking. | Stakeholder session 1; clarification |
| D-14 | Availability target | Monthly system availability must be at least 99.5%. | Stakeholder session 1 |
| D-15 | Maintenance | Planned maintenance is permitted only on Tuesdays from 02:00 to 04:00. | Stakeholder session 1 |
| D-16 | Booking failure | If the platform fails during a booking, the guest must be told that the booking was not completed. | Stakeholder session 1 |
| D-17 | Displayed prices | Displayed prices must include taxes. | Stakeholder session 1 |
| D-18 | Peak load | The platform must support 3,000 simultaneous users. | Stakeholder session 1 |
| D-19 | Growth | There are about 3,000 users currently. The expected number is about 10,000 within one to two years. | Stakeholder session 1; clarification |
| D-20 | Guest refunds | A guest who cancels at least 48 hours before arrival receives a full refund. For later cancellation, the first night's price is charged and the rest of the payment is refundable, if applicable. | Stakeholder session 1; clarification |
| D-21 | Temporary hold | Pressing **Pay** holds an available room for 30 minutes. A hold is not a confirmed booking. | Stakeholder session 1 |
| D-22 | Hold expiry | If payment has not succeeded when the hold expires, the room becomes available again. | Stakeholder session 1; clarification |
| D-23 | Promotions | Guests may use promotional codes when booking. | Stakeholder session 1 |
| D-24 | Complaints | Guests may submit complaints through the portal. Hotel owners have 14 days to respond. | Stakeholder session 1 |
| D-25 | Reviews | Owners are not required to respond to guest reviews. | Stakeholder session 1 |
| D-26 | Competing bookings | The request received first by the system has priority when guests compete for the same available room. | Stakeholder session 1 |
| D-27 | Failed payments | After a failed payment, the guest's entered booking information is kept for 30 minutes to allow a retry. This does not extend the room hold. | Stakeholder session 1 |
| D-28 | Discrimination reports | Guests must be able to report discrimination. | Stakeholder session 1 |
| D-29 | Data retention | Accounts that have never made a booking are deleted after two years. Personal data of guests who have booked is kept for three years. | Clarified by instructor |

## Points to check

- Earlier notes mentioned changing the **number of guests**, but the confirmed clarification names **dates and room type**. Check the stakeholder notes before including guest-count changes.
- The decision allows payment-method changes under the same booking-change rules, but the exact steps for changing only the method were not recorded.
- For D-29, the start date used to calculate each retention period has not been specified in the material available to us.
