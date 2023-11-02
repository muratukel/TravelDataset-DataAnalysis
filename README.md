# WanderLuxe Travel Data Analysis ✈️ 🌍 🏨

![World Tourism Day](https://img.freepik.com/free-photo/top-view-world-tourism-day-with-lettering_23-2148608799.jpg?w=1380&t=st=1698343584~exp=1698344184~hmac=7546ca34214ef38e0295f0368fb53eb071c097b0f9532a9b0bcacd8e8e455161)

## Data Set Overview: WanderLuxe Travel Data Analysis 🔍 📑

🔖 This data set comprises three distinct tables from a travel reservation platform, namely the "Booking Table," "Passenger Table," and "Payment Table." These tables contain detailed data related to customer reservations, passenger details, and payment transactions. Below is a more in-depth description of the components of this data set:

**Booking Table 📅:**

- The "id" column serves as a unique identifier for each reservation.
- "contact_id" represents customers and indicates that a customer can make multiple reservations.
- "e_mail" contains the contact email addresses of customers.
- "booking_company" specifies through which travel company the customer made the reservation.
- "member_sales" reflects whether the customer is a member or not and is associated with the "user_id."
- "user_id" is the customer's identifier, taking "id" if they are a member, or "Not-Member" if not.
- "user_register_date" displays the date when a customer became a member.
- "booking_environment" indicates where the reservation was made, either through an app or online.
- "booking_date" records the date when the reservation was made by the customer.

**Passenger Table 🚶‍♂️:**

- "id" serves as a unique identifier for each passenger.
- "booking_id" is used to link passengers to reservations and matches with the "id" in the "Booking" table.
- "gender" specifies the gender of the passengers.
- "name" contains the names of the passengers.
- "date_of_birth" displays the birthdate of the passengers.

**Payment Table 💳:**

- "id" is a unique identifier for each payment transaction.
- "booking_id" is used to associate payments with relevant reservations.
- "payment_status" indicates whether a payment is successful, faulty, or a refund.
- "card_number" specifies the card used for the payment.
- "payment_date" shows the date on which the payment transaction occurred.

🔖 This data set provides valuable insights into travel reservations and customer information. It is particularly useful for conducting detailed analyses of customer behavior, reservation preferences, and payment transactions. This data set holds significant importance for tasks such as evaluating the impact of membership, payment success, and reservation sources in the travel industry and customer service. The analyses performed on this data set can aid in making strategic decisions for the travel industry and customer service sector.

## Project Objectives 📊 📈

- To conduct in-depth examination and analysis of travel data.
- To identify trends and opportunities within the travel industry.
- To provide analysis results for data-driven decision-making.

# ⭕ Data Set Notes:

- Customers are represented by "contactID."
- "bookingID" is used for the number of reservations, and "passengerID" is used for the number of passengers. While multiple passengers ("passengerID") can be in one reservation, there can only be one "contactID."
- Membership registration dates are left blank for non-member customers.
- "paymentstatus" should not count refunds as both successful and unsuccessful.

These notes provide an explanation of the dataset's characteristics and some essential considerations to keep in mind.

## 🏗️Database Structure and Diagram 

To represent the database structure and relationships between tables, you can use a textual format. Below is an example of a simple database structure:

**Tables:**

- `Booking Table`
  - Columns: `id`, `contact_id`, `e_mail`, `booking_company`, `member_sales`, `user_id`, `user_register_date`, `booking_environment`, `booking_date`

- `Passenger Table`
  - Columns: `id`, `booking_id`, `gender`, `name`, `date_of_birth`

- `Payment Table`
  - Columns: `id`, `booking_id`, `payment_status`, `card_number`, `payment_date`

**Relationships:**

- The "Booking Table" and "Passenger Table" are related through the "booking_id" column, indicating that passengers are associated with bookings.

- The "Booking Table" and "Payment Table" are linked through the "booking_id" column, showing that payments are related to bookings.

This is a simplified textual representation of the database structure and relationships between tables. For a more detailed visual representation, you can use database modeling tools like Entity-Relationship Diagrams (ERD) or draw diagrams using applications like draw.io or Lucidchart.

![image](https://github.com/muratukel/TravelDataset-DataAnalysis/assets/136103635/8bebb0ec-32ff-4bea-ae07-2c1b88c4e17a)


## 1-) Retrieve total sales quantities, amounts, and average ticket prices on a per-customer basis.

-  This question might have been posed by a marketing team looking to understand customer behavior and enhance marketing strategies. Total sales quantities, amounts, and average ticket prices on a per-customer basis provide insights into how frequently customers make purchases, how much they spend, and their preferences for specific product categories. This information can be utilized for making decisions related to customer segmentation, loyalty programs, personalized recommendations, and discount campaigns.

- To answer this question, it is necessary to group sales transactions in the dataset by customer identification numbers and calculate the total sales quantity, total sales amount, and average ticket price for each group.
