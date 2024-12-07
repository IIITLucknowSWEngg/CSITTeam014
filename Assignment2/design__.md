# Software Design Document for PhonePe Application (Clone)

## 1. Title Page

*Project Title:* PhonePe Application Design Document  
*Authors:* [CSITTeam014]  
*Version:* 1.0  
*Date:* [07-12-2024]  

---

## 2. Table of Contents

1. Introduction  
   1.1 Purpose  
   1.2 Scope  
   1.3 Overview  
   1.4 Reference Material  
   1.5 Definitions and Acronyms  
2. System Architecture  
3. Functional Requirements and Design Components  
4. Non-Functional Requirements and Design Components  
5. Data Design  
6. Interface Design  
7. Error Handling and Recovery  
8. Assumptions and Dependencies  
9. Glossary  
10. References  

---

## 1. Introduction

### 1.1 Purpose
This Software Design Document (SDD) provides the detailed design of the PhonePe clone, a digital wallet and payment application. It outlines the system architecture, components, interfaces, and interactions needed to ensure the implementation meets both functional and non-functional requirements. This document serves as a reference to the developers, designers, and stakeholders involved in the development and deployment of the application.

### 1.2 Scope
The PhonePe clone system is a comprehensive platform that allows users to:
- Create digital wallets
- Add and withdraw funds
- Transfer money to other users
- Make online payments
- Recharge mobile phones and DTH services
- Pay utility bills
- Invest in mutual funds
- Purchase insurance policies

The system includes the mobile application (frontend), backend services (server-side), payment processing, security features, and integration with various financial institutions and service providers.

### 1.3 Overview
This document includes a high-level design of the PhonePe clone system. It covers key components like the mobile application, backend API services, user authentication, transaction processing, payment gateways, and integration with external financial systems. Additionally, the document discusses scalability, security, and data management strategies to ensure a reliable, secure, and user-friendly application.

### 1.4 Reference Material
The following materials were referenced during the design of the PhonePe clone:
1. IEEE Std 830-1998 (IEEE Recommended Practice for Software Requirements Specifications)
2. IEEE Std 1016-2009 (IEEE Standard for Software Design Descriptions)
3. PhonePe API Documentation (for payment gateway integration)
4. Financial and regulatory guidelines for secure payment processing
5. Existing design documents and case studies of similar financial applications

### 1.5 Definitions and Acronyms
- **User**: A person who uses the PhonePe clone application for transactions and financial activities.
- **Merchant**: A business entity that accepts payments through the PhonePe clone platform.
- **Admin**: A user with administrative privileges responsible for managing user accounts and overseeing the platform’s operations.
- **API**: Application Programming Interface, used for communication between the mobile application and backend services.
- **UPI**: Unified Payments Interface, a system that facilitates instant payment transfers between banks.
- **DTH**: Direct-to-Home, refers to satellite TV service providers for recharges.
- **Wallet**: A virtual store for users to manage funds and conduct financial transactions in the application.
- **MFA**: Multi-Factor Authentication, a security feature requiring users to verify their identity via multiple methods.
- **SMS/Email Notifications**: Alerts sent to users about transactions, offers, and security updates.
- **QR Code**: A quick response code used to facilitate payments and transactions.

---

## 2. System Architecture

The PhonePe clone follows a multi-layered architecture consisting of three main components:
1. **Presentation Layer**: Mobile application (frontend)
2. **Business Logic Layer**: Backend services (server-side processing)
3. **Data Layer**: Database (stores transaction and user data)

**Diagram:**

