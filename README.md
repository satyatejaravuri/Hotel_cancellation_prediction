# Hotel_cancellation_prediction
a machine learning model to identify if the given booking can get cancel or not along with various insights in the hospitality domain.

## Executive Summary

Our goal is to build a model able to classify a booking as canceled or not canceled. In order to do so, we used data from the Hotel Booking Demand Datasets. The dataset provides data from real bookings scheduled to arrive between July, 1st 2015 and August, 31st 2017 from two hotels in Portugal (a resort in the Algarve region (H1) and a hotel in the city of Lisbon (H2)). Booking data from both hotels share the same structure, with 31 variables describing the 40,060 observations of H1 and 79,330 observations of H2. For a detailed list and description of those variables refer to the data dictionary. The two hotel datasets were merged into one main dataframe. The dataframe was then cleaned making sure to address any null values, reformat certain features, and engineer new ones. Exploratory analysis included analysis of the cancellation target variable and its relation with other features. Data visualisation tools were used to identify trends and valuable insights from those analysis. A Random forest Classifier model was then used in order to identify the accuracy of the model. The models were evaluated, and conclusions and recommendations were derived to optimize occupancy, improve operations, and increase a hotel's revenue.


## Quick Problem Overview

1.  Who is our stakeholder? - Booking Manager
2.  What is the core business problem we are solving? - Revenue Management, cost implications due to cancellations.
3.  Convert Business to DS Problem: Determine if a booking will be canceled or not. And what leads to cancellations.
4.  Business Metric: How much Overbookings can we take ( based on reliable cancelation predictions from the model)
5.  Data Science Metric: Recall/ Precision/ F1 Score
6.  Feature Selection: Done
7.  Feature Engineering: Done
8.  EDA Questions: Done

# Problem with Cancellations
  * Customer accustomed to free cancellation policies
  * Operational Problems
  * Non-optimized Occupancy
  * Poor Management
  * Revenue Loss

In order to fight the negative impact of cancellations, hotels need to be able to identify which bookings are likely to be cancelled.

> Here the solution will allow hotels/resorts to predict if a new booking will be cancelled or not, manage their business accordingly, and increase their revenue.


# The Data & Dictionary

From: Property Management System

Bookings are due to arrive between July 01, 2015 and August 31, 2017.

40,060 Hotel 1 (Algarve) | **79,330 **Hotel 2 (Lisbon) | 31 Variables

