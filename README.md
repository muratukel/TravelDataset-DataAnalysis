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

![image](https://github.com/muratukel/TravelDataset-DataAnalysis/assets/136103635/7a526791-5fc3-48a9-9e66-19badfa7b0c0)

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
- `select distinct b.contact_id as customers`: Selects the column `contact_id`, which represents customer ID numbers.

- `count(distinct b.id) as total_sales`: Counts the total number of sales (bookings).

- `sum(pt.amount) as total_price`: Calculates the total sales amount by summing the `amount` column from the payment table.

- `round(avg(pt.amount), 2) as avg_ticket_price`: Computes the average ticket price by rounding the average of the `amount` column in the payment table to two decimal places.

- `from booking as b`: Includes the `booking` table in the query with the alias `b`.

- `left join payment as pt on pt.booking_id = b.id`: Performs a left join between the `booking` table and the `payment` table, linking them based on the booking ID (`id` in the `booking` table and `booking_id` in the `payment` table).

- `where pt.payment_status = 'Succes-Payment'`: Filters the results to include only reservations with a payment status of 'Succes-Payment,' representing successful payments.

- `group by 1`: Groups the results by customer, displaying the total sales, total sales amount, and average ticket price for each customer.

- This code retrieves the total sales quantity, amount, and average ticket price for each customer in the dataset and sorts them in descending order by the total amount. This allows you to see the customers who spend the most.

| customers | total_sales | total_price | avg_ticket_price |
|-----------|-------------|-------------|------------------|
| 157       | 2           | 500         | 250.00           |
| 244       | 1           | 575         | 575.00           |
| 271       | 1           | 85          | 85.00            |
| 799       | 1           | 70          | 70.00            |
| 1894      | 1           | 80          | 80.00            |
| 2338      | 4           | 1350        | 337.50           |
| 2800      | 2           | 75          | 37.50            |
| 2935      | 1           | 137         | 137.00           |
| 3013      | 2           | 270         | 135.00           |
| 3172      | 1           | 150         | 150.00           |

- The first 10 rows are shown.
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
- `to_char(b.booking_date, 'YYYY-MM') as year_filter`: In this section, we convert the reservation date in the `booking_date` column to the 'YYYY-MM' format, creating a column that represents the reservation date in the year and month format.

- `b.booking_environment as environment_breakdown`: In this section, we select the `booking_environment` column, which represents the reservation environment. It indicates where the reservations were made.

- `count(distinct p.id) as total_passenger_numbers`: This part calculates the number of unique passengers for each reservation. It counts the total number of passengers with a left join to the `passenger` table, obtaining the passenger count for each reservation.

- `count(distinct b.id) as total_number_of_baskets`: This part calculates the number of unique baskets for each reservation. It assumes that each reservation has a unique basket number.

- `from booking as b`: Includes the `booking` table in the query with the alias `b`.

- `left join passenger as p on p.booking_id = b.id`: It performs a left join between the `booking` table and the `passenger` table, linking them based on the reservation ID (`id` in the `booking` table and `booking_id` in the `passenger` table). This is used to obtain the passenger count for each reservation.

- `where extract(year from b.booking_date) = 2020`: In this section, it filters reservations for the year 2020. It focuses only on data from the year 2020.

- `group by 1,2`: The query groups the results by the `year_filter` and `environment_breakdown` columns. This allows the results to be aggregated separately for each year and environment.

- As a result, this query retrieves the passenger count and basket count for reservations made in different reservation environments on a monthly basis for the year 2020.

| year_filter | environment_breakdown | total_passenger_numbers | total_number_of_baskets |
|-------------|------------------------|--------------------------|-------------------------|
| 2020-01     | Application            | 8892                     | 6985                    |
| 2020-01     | Internet               | 14983                    | 11692                   |
| 2020-02     | Application            | 6111                     | 5029                    |
| 2020-02     | Internet               | 8400                     | 6868                    |
| 2020-03     | Application            | 5299                     | 4518                    |
| 2020-03     | Internet               | 6208                     | 5213                    |
| 2020-04     | Application            | 203                      | 177                     |
| 2020-04     | Internet               | 127                      | 107                     |
| 2020-05     | Application            | 2023                     | 1737                    |
| 2020-05     | Internet               | 2448                     | 2040                    |
| 2020-06     | Application            | 5414                     | 4537                    |
| 2020-06     | Internet               | 4975                     | 4084                    |
| 2020-07     | Application            | 9262                     | 7233                    |
| 2020-07     | Internet               | 7881                     | 6007                    |
| 2020-08     | Application            | 8680                     | 6805                    |
| 2020-08     | Internet               | 5310                     | 4026                    |
| 2020-09     | Application            | 5740                     | 4680                    |
| 2020-09     | Internet               | 3161                     | 2484                    |
| 2020-10     | Application            | 5867                     | 4848                    |
| 2020-10     | Internet               | 3253                     | 2604                    |
| 2020-11     | Application            | 4899                     | 4092                    |
| 2020-11     | Internet               | 2564                     | 2134                    |
| 2020-12     | Application            | 4519                     | 3852                    |
| 2020-12     | Internet               | 2555                     | 2170                    |

## 3-) Calculate the success rates of the banks and present them in a graph.
- This analysis has been requested to evaluate and compare the performance of the bank. The success rate of the bank is a measure that indicates how effective its activities such as lending, deposit collection, generating interest income, and risk management are. By comparing the success rate of the bank over time or with other banks in a graph, it is possible to identify the strengths and weaknesses, as well as opportunities and threats of the bank. This analysis can assist the bank in making better decisions in areas such as strategic planning, marketing, customer relations, and competitive advantage.

```sql
select 
	card_type,
	count(case 
		when payment_status = 'Succes-Payment' then 1 end) as total_successful_payment,
	count(*) as total_payments,
		round((count(case 
		when payment_status = 'Succes-Payment' then 1 end) * 1.0 / count(*) * 1.0),2) as bank_success_rate
from payment 
where card_type = 'Credit-Card' and payment_status != 'Return'
group by 1
```
**select card_type, ...:**
This section specifies the columns that the query will select. The "card_type" column and other calculations are the selected columns in this query.

**count(case when payment_status = 'Succes-Payment' then 1 end) as total_successful_payment, ...:**
In this part, it calculates the total count of payments in the "Succes-Payment" status and assigns it to a column named "total_successful_payment." Similarly, it counts the total number of payments and assigns it to a column named "total_payments."

**round((count(case when payment_status = 'Succes-Payment' then 1 end) * 1.0 / count(*) * 1.0), 2) as bank_success_rate:**
This section calculates the success rate. The success rate is the ratio of payments in the "Succes-Payment" status to the total number of payments. It assigns this ratio to a column named "bank_success_rate" and rounds it to 2 decimal places.

**from payment:**
This part specifies the table from which the data will be retrieved. In this case, data is being pulled from the "payment" table.

**where card_type = 'Credit-Card' and payment_status != 'Return':**
This section specifies which payments to select. It includes only payments related to "Credit-Card" type cards and excludes those with a payment status of "Return."

**group by 1:**
This part specifies the criterion for grouping the results. In this case, it groups the results based on the "card_type" column.

# More of our case studies to come!