![System Architecture](https://github.com/user-attachments/assets/4748ddfd-784e-4fa9-9b9f-fcf4b5723a66)

---

## 3. Functional Requirements and Design Components

### 3.1 User Requirements

#### 3.1.1 Register
- **Actor**: User
- **Precondition**: None
- **Description**: Create a user account to access the system’s features.
- **Design Component**: User Registration Module  
  - Handles user input validation, data storage, and account creation.

**Diagram:**

![User Registration](https://github.com/user-attachments/assets/7d0f94c1-c5fd-4e9e-9c9f-71b64b8e2e98)

#### 3.1.2 Login
- **Actor**: User
- **Precondition**: User must have an existing account.
- **Description**: Allows the user to log into the system.
- **Design Component**: Authentication Module  
  - Manages user sessions, validates credentials, and ensures security.

**Diagram:**

![User Login](https://github.com/user-attachments/assets/96322fbb-0ae1-42ea-a087-081f5ff59932)

#### 3.1.3 Add Money to Wallet
- **Actor**: User
- **Precondition**: Must have a linked payment method.
- **Description**: Add funds to the wallet for transactions.
- **Design Component**: Wallet Management Module  
  - Facilitates linking payment methods and deposit processing.

**Diagram:**

![Add Money to Wallet](https://github.com/user-attachments/assets/3e279b99-4f90-4f1e-9d1c-c68d5fcf9d4f)

#### 3.1.4 Send Money to Contacts
- **Actor**: User
- **Precondition**: Sufficient balance in wallet.
- **Description**: Transfer money to another user.
- **Design Component**: Transaction Processing Module  
  - Manages the fund transfer, recipient validation, and authorization.

**Diagram:**

![Send Money to Contacts](https://github.com/user-attachments/assets/19d25b5d-b330-4e5e-9499-288dc3ac8bc7)

#### 3.1.5 Pay Bills
- **Actor**: User
- **Precondition**: Must have linked bank account or sufficient wallet balance.
- **Description**: Allows the user to pay utility bills.
- **Design Component**: Bill Payment Module  
  - Interfaces with biller APIs and processes payments.

**Diagram:**

![Pay Bills](https://github.com/user-attachments/assets/87bb9b2e-cf1e-4a53-8ac5-639d970be235)

#### 3.1.6 Recharge Mobile
- **Actor**: User
- **Precondition**: Must have wallet balance.
- **Description**: Recharge a mobile phone number through the app.
- **Design Component**: Mobile Recharge Module  
  - Handles recharge plans selection and payment processing.

**Diagram:**

![Recharge Mobile](https://github.com/user-attachments/assets/3c6fd0b8-dcf1-47be-a285-4b209a347acb)

#### 3.1.7 Book Tickets
- **Actor**: User
- **Precondition**: Must have sufficient funds in wallet or linked payment method.
- **Description**: Book tickets for various services.
- **Design Component**: Ticket Booking Module  
  - Manages ticket bookings, payment processing, and confirmations.

**Diagram:**

![Book Tickets](https://github.com/user-attachments/assets/f6f6c158-e730-4c75-a149-6fbb35f8231b)

#### 3.1.8 View Transaction History
- **Actor**: User
- **Precondition**: Must be logged in.
- **Description**: Displays past transaction details.
- **Design Component**: Transaction History Module  
  - Retrieves user transaction history for review.

**Diagram:**

![Transaction History](https://github.com/user-attachments/assets/58cd672f-ff51-40bc-a07b-b62515dbb877)

#### 3.1.9 Raise Dispute
- **Actor**: User
- **Precondition**: Must have a completed transaction.
- **Description**: Allows the user to raise disputes regarding transactions.
- **Design Component**: Dispute Management Module  
  - Facilitates the dispute submission and tracking process.

**Diagram:**

![Raise Dispute](https://github.com/user-attachments/assets/7b84e249-fd9d-4195-92e7-b6185b0c2c29)

---

### 3.2 Merchant Requirements

#### 3.2.1 Accept Payments
- **Actor**: Merchant
- **Precondition**: Merchant must be registered and set up.
- **Description**: Allows the merchant to accept digital payments from users.
- **Design Component**: Merchant Payment Module  
  - Handles payment acceptance through various methods.

**Diagram:**

![Merchant Payment](https://github.com/user-attachments/assets/36a1f9e4-80de-4318-8ec7-f68dff8daecb)

#### 3.2.2 View Payment History
- **Actor**: Merchant
- **Precondition**: Merchant must be registered.
- **Description**: View past payment transactions.
- **Design Component**: Merchant Dashboard Module  
  - Displays payment history and transaction details.

**Diagram:**

![Merchant Dashboard](https://github.com/user-attachments/assets/4d63b5fa-1f2b-41a6-a22c-295b74a4d413)

---

## 4. Non-Functional Requirements and Design Components

### 4.1 Modularity
- **Importance Level**: Critical
- **Design Component**: Modular Architecture Framework

### 4.2 Maintainability
- **Importance Level**: High
- **Design Component**: Code Maintenance Guidelines

### 4.3 Reusability
- **Importance Level**: High
- **Design Component**: Shared Libraries/Components

### 4.4 Testability
- **Importance Level**: High
- **Design Component**: Testing Framework Integration

### 4.5 Documentation
- **Importance Level**: Moderate
- **Design Component**: Documentation Standards

### 4.6 Error Handling
- **Importance Level**: Critical
- **Design Component**: Error Handling Framework

---

## 5. Data Design

### 5.1 Database Schema

The database schema includes core entities like:

- **Users**: Stores user details such as name, contact info, preferences, and balance.
- **Merchants**: Stores merchant business info, transaction history, and ratings.
- **Transactions**: Stores transaction details, such as payer, payee, amount, timestamp, and status.
- **Payments**: Includes payment method details (UPI, card, net banking), success/failure status, and refund information.
- **Bills & Recharges**: Contains data related to bill payments and recharge transactions.
- **Investments**: Stores data about mutual funds, insurance policies, and portfolio details.

---

## 6. Interface Design

### 6.1 Mobile Application (Frontend)

The app will have several screens:
- **Home Screen**: Displays user balance, transaction history, and quick links to features like wallet management and payments.
- **Wallet**: Lets users manage funds (add/withdraw) and view transaction history.
- **Payments**: Displays payment options (UPI, cards, net banking).
- **Recharge & Bills**: Provides mobile recharge and utility bill payment options.
- **Investments**: Shows investment options for mutual funds and insurance.
- **Settings/Support**: Contains user settings and customer support.

### 6.2 API Design

RESTful APIs facilitate communication between the frontend and backend. Key API endpoints:
- **POST /register** - Registers a new user.
- **POST /login** - Authenticates user login.
- **POST /transaction/send** - Sends money to another user.
- **POST /payment/recharge** - Processes mobile recharge.
- **GET /transactions/history** - Fetches user’s transaction history.

**Diagram:**

![API Design](https://github.com/user-attachments/assets/adda3597-7bc2-4c08-8e77-376fb134fa87)

---

## 7. Error Handling and Recovery

The application will include:
- **Error Logging:** For tracking issues and preventing future occurrences.
- **Graceful Recovery:** Mechanisms to ensure continuous operation during failures.
- **User Notifications:** Alerts the user in case of issues like failed transactions or server downtime.

---

## 8. Assumptions and Dependencies

- The system assumes that the user will have access to a stable internet connection.
- The system depends on third-party payment gateways for transaction processing.
- The system assumes the availability of APIs for bill payments and recharge services.
  
---

## 9. Glossary

- **Transaction:** Any movement of funds from one wallet to another.
- **UPI:** Unified Payments Interface, a payment system used for real-time transactions.
- **Merchant:** A business or vendor that accepts payments via the platform.

---

## 10. References

1. [IEEE Software Requirements Specification](https://ieeexplore.ieee.org/document/5547045)
2. [PhonePe API Documentation](https://www.phonepe.com/api)
3. [Payment Gateway Integration Guide](https://www.paypal.com/in/webapps/mpp/merchant)
