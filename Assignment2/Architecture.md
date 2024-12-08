# 7.1 : System Context  Diagram Code

![image](https://github.com/user-attachments/assets/1f5019a1-eedb-4537-98cf-a4ae03837e61)


```plantuml
@startuml
   title C4 Model: System Context Diagram - PhonePe Competitor

    ' External Actors
    actor "End User" as User
    actor "Merchant" as Merchant
    actor "Admin" as Admin
    actor "Payment Gateway" as PaymentGateway
    actor "Notification Service" as NotificationService
    actor "Customer Support" as CustomerSupport
    actor "Banking System" as BankingSystem

    ' System Boundary: PhonePe Clone
    package "PhonePe Competitor" {

        ' Subsystems
        rectangle "End User Registration and Authentication" as Registration
        rectangle "Transaction Management" as TransactionManagement
        rectangle "Payment Gateway Integration" as PaymentGatewayIntegration
        rectangle "Merchant Services" as MerchantServices
        rectangle "Push Notifications" as PushNotifications
        rectangle "In-App Chat \nand Support" as ChatSupport
        rectangle "Admin Panel" as AdminPanel
    }

    ' Relationships between actors and system components
    User --> Registration : Sign Up/Login
    User --> TransactionManagement : Make Payment
    User --> PushNotifications : Receive Notifications
    User --> ChatSupport : In-App Chat End User with Support

    Merchant --> TransactionManagement : Process Payment
    Merchant --> MerchantServices : Manage Business Profile
    Merchant --> PushNotifications : Receive Payment Notifications
    Merchant --> ChatSupport : In-App Chat with Merchant with support

    Admin --> AdminPanel : Manage End Users/Merchants/Transactions
    Admin --> TransactionManagement : Monitor Transactions
    Admin --> PushNotifications : Send Notifications

    ' External Interactions
    TransactionManagement --> PaymentGateway : Process Payment Transactions
    PushNotifications --> NotificationService : Send Notifications
    ChatSupport --> CustomerSupport : Handle End User Issues
    TransactionManagement --> BankingSystem : Bank Transfers/Settlement

@enduml
```

# Container Diagram
## 7.2 : End User
![image](https://github.com/user-attachments/assets/57efbe64-f14d-4c79-8775-d454ad36701b)

```plantuml
@startuml
!define RECTANGLE rectangle
!define BOLD **<color:Black>**

title C4 Model - Container Diagram (End User) - PhonePe Clone

' Add primary containers
' End User-facing applications
RECTANGLE "Mobile App" as mobileApp <<Mobile Application>>
RECTANGLE "Web App" as webApp <<Web Application>>
RECTANGLE "End User API Gateway" as endUserGateway <<API Gateway>>

' Backend services
RECTANGLE "Transaction Service" as transactionService <<Microservice>> 
RECTANGLE "End User Service" as endUserService <<Microservice>>
RECTANGLE "Bill Payment Service" as billService <<Microservice>>
RECTANGLE "Investment Service" as investmentService <<Microservice>>
RECTANGLE "Insurance Service" as insuranceService <<Microservice>> 
RECTANGLE "Notification Service" as notificationService <<Microservice>>
RECTANGLE "Chat Service" as chatService <<Microservice>>

' Database containers
RECTANGLE "Transaction Database" as transactionDB <<Database>> 
RECTANGLE "End User Database" as endUserDB <<Database>> 
RECTANGLE "Bill Payment Database" as billDB <<Database>>
RECTANGLE "Investment Database" as investmentDB <<Database>> 
RECTANGLE "Insurance Database" as insuranceDB <<Database>> 

' External systems
RECTANGLE "Bank/UPI System" as bankSystem <<External System>> 
RECTANGLE "Third-Party Billers" as billers <<External System>> 
RECTANGLE "Push Notification Service" as pushNotification <<External System>>
RECTANGLE "Customer Support System" as customerSupport <<External System>>


' Relationships between containers
mobileApp --> endUserGateway : "API Calls"
webApp --> endUserGateway : "API Calls"
endUserGateway --> transactionService : "Manage Transactions"
endUserGateway --> endUserService : "Manage End User Data"
endUserGateway --> billService : "Manage Bill Payments"
endUserGateway --> investmentService : "Manage Investments"
endUserGateway --> insuranceService : "Manage Insurance Policies"
endUserGateway --> notificationService : "Send Notifications"
endUserGateway --> chatService : "In-App Chat"


transactionService --> transactionDB : "Read/Write Data"
endUserService --> endUserDB : "Read/Write Data"
billService --> billDB : "Read/Write Data"
investmentService --> investmentDB : "Read/Write Data"
insuranceService --> insuranceDB : "Read/Write Data"

transactionService --> bankSystem : "Process UPI Transactions"
billService --> billers : "Communicate with Billers"
notificationService --> pushNotification : "Send Push Notifications"
chatService --> customerSupport : "Escalate Issues"

@enduml


```
## 7.3 : Merchant
![image](https://github.com/user-attachments/assets/26ba55b4-3194-4d68-898d-8606d8ee28d6)
```plantuml
@startuml
!define RECTANGLE rectangle
!define BOLD **<color:Black>**

title C4 Model - Container Diagram (Merchant) - PhonePe Competitor

' Add primary containers
' Merchant-facing application
RECTANGLE "Merchant App" as merchantApp <<Mobile Application>>
RECTANGLE "Merchant Web" as merchantWeb <<Web Application>>

' API Gateway
RECTANGLE "Merchant API Gateway" as merchantGateway <<API Gateway>>

' Backend services
RECTANGLE "Merchant Service" as merchantService <<Microservice>>
RECTANGLE "Transaction Service" as transactionService <<Microservice>>
RECTANGLE "Notification Service" as notificationService <<Microservice>>
RECTANGLE "Chat Service" as chatService <<Microservice>>

' Database containers
RECTANGLE "Merchant Database" as merchantDB <<Database>>
RECTANGLE "Transaction Database" as transactionDB <<Database>>

' External systems
RECTANGLE "Banking System" as bankingSystem <<External System>>
RECTANGLE "Payment Gateway" as paymentGateway <<External System>>
RECTANGLE "Push Notification Service" as pushNotification <<External System>>
RECTANGLE "Customer Support System" as customerSupport <<External System>>

' Relationships between containers
merchantApp --> merchantGateway : "API Calls"
merchantWeb --> merchantGateway : "API Calls"
merchantGateway --> merchantService : "Manage Merchant Profile"
merchantGateway --> transactionService : "Track Transactions"
merchantGateway --> notificationService : "Send Payment Notifications"
merchantGateway --> chatService : "In-App Chat"

merchantService --> merchantDB : "Read/Write Data"
transactionService --> transactionDB : "Read/Write Data"

transactionService --> bankingSystem : "Bank Settlements"
transactionService --> paymentGateway : "Process Payments"
notificationService --> pushNotification : "Send Notifications"
chatService --> customerSupport : "Escalate Issues"

@enduml

```
## 7.4 : Admin
![image](https://github.com/user-attachments/assets/23148d7b-dbb6-44f0-9b1c-b89b561a0678)
```plantuml
@startuml
!define RECTANGLE rectangle
!define BOLD **<color:Black>**

title C4 Model - Container Diagram (Admin) - PhonePe Competitor

' Add primary containers
' Admin-facing web application
RECTANGLE "Admin Web Panel" as adminWebPanel <<Web Application>>
RECTANGLE "Admin App Panel" as adminAppPanel <<App Application>>
' API Gateway
RECTANGLE "Admin API Gateway" as adminGateway <<API Gateway>>

' Backend services
RECTANGLE "Admin Service" as adminService <<Microservice>>
RECTANGLE "Transaction Service" as transactionService <<Microservice>>
RECTANGLE "Notification Service" as notificationService <<Microservice>>
RECTANGLE "Chat Service" as chatService <<Microservice>>

' Database containers
RECTANGLE "Admin Database" as adminDB <<Database>>
RECTANGLE "Transaction Database" as transactionDB <<Database>>

' External systems
RECTANGLE "Banking System" as bankingSystem <<External System>>
RECTANGLE "Push Notification Service" as pushNotification <<External System>>
RECTANGLE "Customer Support System" as customerSupport <<External System>>

' Relationships between containers
adminWebPanel --> adminGateway : "API Calls"
adminAppPanel --> adminGateway : "API Calls"
adminGateway --> adminService : "Manage End Users/Merchants"
adminGateway --> transactionService : "Monitor Transactions"
adminGateway --> notificationService : "Send Notifications"
adminGateway --> chatService : "Handle Support Issues"

adminService --> adminDB : "Read/Write Data"
transactionService --> transactionDB : "Read/Write Data"

transactionService --> bankingSystem : "Monitor Bank Settlements"
notificationService --> pushNotification : "Send Notifications"
chatService --> customerSupport : "Escalate Issues"

@enduml

```
# Component Diagram
## 7.5 : End User
![image](https://github.com/user-attachments/assets/52772aa0-ea34-46c2-b2e6-9f11638ac9bd)

```plantuml
@startuml
title C4 Model - Component Diagram (End User) - PhonePe Competitor
' External Actors
actor "End User" as EndUser
actor "Merchant" as Merchant
actor "Payment Gateway" as PaymentGateway
actor "Notification Service" as NotificationService
actor "Customer Support" as CustomerSupport
actor "Banking System" as BankingSystem

' System Boundary: PhonePe Competitor
package "PhonePe Competitor" {

    ' Subsystems related to EndUser
    rectangle "End User Registration \nand Authentication" as EndUserRegistration
    rectangle "Transaction Management" as EndUserTransactionManagement
    rectangle "Payment Gateway Integration" as EndUserPaymentGatewayIntegration
    rectangle "Push Notifications" as EndUserPushNotifications
    rectangle "In-App Chat \nand Support" as EndUserChatSupport
}

' Relationships between EndUser and system components
EndUser --> EndUserRegistration : Sign Up/Login
EndUser --> EndUserTransactionManagement : Make Payment
EndUser --> EndUserPaymentGatewayIntegration : Process Payment
EndUser --> EndUserPushNotifications : Receive Notifications
EndUser --> EndUserChatSupport : In-App Chat with Support

' External Interactions
EndUserTransactionManagement --> PaymentGateway : Process Payment Transactions
EndUserPushNotifications --> NotificationService : Send Notifications
EndUserChatSupport --> CustomerSupport : Handle End User Issues
EndUserTransactionManagement --> BankingSystem : Bank Transfers

@enduml

```
## 7.6 : Merchant
![image](https://github.com/user-attachments/assets/084633d9-6aab-4374-a083-5abbfd296f6b)


```plantuml
@startuml

title C4 Model - Component Diagram (Merchant) - PhonePe Competitor

' External Actors
actor "Merchant" as Merchant
actor "Payment Gateway" as PaymentGateway
actor "Notification Service" as NotificationService
actor "Customer Support" as CustomerSupport
actor "Banking System" as BankingSystem

' System Boundary: PhonePe Competitor
package "PhonePe Competitor" {

    ' Subsystems related to Merchant
    rectangle "Merchant Profile Management" as MerchantProfile
    rectangle "Transaction Management" as MerchantTransactionManagement
    rectangle "Push Notifications" as MerchantPushNotifications
    rectangle "In-App Chat \nand Support" as MerchantChatSupport
}

' Relationships between Merchant and system components
Merchant --> MerchantProfile : Manage Profile
Merchant --> MerchantTransactionManagement : Process Payment
Merchant --> MerchantPushNotifications : Receive Notifications
Merchant --> MerchantChatSupport : In-App Chat with Merchant with Support

' External Interactions
MerchantTransactionManagement --> PaymentGateway : Process Payment Transactions
MerchantPushNotifications --> NotificationService : Send Notifications
MerchantChatSupport --> CustomerSupport : Handle Merchant Issues
MerchantTransactionManagement --> BankingSystem : Bank Transfers

@enduml

```
## 7.7 : Admin
![image](https://github.com/user-attachments/assets/0249364a-7877-4be6-9524-97a7143fd54e)

```plantuml
@startuml

' Define the system components for the Admin Panel
title C4 Model - Component Diagram (Admin) - PhonePe Competitor

package "Admin Panel" {
    component "Dashboard" as Dashboard
    component "End User Management" as UserManagement
    component "Merchant Management" as MerchantManagement
    component "Transaction Monitoring" as TransactionMonitoring
    component "Payment Management" as PaymentManagement
    component "Analytics and Reports" as AnalyticsReports
    component "Notification Management" as NotificationManagement
}

' External services used by the Admin Panel
database "End User Database" as UserDB
database "Merchant Database" as MerchantDB
database "Transaction Database" as TransactionDB
database "Payment Database" as PaymentDB
component "Notification Service" as NotificationService
component "Payment Gateway" as PaymentGateway

' Relationships between Admin Panel components
Dashboard --> UserManagement : Access End User Data
Dashboard --> MerchantManagement : Access Merchant Data
Dashboard --> TransactionMonitoring : Monitor Transactions
Dashboard --> PaymentManagement : View Payment Info
Dashboard --> AnalyticsReports : Generate Reports
Dashboard --> NotificationManagement : Send Notifications

' Internal component interactions
UserManagement --> UserDB : Read/Write End User Data
MerchantManagement --> MerchantDB : Read/Write  Merchant Data
TransactionMonitoring --> TransactionDB : Access Transaction Data
PaymentManagement --> PaymentDB : Access Payment Data
AnalyticsReports --> UserDB : Generate End User Reports
AnalyticsReports --> MerchantDB : Generate Merchant Reports
AnalyticsReports --> TransactionDB : Generate Transaction Reports
AnalyticsReports --> PaymentDB : Generate Payment Reports

' External interactions
PaymentManagement --> PaymentGateway : Process Payment Refunds
NotificationManagement --> NotificationService : Send Notifications to End Users

@enduml

```

# 7.8 : Deployment Diagram Code

![image](https://github.com/user-attachments/assets/0b21f083-c370-45e8-a4fa-d8a4e78cfe16)

```plantuml
@startuml
title C4 Model - Deployment Diagram - PhonePe Competitor System

node "End User's Mobile Device" {
    [End User Mobile App] <<Mobile App>>
}

node "Merchant's Mobile Device" {
    [Merchant Mobile App] <<Mobile App>>
}

node "Admin's PC" {
    [Admin Web Dashboard] <<Web App>>
}

node "Web Server" {
    [Transaction Service] <<Microservice>>
    [End User Service] <<Microservice>>
    [Payment Service] <<Microservice>>
    [Merchant Service] <<Microservice>>
    [Notification Service] <<Microservice>>
}

node "Database Server" {
    database "End User Database" as UserDB
    database "Merchant Database" as MerchantDB
    database "Transaction Database" as TransactionDB
    database "Payment Database" as PaymentDB
}

cloud "Third-Party Services" {
    [Payment Gateway] <<External Service>>
    [Push Notification Service] <<External Service>>
    [Banking System] <<External Service>>
}

' Connections
[End User Mobile App] --> [Transaction Service] : "Request transactions"
[End User Mobile App] --> [Payment Service] : "Process payment"
[End User Mobile App] --> [Notification Service] : "Receive notifications"
[End User Mobile App] --> [End User Service] : "Manage profile"

[Merchant Mobile App] --> [Payment Service] : "Process payment"
[Merchant Mobile App] --> [Transaction Service] : "Request transactions"
[Merchant Mobile App] --> [Notification Service] : "Receive notifications"
[Merchant Mobile App] --> [Merchant Service] : "Manage profile"

[Admin Web Dashboard] --> [Transaction Service] : "Monitor transactions"
[Admin Web Dashboard] --> [End User Service] : "Manage End Users"
[Admin Web Dashboard] --> [Merchant Service] : "Monitor merchants"
[Admin Web Dashboard] --> [Notification Service] : "Send notifications"

[Transaction Service] --> UserDB : "Read/Write End User data"
[Transaction Service] --> MerchantDB : "Read/Write Merchant data"
[End User Service] --> UserDB : "Manage End User data"
[Payment Service] --> PaymentDB : "Read/Write payment data"
[Merchant Service] --> MerchantDB : "Manage merchant data"
[Merchant Service] --> PaymentDB : "Process merchant payments"
[Transaction Service] --> TransactionDB : "Read/Write transaction data"

[Payment Service] --> [Payment Gateway] : "Process payment"
[Notification Service] --> [Push Notification Service] : "Send push notifications"
[Transaction Service] --> [Banking System] : "Bank Transfers"

@enduml

```
