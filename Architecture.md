# System Context  Diagram Code

<img width="1418" alt="System Context" src="https://www.planttext.com/api/plantuml/png/X5NBRjim4BpdAnQ-z6JudaCHsoXQ0tLXMCsj5qPUIuIbfK1ISOsYNzP3Fwc_K3v4cvGO9vU8kpkhsPqH_U_FNp1_JqepgVksUNYmnm_mwQT6IQo1PQc5L2xAx2FCdXNA6J05zY5ER56MDIFjak4G5omFBIUNTKznQiSkBPA6pqpZcLrSqH0RGd7rDw7vaPTCSq5Ge7pb9Jf8d1ZYCMxTAorQb53qNIUaPng2GookNp4wSQgWk2YDhQiUGZuIjkLFi18z7PYyFCAk5eGxX7LZ_hkYZfKdLg6PD4xDu9VlCVJfNvHhfQv1YQLcL3Ne5mzxhBZIqe_-WnWTODdhsknf6DknZAjohRvBHieCQPji6HbYTjCE6gLkcLoFaMIm8OsLl758vOkokMR1Ba5DbPWe1BCqUbKdkdke3IVH77P3ysNNmRfcUjXbOWmJZaqn0ZiFcoa9cvkdtT5L_mxcs6FZ6TIyK_22-en8tc4Ax3kzv52AjZEM8EsfEhNdyu-fuezGy8hWkLjy5TNm2Lqhiz8Po9QTCCYH8YPRCjLxB96_8aotTuL5cp60U8jdhkkmHB-0gxBt6EwaCFAgX6G273l1JMKRmAfNd1nMYYDlS8gzDsGmyNJOfCKx0zl5B9AflJaiz6QB6sTRhnRX3MeHhKMDu6zgAeZRE-eED3TtWSPmwR3Z6zz-gJBkcAVWtf1yubCTf-ocd6oVpBMTvsfRn5euRTBxsm2_cA-gyLk6ZL8zlZT7SgcR1lRiouzMg0ArRlmzw1ez6MBsj_8_0000__y30000">

```plantuml
@startuml

    ' External Actors
    actor "User" as User
    actor "Merchant" as Merchant
    actor "Admin" as Admin
    actor "Payment Gateway" as PaymentGateway
    actor "Notification Service" as NotificationService
    actor "Customer Support" as CustomerSupport
    actor "Banking System" as BankingSystem

    ' System Boundary: PhonePe Clone
    package "PhonePe Clone" {

        ' Subsystems
        rectangle "User Registration \nand Authentication" as Registration
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
    User --> ChatSupport : In-App Chat with Support

    Merchant --> TransactionManagement : Process Payment
    Merchant --> MerchantServices : Manage Business Profile
    Merchant --> PushNotifications : Receive Payment Notifications
    Merchant --> ChatSupport : In-App Chat with User/Support

    Admin --> AdminPanel : Manage Users/Merchants/Transactions
    Admin --> TransactionManagement : Monitor Transactions
    Admin --> PushNotifications : Send Notifications

    ' External Interactions
    TransactionManagement --> PaymentGateway : Process Payment Transactions
    PushNotifications --> NotificationService : Send Notifications
    ChatSupport --> CustomerSupport : Handle User Issues
    TransactionManagement --> BankingSystem : Bank Transfers/Settlement

@enduml
```

