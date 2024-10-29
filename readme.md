A CRM APPLICATION FOR LAPTOP RENTALS


## Demonstration

[![Demo Video](https://img.youtube.com/vi/1LPCCrnY71qEdkkGeg8TkLURvzlV1ss-l/0.jpg)](https://drive.google.com/file/d/1LPCCrnY71qEdkkGeg8TkLURvzlV1ss-l/view?usp=drive_link)


1.Project Overview

The CRM Application for Laptop Rentals focuses on efficiently delivering rental items to customers, leveraging customer relationship management (CRM) to improve customer experiences, streamline store operations, and increase overall efficiency. Additionally, the project emphasizes effective CRM practices, specifically through targeted email communication with potential customers.

2.Objectives

Business Goals:
•	Automate the booking and inventory management processes.
•	Enhance customer interaction via automated email notifications.
•	Maintain up-to-date records of rented and available laptops.
•	Provide insightful reports and dashboards to track performance.
•	Implement a structured billing system for rentals.

Specific Outcomes:
•	Track individual laptop rentals, customer details, and billing information.
•	Automate communication via Apex triggers.
•	Enable real-time inventory visibility using roll-up summary fields.
•	Create custom reports and dashboards for data-based insights.

3.Salesforce Key Features and Concepts Utilized

•	Objects Created:
  - Total Laptops: Manages laptop inventory details.
  - Consumer: Stores customer information, including name and email.
  - Laptop Bookings: Manages rental orders.
  - Billing Process: Tracks payment records for rentals.

•	Custom Tabs:
  - Each object (e.g., Consumer, Laptop Bookings) has its tab for easier navigation.
•	Lightning App:
  - A custom Lightning App integrates all objects to streamline the user experience.

•	Validation Rule:	
  - Phone Number Validation ensures only valid numbers in the Consumer object.

•	Profiles & Roles:
  - Owner Profile: Oversees overall operations.
  - Agent Profile: Manages bookings and customer interactions.

•	Role Hierarchy: 
Maintains secure access to customer and booking data.

•	Flows:
•	Automated processes for specific laptop models (Dell, HP, Acer, Mac) using Salesforce Flows.

4.Detailed Steps to Solution Design
Objects Creation and Configuration:
1.	Create Total Laptops Object:
▪	Stores the total inventory of available laptops.
2.	Create Consumer Object:
▪	Manages customer details such as name, email, and phone.
3.	Create Laptop Bookings Object:
▪	Tracks individual laptop rental orders linked to both Consumer and Total Laptops.
4.	Create Billing Process Object:
▪	Manages billing information, including rental charges.
Fields and Relationships:
1.	Consumer Object:
▪	Fields: Name, Email, Phone (with a validation rule for phone number).
2.	Laptop Bookings Object:
▪	Fields: Amount, Core Type, Laptop Type, and a lookup field to Consumer.
3.	Billing Process Object:
▪	Fields: Billing Amount, Payment Status, and Due Date.
4.	Relationships:
▪	Lookup and master-detail relationships between Laptop Bookings, Consumer, and Total Laptops objects.
Validation Rules:
●	Phone Number Validation for Consumer: Ensures valid phone numbers (only digits allowed).

Apex Implementation:
●	Trigger for Email Notification: Sends email to customers upon booking

Trigger Code: 
trigger LaptopBooking on Laptop_Bookings__c (After insert,after update) {

 

    if(trigger.isAfter && ( trigger.isInsert || trigger.isupdate))

    {

    LaptopBookingHandler.sendEmailNotification(trigger.new);

        }

Handler Class Code:
public class LaptopBookingHandler {

    public static void sendEmailNotification (List<Laptop_Bookings__c> lapList){

        for(Laptop_Bookings__c lap:lapList)

        {

            Messaging.SingleEmailMessage email = new Messaging.SingleEmailMessage();

                email.setToAddresses( new List<String>{lap.Email__c});

                email.setSubject('Welcome to our company');

             string body = 'Dear ' +lap.Name +', \n';

             body += 'Welcome to Laptop Rentals! You have been seen as a valuable customer to us.\n Please continue your journey with us, while we try to provide you with good quality resources. \n Laptop Amount = ' + lap.Amount_c + ' \n core type = '+lap.core_typec +' \n Laptop type = '+lap.Laptop_type_c;

             email.setPlainTextBody(body);

                Messaging.sendEmail(new List<Messaging.SingleEmailMessage>{email});


        }

    }

}



Reports and Dashboards Configuration
●	Create a Report:
▪	Report Type: "Consumers with Laptop Bookings and Total Laptops."
▪	Fields: Consumer Name, Booking Amount, Laptop Type, and Core Type.
●	Sharing Report:
▪	Share the report with the Owner Profile to provide visibility into booking trends.
●	Create Dashboard:
▪	Dashboard Folder: Store the dashboards for easy access.
▪	Dashboard Components: Add widgets for total bookings, available laptops, and billing summary.







5.Testing and Validation
Testing Approach:
1.	Unit Testing: Validate that email triggers function correctly.
2.	Functional Testing: Verify that relationships between objects are working.
3.	User Acceptance Testing: Ensure that the system meets user expectations.
Sample Test Cases:
●	Test Case 1: Verify that the email notification is sent after booking.
●	Test Case 2: Check that the roll-up summary field displays the correct count of available laptops.
●	Test Case 3: Ensure that users can only select available laptops during the booking process.


6.Key Scenarios Addressed by Salesforce in the Implementation Project

●	Automated Booking Management:
▪	Automates the booking process and tracks customer interactions.
●	Inventory Tracking:
▪	Ensures real-time visibility of rented and available laptops.
●	Automated Customer Communication:
▪	Sends email notifications for bookings using Apex triggers.
●	Insightful Reporting:
▪	Custom reports and dashboards provide data-driven insights into rental operations.
●	Effective Billing Management:
▪	Tracks payments and billing statuses for each rental.





7.Conclusion

Summary of Achievements:

•	Streamlined Rental Management:
  - Developed a CRM solution to manage laptop rentals effectively.
•	Automated Communication:
  - Strengthened customer engagement through automated emails.
•	Real-Time Inventory Tracking:
  - Facilitated informed decision-making with accurate inventory status.
•	Comprehensive Reporting:
  - Created custom reports and dashboards for operational insights.

This CRM solution for Laptop Rentals has optimized processes, enhanced customer satisfaction, and improved visibility into rental trends and inventory status, offering a scalable, efficient solution for managing laptop rentals.


