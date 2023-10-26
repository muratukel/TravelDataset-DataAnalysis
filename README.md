# WanderLuxe Travel Data Analysis ✈️ 🌍 🏨

![World Tourism Day](https://img.freepik.com/free-photo/top-view-world-tourism-day-with-lettering_23-2148608799.jpg?w=1380&t=st=1698343584~exp=1698344184~hmac=7546ca34214ef38e0295f0368fb53eb071c097b0f9532a9b0bcacd8e8e455161)

**Data Set Overview: Travel Reservation Analysis**

This data set comprises three distinct tables from a travel reservation platform, namely the "Booking Table," "Passenger Table," and "Payment Table." These tables contain detailed data related to customer reservations, passenger details, and payment transactions. Below is a more in-depth description of the components of this data set:

**Booking Table:**

- The "id" column serves as a unique identifier for each reservation.
- "contact_id" represents customers and indicates that a customer can make multiple reservations.
- "e_mail" contains the contact email addresses of customers.
- "booking_company" specifies through which travel company the customer made the reservation.
- "member_sales" reflects whether the customer is a member or not and is associated with the "user_id."
- "user_id" is the customer's identifier, taking "id" if they are a member, or "Not-Member" if not.
- "user_register_date" displays the date when a customer became a member.
- "booking_environment" indicates where the reservation was made, either through an app or online.
- "booking_date" records the date when the reservation was made by the customer.

**Passenger Table:**

- "id" serves as a unique identifier for each passenger.
- "booking_id" is used to link passengers to reservations and matches with the "id" in the "Booking" table.
- "gender" specifies the gender of the passengers.
- "name" contains the names of the passengers.
- "date_of_birth" displays the birthdate of the passengers.

**Payment Table:**

- "id" is a unique identifier for each payment transaction.
- "booking_id" is used to associate payments with relevant reservations.
- "payment_status" indicates whether a payment is successful, faulty, or a refund.
- "card_number" specifies the card used for the payment.
- "payment_date" shows the date on which the payment transaction occurred.

This data set provides valuable insights into travel reservations and customer information. It is particularly useful for conducting detailed analyses of customer behavior, reservation preferences, and payment transactions. This data set holds significant importance for tasks such as evaluating the impact of membership, payment success, and reservation sources in the travel industry and customer service. The analyses performed on this data set can aid in making strategic decisions for the travel industry and customer service sector.

## Project Objectives

- To conduct in-depth examination and analysis of travel data.
- To identify trends and opportunities within the travel industry.
- To provide analysis results for data-driven decision-making.