| Feature Name	 | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `ADR	`      | `Float` |Average Daily Rate. Calculated by dividing the sum of all lodging transactions by the total number of staying nights. |
| Adults		      | Integer	 | Number of adults. |
| Agent			      | Categorical	 | ID of the travel agency that made the booking. |
| ArrivalDateDayOfMonth			      | Integer	 |Day of the month of the arrival date. |
| ArrivalDateMonth			      | Integer	 | Number of adults. |
| Adults		      | Categorical		 | Month of arrival date with 12 categories: “January” to “December”. |
| ArrivalDateWeekNumber			      | Integer	 | Week number of the arrival date. |
| ArrivalDateYear				      | Integer	 | Year of arrival date.  |
| AssignedRoomType				      | Categorical	 | Code for the type of room assigned to the booking. Sometimes the assigned room type differs from the reserved room type due to hotel operation reasons (e.g. overbooking) or by customer request. Code is presented instead of designation for anonymity reasons. |
| Babies			      | Integer	 | Number of babies. |
| ArrivalDateWeekNumber			      | Integer	 | Number of changes/amendments made to the booking from the moment the booking was entered on the Property Management System until the moment of check-in or cancellation. Calculated by adding the number of unique iterations that change some of the booking attributes, namely: persons, arrival date, nights, reserved room type or meal. |
| Children			      | Integer	 | Number of children. Sum of both payable and non-payable children. |
| Company				      | Categorical	 |ID of the company/entity that made the booking or responsible for paying the booking. ID is presented instead of designation for anonymity reasons.  |
| Country			      | Categorical		 | Country of origin. Categories are represented in the International Standards Organization (ISO) 3155–3:2013 format. |
| CustomerType				      | Categorical	 | Type of booking, assuming one of four categories: Contract (when the booking has an allotment or other type of contract associated to it), Group (when the booking is associated to a group), Transient (when the booking is not part of a group or contract, and is not associated to other transient booking), and Transient-party (when the booking is transient, but is associated to at least other transient booking). |
| DaysInWaitingList				      | Integer	 | Number of days the booking was in the waiting list before it was confirmed to the customer. Calculated by subtracting the date the booking was confirmed to the customer from the date the booking entered on the Property Management System. |
| DepositType			      | Categorical	 | Indication on if the customer made a deposit to guarantee the booking. This variable can assume three categories: No Deposit (no deposit was made), Non Refund (a deposit was made in the value of the total stay cost), and Refundable (a deposit was made with a value under the total cost of stay). Value calculated based on the payments identified for the booking in the transaction (TR) table before the booking׳s arrival or cancellation date. In case no payments were found the value is “No Deposit”. If the payment was equal or exceeded the total cost of stay, the value is set as “Non Refund”. Otherwise the value is set as “Refundable”. |
| DistributionChannel			      | Categorical	 | Booking distribution channel. The term “TA” means “Travel Agents” and “TO” means “Tour Operators”. |
| IsCanceled			      | Integer	 | Value indicating if the booking was canceled (1) or not (0).  |
| IsRepeatedGuest			      | Integer	 | Value indicating if the booking name was from a repeated guest (1) or not (0). Variable created by verifying if a profile was associated with the booking customer. If so, and if the customer profile creation date was prior to the creation date for the booking on the Property Management System database it was assumed the booking was from a repeated guest. |
| LeadTime			      | Integer	 | Number of days that elapsed between the entering date of the booking into the Property Management System and the arrival date. Calculated by subtracting the entering date from the arrival date. |
| MarketSegment				      | Categotical	 | Market segment designation. In categories, the term “TA” means “Travel Agents” and “TO” means “Tour Operators”. |
| Meals			      | Categorical	 | Type of meal booked. Categories are presented in standard hospitality meal packages: Undefined/SC (no meal package), BB (Bed & Breakfast), HB (Half board: breakfast and one other meal – usually dinner), and FB (Full board: breakfast, lunch and dinner).  |
| PreviousBookingsNotCanceled			      | Integer	 | Number of previous bookings not canceled by the customer prior to the current booking. In case there was no customer profile associated with the booking, the value is set to 0. Otherwise, the value is the number of bookings with the same customer profile created before the current booking and not canceled.|
| PreviousCancellations				      | Integer	 | Number of previous bookings that were canceled by the customer prior to the current booking. In case there was no customer profile associated with the booking, the value is set to 0. Otherwise, the value is the number of bookings with the same customer profile created before the current booking and canceled. |
| RequiredCarParkingSpaces			      | Integer	 |Number of car parking spaces required by the customer. |
| ReservationStatus			      | Categorical	 | Reservation last status, assuming one of three categories: Canceled (booking was canceled by the customer), Check-Out (customer has checked in but already departed), No-Show (customer did not check-in and did inform the hotel of the reason why). |
| ReservationStatusDate			      | Date	 | Date at which the last status was set. This variable can be used in conjunction with the ReservationStatus to understand when was the booking canceled or when did the customer checked-out of the hotel. |
| ReservedRoomType			      | Categorical	 |Code of room type reserved. Code is presented instead of designation for anonymity reasons.  |
| StaysInWeekendNights			      | Integer	 | Number of weekend nights (Saturday or Sunday) the guest stayed or booked to stay at the hotel. Calculated by counting the number of weekend nights from the total number of nights. |
| StaysInWeekNights				      | Integer	 | Number of week nights (Monday to Friday) the guest stayed or booked to stay at the hotel. Calculated by counting the number of week nights from the total number of nights. |
| TotalOfSpecialRequests			      | Integer	 | Number of special requests made by the customer (e.g. twin bed or high floor). |


# Workflow
* Data Acquisition
* Data Cleaning
* EDA
* Feature Engineering
* Conclusion

## Outcomes

> Percentage of cancelled bookings overall is ~37%
![percentage_booking_per_status](https://github.com/satyatejaravuri/Hotel_cancellation_prediction/assets/31037816/f0c48f51-1dd8-409d-8614-701ea206c99a)



> Features correlated with cancellations

* Lead Time
* Previous Cancellations

![corr_coefficient](https://github.com/satyatejaravuri/Hotel_cancellation_prediction/assets/31037816/c44d003a-ad51-4f8d-a189-63931f976823)

> Lead time booking per status

Days between booking and arrival

* Cancelled bookings have longer average lead time
* More time to cancel
* More time for unexpected events


![lead_time_booking_per_status](https://github.com/satyatejaravuri/Hotel_cancellation_prediction/assets/31037816/4a28c938-8cc1-4724-84e6-cc29bf612fd7)



> Special Requests
 * Canceled bookings have lower average number of special requests.
 * Engagement
 * Communication between customer and hotel


![total_special_requests](https://github.com/satyatejaravuri/Hotel_cancellation_prediction/assets/31037816/9b880f80-1ac9-4eee-853d-c0afacd99539)





> Parking Spaces
  * Cancelled bookings have lower average number of required parking spaces
  * Shows commitment to destination
  * Limit customer hotel opinion


![parking_space_required](https://github.com/satyatejaravuri/Hotel_cancellation_prediction/assets/31037816/19aaf593-7f81-4ec2-b486-f88ebd51efb3)



> Deposit Type
  * Customer who pay a non-refundable deposit have a much higher percentage of cancelled reservations
  * Transient groups who use a travel agent

 
![deposit_type_bookings_cancelled](https://github.com/satyatejaravuri/Hotel_cancellation_prediction/assets/31037816/4b870f56-c402-447a-93b9-8c32629c1bbe)

  * Hotel deposit policies






