# Conflicts and Open Questions

<!--
From the two stakeholder emails: where do they contradict each other, what do they leave open?
Do NOT resolve anything here — you get the decisions in the stakeholder session.
-->

| # | Conflict or open question | Who says what (quote) | Decision we need | Affects |
|---|---|---|---|---|
| Q1 |Booking confirmation | Malte Hansen: owners should approve or decline requests within one day. Selin Aydın: guests should receive instant confirmation.|Should a booking be confirmed immediately or only after owner approval? What should the guest receive while waiting? | UC-01 Book a Room; UC-02 Review a Booking Request|

| Q2 |Cancellation policy | Malte Hansen: guests cancelling less than 14 days before arrival pay for the full stay. Selin Aydın: cancellation should be free until the day before arrival.| What is the cancellation deadline, and what charges apply after it?|UC-03 Cancel a Booking |

| Q3 |Payment timing | Malte Hansen: guests pay at the time of booking. Selin Aydın: guests should be allowed to pay at the hotel.| When must guests pay, and which payment methods should be supported?|UC-01 Book a Room |

| Q4 | Overbooking| Malte Hansen proposes allowing approximately 10% overbooking. Selin Aydın wants to ensure confirmed guests are never left without a room.| Is overbooking permitted? If so, how should the system handle cases where there are more confirmed bookings than available rooms?|UC-01 Book a Room; UC-02 Review a Booking Request |

| Q5 |Room prices and price changes | Malte Hansen says owners can change prices at any time and the platform should use the current price. Selin Aydın says the displayed price should be final, including taxes and fees.| At what point is the price fixed for a guest? How should taxes, fees and later price changes be handled?| UC-01 Book a Room|

| Q6 |Data retention and birthday offers |Malte Hansen wants to use guest birthdays for offers and requests extensive personal data. | How long should guest data be retained, and which data may be used for marketing offers?| UC-01 Book a Room|

