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

# CASE STUDY QUESTİONS AND QUERYS 

## 1-) Retrieve total sales quantities, amounts, and average ticket prices on a per-customer basis.

-  This question might have been posed by a marketing team looking to understand customer behavior and enhance marketing strategies. Total sales quantities, amounts, and average ticket prices on a per-customer basis provide insights into how frequently customers make purchases, how much they spend, and their preferences for specific product categories. This information can be utilized for making decisions related to customer segmentation, loyalty programs, personalized recommendations, and discount campaigns.

- To answer this question, it is necessary to group sales transactions in the dataset by customer identification numbers and calculate the total sales quantity, total sales amount, and average ticket price for each group.

``` sql
select 
	distinct b.contact_id as customers,  		-- customer id number
	count(distinct b.id) as total_sales, 	 	-- total number of sales (bookings)
	sum(pt.amount) as total_price,		  	-- total sales amount
	round(avg(pt.amount),2) as avg_ticket_price,	-- average ticket price 
from booking as 
left join payment as pt
	on pt.booking_id=b.id
where pt.payment_status = 'Succes-Payment'		-- successful payment filter 
group by 1                                      	-- customer-based grouping
```
- This code retrieves the total sales quantity, amount, and average ticket price for each customer in the dataset and sorts them in descending order by the total amount. This allows you to see the customers who spend the most.

## 2-) In 2020, on a monthly basis, retrieve the total number of passengers and basket counts in environmental breakdowns.

- This question seeks to analyze the profiles of customers of an airline company and determine how much sales were made in different environments (web, mobile, call center, etc.) on a monthly basis in the year 2020. Bringing the total number of passengers and basket counts in monthly environmental breakdowns reveals where the airline company received more demand, where more baskets were created, and where more passengers made purchases. This information can assist the airline company in optimizing its marketing and sales strategies.

- To answer this question, it is necessary to join the booking and passenger tables in the dataset and group them by booking_date (reservation date) and booking_environment (reservation environment) columns.

```sql
select 
	to_char(b.booking_date,'YYYY-MM') as year_filter, 	-- column representing year and month
	b.booking_environment as environment_breakdown,		-- reservation environment
	count(distinct p.id) as total_passenger_numbers,	-- total number of passengers
	count(distinct b.id) as total_number_of_baskets		-- total number of baskets
from booking as b
left join passenger as p
	on p.booking_id=b.id
where extract(year from b.booking_date) = 2020			-- bookings for 2020
group by 1,2
```
  