# Container Diagram
## User
## Merchant
![container-diagram-Merchant](https://www.planttext.com/api/plantuml/png/b5NDZjem4BxdALnwg8I4zeuGMW9eLMdP8jXgpvDa21QE4zccb6VheO_KL-Zatmw1XHFAp7pV_7mpvj-Vly_QW3B7H7XV8jnnYMopdB_FtbvUbqnXQ4360XkV_-DrmOR3IPYAL8rz0U5XEXnwdk5689kdqW25ARRW42j8s8Yjzwd4DVa4_NhUDpQB8fOfde0wix06Q7Byr0JKb9AdqckB6ApIW1FvBCi633HBYa_wOfD9wn8yX1mudRAlWiTx4uWZsYmV63GK9mnAV6Ny55oKDbj_PozWy0JdWkL8nkgRg2olIqET-JGcb14rftxn4BLD_Qv0QYYQPjlINx2RrbwPytvvgDAAfSaIAqHvKQtDbLVwACaQpWbAu_1afUrHghVKy5qrOeTFMev7ILUemZrq2amgurra9Cm230IWqLx4AzhKeLrn5ZvbgPrDXZCAaPukH758SbNkHTTgE0IL73SvgCdbRuDAWc3wh0qcJeUDhv6xY77KBYoKeeajBNccZCk3K-PHxzbLkJFoEiwxE7sG1ovZkxAWD7rQ6JM_GL7aqdkU4H3DYQItvMwVaz5ewjpqc0toevw347hWLM_6xI3RaqVs7341LY0XHcPjLm_KljaMqspH9Q1pd8HPgvGU6rrhsvEaxm09kCqVArkf7cZtrDeQwyiaaDSpWCvSQ7i9ka68dZuKDsXrPoEgO-aBxJHkpU8Au0QYMgdUuNKxlZtqvdrg2VgcNP1qxwAMuEASRepKlObnUJVbZkrepv-sQEWlEg-4E9w9FV_B_my00F__0m00)
```plantuml
   @startuml
   !define RECTANGLE rectangle
!define BOLD **<color:Black>**

title Container Diagram - PhonePe Clone

' Add primary containers
' User section
RECTANGLE "Mobile App" as mobileApp <<Mobile Application>> #lightblue
RECTANGLE "Web App" as webApp <<Web Application>> #lightblue
RECTANGLE "User API Gateway" as userGateway <<API Gateway>> #lightblue

' Backend services
RECTANGLE "Transaction Service" as transactionService <<Microservice>> #lightgreen
RECTANGLE "User Service" as userService <<Microservice>> #lightgreen
RECTANGLE "Payment Service" as paymentService <<Microservice>> #lightgreen
RECTANGLE "Notification Service" as notificationService <<Microservice>> #lightgreen
RECTANGLE "Merchant Service" as merchantService <<Microservice>> #lightgreen

' Database containers
RECTANGLE "Transaction Database" as transactionDB <<Database>> #lightyellow
RECTANGLE "User Database" as userDB <<Database>> #lightyellow
RECTANGLE "Payment Database" as paymentDB <<Database>> #lightyellow

' External systems
RECTANGLE "External Payment System" as paymentSystem <<External System>> #pink
RECTANGLE "Push Notification Service" as pushNotification <<External System>> #pink
RECTANGLE "Banking System" as bankingSystem <<External System>> #pink

' Relationships between containers
mobileApp --> userGateway : "API Calls"
webApp --> userGateway : "API Calls"
userGateway --> transactionService : "Manage Transactions"
userGateway --> userService : "Manage User Data"
userGateway --> paymentService : "Process Payments"
userGateway --> notificationService : "Send Notifications"
userGateway --> merchantService : "Manage Merchants"

transactionService --> transactionDB : "Read/Write Data"
userService --> userDB : "Read/Write Data"
paymentService --> paymentDB : "Read/Write Data"

paymentService --> paymentSystem : "Process Payments"
merchantService --> paymentService : "Process Merchant Payments"
notificationService --> pushNotification : "Send Push Notifications"

transactionService --> bankingSystem : "Bank Transfers/Settlement"

@enduml
```
## Admin

# Component Diagram
## User
![Component_Diagram_User](https://www.planttext.com/api/plantuml/png/X5H1Rjim4Bph5GjVUZ9wpw68OnIjWRemxFJMoqRUI8GbKY1NSOoYB-kXJ-eNkXJ5X9GSn1T9kpFZdLbH__xylNMCblksAOeFyFcPoMfiO5MoiQv0Vu753qTs0UZ0tyJYbcnPe-QX4HzYSuUNbZJ35sGwusN0ZBMn597V3Qj7LI8he-50zacLDC3JnbYFd7NlsBHauT1tdR5XX5WSQn5xX_gaT0M7YsDg1-HO2XLlEzp1dUdr4Utb1dQrqRGZM3ToBJeiJrYHk4hB2_XL520_uVSFRf1mOAaHVqTW4yBo04ibewuQ2ad2dYhbs0RBFpNg8wnwhYMRqUvBrYboAdLlKJinwKMsg6L0d-uBDMc_TgSQapN1HZDLDfyXNrk2c8drhiwsvburf9LrfjoDNgww3jOryfX8kbeluLjnjR_zqlO-QQzLgyx10_6PI0zGyFom42XDsycoDBjYQ2sNdsR9mWqSL2NSxkCtKocT8wy6APGjdYY-qpdZpSI4jREc9EVU84vZ4iAUIb9Fb0URqv9eX916ULPSnoIpy-s7ii5K4Blkqlz3xcPk0H9gq9hRy3fNphCFdcHNSs-f9K-U76uXVfKbovip1B5nhgVtV6IdNWJySvZzaUHJLzpA9Fup-1y00F__0m00)
```plantuml
@startuml

' External Actors
actor "User" as User
actor "Merchant" as Merchant
actor "Payment Gateway" as PaymentGateway
actor "Notification Service" as NotificationService
actor "Customer Support" as CustomerSupport
actor "Banking System" as BankingSystem

' System Boundary: PhonePe Clone
package "PhonePe Clone" {

    ' Subsystems related to User
    rectangle "User Registration \nand Authentication" as UserRegistration
    rectangle "Transaction Management" as UserTransactionManagement
    rectangle "Payment Gateway Integration" as UserPaymentGatewayIntegration
    rectangle "Push Notifications" as UserPushNotifications
    rectangle "In-App Chat \nand Support" as UserChatSupport
}

' Relationships between User and system components
User --> UserRegistration : Sign Up/Login
User --> UserTransactionManagement : Make Payment
User --> UserPaymentGatewayIntegration : Process Payment
User --> UserPushNotifications : Receive Notifications
User --> UserChatSupport : In-App Chat with Support

' External Interactions
UserTransactionManagement --> PaymentGateway : Process Payment Transactions
UserPushNotifications --> NotificationService : Send Notifications
UserChatSupport --> CustomerSupport : Handle User Issues
UserTransactionManagement --> BankingSystem : Bank Transfers

@enduml
```
## Merchant
![Component_Diagram_Merchant](https://www.planttext.com/api/plantuml/png/Z5JBRjim4BphAnQ-z6JqdaEHn2XQ7r88SNFBPKElBIBIKY1NSOqWNzP3Foc_aAKbMWyhG7MHj3ipv0orUl_xxpe8UccgCik-mFS_GfwnX1iZpeSCumqMT-HDWImBm03f9JLpF5R40ZzGw8374wQhTQM4_EN4xgn1iOvXG_x56Zh1XuskdZYh9eYhoCEcgMldsosaObTBs5laPyjxs1o3K7L2TgMs4XssJt3h6jwYFrv1NZYcd61LwZshqJpZdjJLiBo0rom3lPJVF8MJH01FfVhRWhW-amZoP0HvNr8V7EJUxQnMxf1LFcOpoh9hJ-c_FN9GSp6lJvW3I8-OwkHDA4OXX_7gsXvrf_mrBs_g6bO52ZmoydPq6aacjjE9lCMixsD0KQ-mTO0daWCHd-4GTTeimRYgrfnPGdPkBvVVfld0LHT3odCUFPk9SfLaA9o_pa-MceQXn7ioP5ze7E4yVH224eV17QmKy138VqqX3GTkpVhGxhbNdZSIbniFsAKt651xlKjlKMjc-bHmGteyyuQ77gF0P1oL_5FFDdxjAQ5r20tzZw_HlAfGV6-zx4Z_HzcrxYh-gpu0003__mC0)

```plantuml
@startuml

' External Actors
actor "Merchant" as Merchant
actor "Payment Gateway" as PaymentGateway
actor "Notification Service" as NotificationService
actor "Customer Support" as CustomerSupport
actor "Banking System" as BankingSystem

' System Boundary: PhonePe Clone
package "PhonePe Clone" {

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
Merchant --> MerchantChatSupport : In-App Chat with User/Support

' External Interactions
MerchantTransactionManagement --> PaymentGateway : Process Payment Transactions
MerchantPushNotifications --> NotificationService : Send Notifications
MerchantChatSupport --> CustomerSupport : Handle Merchant Issues
MerchantTransactionManagement --> BankingSystem : Bank Transfers

@enduml
```
## Admin
<img width="1414" alt="Component Diagram - Admin" src="https://www.planttext.com/api/plantuml/png/V9N1Rjim38RlUWeYbvwAtNSeci93qKEB8EssCsFJZT1O2YHbcL7qoNRO8-qLHYkoGyjESnF9dwG-_KR-_VbxwmEwS6XsIbr1GRKs165Bu5iVg87IDdjho0GFjNKniwmQRM25XdPgZ-KRlX8iH701xmhuDqXXKQ3VRYowQW7eOJZbPTyzENX4mnqR3iJYBdOEvOeNXyPZ6RGry6YD3jPfyng58dNEvFeLjbtRV6WANvwxDBXhWouzeAbWJNlhWe_I8PE2kVB91bth4ayhZyVAd9ZzqJtDjz-17FS6vl5Bb-JXuAc2JJjvame3Rj1Jubcauq2pk1Cb4k2eKYH6WfxOg3W5kV3IJPzFMq-kcU9gvatkCT0HMpaWXJeUQzh51dwhznus58v4Hd8GrbM3u-3w-YQp57o5PSayJt3YlRBwMIUnB1raFXyrCHBBVcWwzWbuCBNDDBc3M79FXXpVlNTQffZt3UkUYTqfixv3zs2IbSxGTHVghv3nwP4LTznnJLXz-UaqxtB6DGyeGnVbYNJkEZNb9EX9fRIVcf0QhJf0Yulsv6Or-Pg3L2xwQGUvwg3kb-sLyZCU4V_q-idqt7Zbx0Z2ckg3gRowyFwvDTAtDkiB23PouYLlETdz7_m7003__mC0">

```plantuml
@startuml

' Define the system components for the Admin Panel
package "Admin Panel" {
    component "Dashboard" as Dashboard
    component "User Management" as UserManagement
    component "Transaction Monitoring" as TransactionMonitoring
    component "Payment Management" as PaymentManagement
    component "Analytics and Reports" as AnalyticsReports
    component "Notification Management" as NotificationManagement
}

' External services used by the Admin Panel
database "User Database" as UserDB
database "Transaction Database" as TransactionDB
database "Payment Database" as PaymentDB
component "Notification Service" as NotificationService
component "Payment Gateway" as PaymentGateway

' Relationships between Admin Panel components
Dashboard --> UserManagement : Access User Data
Dashboard --> TransactionMonitoring : Monitor Transactions
Dashboard --> PaymentManagement : View Payment Info
Dashboard --> AnalyticsReports : Generate Reports
Dashboard --> NotificationManagement : Send Notifications

' Internal component interactions
UserManagement --> UserDB : Read/Write User Data
TransactionMonitoring --> TransactionDB : Access Transaction Data
PaymentManagement --> PaymentDB : Access Payment Data
AnalyticsReports --> UserDB : Generate User Reports
AnalyticsReports --> TransactionDB : Generate Transaction Reports
AnalyticsReports --> PaymentDB : Generate Payment Reports

' External interactions
PaymentManagement --> PaymentGateway : Process Payment Refunds
NotificationManagement --> NotificationService : Send Notifications to Users

@enduml
```

# Deployment Diagram Code

![Deployment Diagram](https://www.planttext.com/api/plantuml/png/b5PDZzCm4BtxLunosLF57QsgtMtHdeeY2je3uZ1Dfer5OWVRALI8NyQ1dyHVm7RYjFbmo_PITUQzvtapOwj_V_zvq0QLQQgI6MvAWZNLfJnL90oiEHuKLh20j922Ke9LQRzXUzA6AiQ4p0cIJvhKdOQDt75FF_AC4lZ9m7u-ksH8FTRr5xY_F_zQBjcleB8XbHKeJ5Gf0FvBxJ6lkB1IwQhd-n2yq0xMg8kTH9KxlWkCo2wq9NKarPC_AXGQCyEby2bRc3-SPqhgzhTLE3k-WKcnRV0DM6_v1kwzD7pFCxnHNczmZGPtg6daCWzXFr88g0HGWukidqQmowuCq1U92Ibu7n2we0NR8hDIDhbLBxZA5wbTpbCmfVk119LdDFGTJyxjkn-6bC0oWFjcDxg0M8jYf2SKNxauTAiUGTfQxs0bXI1lLRFfkYyMoyZsl8Na0trhI1imvxnEOYAJdR42gPAsAHhgDXVbphlt5MJ4ZmJY0X0lORZQbhv1WGU2MiczHIQCpTzIJvukywo1kC2hJRoobgcPsIVZwaGtKd0ZrNYYSQ5OIniRlywSzz2TNtN9wnBHZcv9vEDsiddJJgXz7DfHOFxcHN7JEl3NtfOmsLt7wk_yYDZjGk1EVGwFx1eM75-d3SuCozTJkvDTqw9U1q_RgFABgNTbHAnFdw_Pkp0_drOW_gY5-TKEChuJKL-J5y_Ak51hUE-taJrONVTFuHy0003__mC0)
```plantuml
@startuml
title Deployment Diagram - PhonePe Clone System

node "User's Mobile Device" {
    [User Mobile App] <<Mobile App>>
}

node "Merchant's Mobile Device" {
    [Merchant Mobile App] <<Mobile App>>
}

node "Admin's PC" {
    [Admin Web Dashboard] <<Web App>>
}

node "Web Server" {
    [Transaction Service] <<Microservice>>
    [User Service] <<Microservice>>
    [Payment Service] <<Microservice>>
    [Merchant Service] <<Microservice>>
    [Notification Service] <<Microservice>>
}

node "Database Server" {
    database "User Database" as UserDB
    database "Transaction Database" as TransactionDB
    database "Payment Database" as PaymentDB
}

cloud "Third-Party Services" {
    [Payment Gateway] <<External Service>>
    [Push Notification Service] <<External Service>>
    [Banking System] <<External Service>>
}

' Connections
[User Mobile App] --> [Transaction Service] : "Request transactions"
[User Mobile App] --> [Payment Service] : "Process payment"
[User Mobile App] --> [Notification Service] : "Receive notifications"
[User Mobile App] --> [User Service] : "Manage profile"

[Merchant Mobile App] --> [Merchant Service] : "Process payment"
[Merchant Mobile App] --> [Notification Service] : "Receive notifications"
[Merchant Mobile App] --> [Merchant Service] : "Manage profile"

[Admin Web Dashboard] --> [Transaction Service] : "Monitor transactions"
[Admin Web Dashboard] --> [User Service] : "Manage users"
[Admin Web Dashboard] --> [Merchant Service] : "Monitor merchants"
[Admin Web Dashboard] --> [Notification Service] : "Send notifications"

[Transaction Service] --> UserDB : "Read/Write user data"
[Payment Service] --> PaymentDB : "Read/Write payment data"
[Merchant Service] --> UserDB : "Manage merchant data"
[Merchant Service] --> PaymentDB : "Process merchant payments"
[Transaction Service] --> TransactionDB : "Read/Write transaction data"

[Payment Service] --> [Payment Gateway] : "Process payment"
[Notification Service] --> [Push Notification Service] : "Send push notifications"
[Transaction Service] --> [Banking System] : "Bank Transfers"

@enduml
```
