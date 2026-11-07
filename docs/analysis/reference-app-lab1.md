# Reference App — Requirements (Lab 1)

<!-- About one page. Evidence for every claim: a screen, a file, or a class. -->

## 1. Covered

1. User registration: Guests can create accounts using their name, email address and password.

2. Hotel search: Users can search by destination, dates, number of guests, star rating, price and amenities.

3. Room availability: The application checks whether rooms are available for selected dates and prevents overlapping bookings.

4. Payment: Guests can pay using simulated credit-card or PayPal payments.

5. Booking management: Guests can view bookings, cancel bookings and modify dates under certain conditions.

6. Pricing: The system calculates room prices, taxes, cleaning fees, seasonal adjustments and discounts.

7. Reviews: Guests can submit reviews after completing their stay.

8. Owner management: Hotel owners can manage hotels, rooms, bookings and availability.

## 2. Ignored

1. Instant confirmation: Paid bookings are not always confirmed immediately. The application allows hotel owners to approve or decline requests unless instant booking is enabled.

2. Thirty-minute reservation hold: A requested booking blocks room availability, but no 30-minute expiration mechanism is implemented.

3. Cancellation policy: StayHub uses configurable Flexible, Moderate and Strict policies instead of the stakeholder-defined 48-hour cancellation rule.

4. Booking modifications: Date changes are only allowed while the booking is still in the REQUESTED state.

5. Payment failure: Payment can be retried, but the specified 30-minute retention of entered booking data is not evident.

6. Accessibility: Generic amenity filters exist, but a dedicated wheelchair-accessibility filter and WCAG 2.1 AA compliance are not demonstrated.

7. Privacy: The implementation does not demonstrate the specified two-year personal-data retention policy or explicit birthday consent.

8. Non-functional requirements: The source code does not establish compliance with the required availability, performance or concurrent-user targets.

## 3. Invented

1. Favourite or saved hotels.

2. Hotel reviews and ratings.

3. Seasonal and weekend price adjustments.

4. Cleaning fees.

5. PayPal as an additional payment method.

6. Guest invoices and notifications.

7. Owner dashboards and occupancy statistics.

8. Hotel check-in and check-out management.

## 4. Silently decided

1. **Overbooking vs. guaranteed bookings:** Malte suggests allowing approximately 10% overbooking to increase hotel occupancy, while Selin insists that every confirmed booking must be guaranteed. StayHub checks room availability and prevents overlapping bookings. This behaviour is closer to Selin's expectation.

2. **Owner approval vs. instant confirmation:** Malte wants owners to accept or decline booking requests, whereas Selin expects instant confirmation. StayHub supports both approaches through an instant-booking setting. Depending on the hotel's configuration, a booking may be confirmed automatically or require owner approval. The application therefore leaves this decision to the hotel configuration instead of enforcing one universal rule.

3. **Owner cancellation vs. booking guarantee:** Malte wants owners to be able to cancel bookings when necessary, while Selin considers a confirmed booking a promise to the guest. StayHub provides owner-side booking management, but its behaviour does not establish the stakeholder-defined restriction on when owners may cancel.

4. **Changing prices vs. fixed prices:** Malte expects hotel owners to change prices whenever necessary and for the system to use current prices. Selin expects guests to pay exactly the price displayed during booking. StayHub supports seasonal and weekend price adjustments, as well as additional fees and discounts. The application does not establish the same explicit price-protection rule that was later decided for existing bookings.

5. **Cancellation policies:** Malte proposes charging the full stay for cancellations less than 14 days before arrival, while Selin wants free cancellation until the day before arrival. StayHub uses configurable Flexible, Moderate and Strict cancellation policies rather than enforcing either stakeholder's proposed rule.

6. **Payment timing:** Malte requires payment before a booking is made, whereas Selin wants guests to have the option of paying at the hotel. StayHub implements payment processing as part of its booking workflow and does not establish the requested universal pay-at-hotel option.

7. **Personal data:** Malte requests extensive guest information, including address, telephone number, date of birth, nationality and identity documents. Selin argues that name and email address should be sufficient. StayHub's registration process uses basic account information and does not implement the full set of additional personal-data fields requested by Malte.

