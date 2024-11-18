# Feature: User Registration

## Scenario: User Registers Successfully

### Given:
- The user has opened the app for the first time.
- The user provides a valid mobile number.

### When:
- The user enters the mobile number and submits it, then the app sends an OTP to the provided number.
- The user enters the correct OTP within the time limit.
- The user completes the registration form with all required details (e.g., name, email).

### Then:
- The user's account is created successfully.
- The user is redirected to the app's dashboard.

---

## Registration.js Code

```javascript
const validator = require('assert');
const registrationPage = require('../pages/registrationPage');

describe('User Registration', function() {
  it('should register user successfully', function() {
    registrationPage.open();
    registrationPage.fillRegistrationForm({
      name: 'John Doe',
      email: 'john@example.com',
      password: 'password123',
      mobileNumber: '9876543210'
    });

    registrationPage.submitForm();

    const successMessage = registrationPage.getSuccessMessage();
    validator.strictEqual(successMessage, 'Registration successful', 'Success message mismatch');

    const currentUrl = browser.getUrl();
    validator.ok(currentUrl.includes('/dashboard'), 'URL does not redirect to dashboard');
  });
});
```
---

# Feature: Account and Identity Verification

## Scenario: User Completes KYC (Know Your Customer) Verification

### Given:
- The user has registered on the app and logged in successfully.
- The user is prompted to complete the KYC process as required by the app.

### When:
- The user navigates to the KYC section.
- The user provides valid government-issued ID (e.g., Aadhaar, Passport, or PAN card).
- The user submits the KYC details and other details for verification.

### Then:
- The app validates the submitted documents and information.
- The account is verified, and the user gains access to full features (e.g., higher transaction limits, withdrawal options).

---

## AccountVerfication.js Code

```javascript
const validator = require('assert');
const kycPage = require('../pages/kycPage');

describe('Account and Identity Verification (KYC)', function() {
  it('should successfully complete KYC verification', function() {
    kycPage.open();

    // Provide user details for verification
    kycPage.uploadDocument('aadhaarCard', '/path/to/aadhaar_card.jpg');
    kycPage.uploadSelfie('/path/to/selfie.jpg');

    // Enter additional information (if required)
    kycPage.enterAddress({
      addressLine1: '123 Main Street',
      city: 'Mumbai',
      postalCode: '400001'
    });

    kycPage.submitKYC();

    const successMessage = kycPage.getSuccessMessage();
    validator.strictEqual(successMessage, 'KYC verification in progress', 'Success message mismatch');
    
    const verificationStatus = kycPage.getVerificationStatus();
    validator.strictEqual(verificationStatus, 'Verified', 'Account verification status mismatch');
  });

  it('should display an error message if KYC documents are invalid', function() {
    // Simulate invalid document upload
    kycPage.uploadDocument('aadhaarCard', '/path/to/invalid_document.jpg');

    // Open the KYC page
    kycPage.open();

    // Validate error message for invalid document
    const errorMessage = kycPage.getErrorMessage();
    validator.strictEqual(errorMessage, 'Invalid document, please upload a valid ID', 'Error message mismatch');
  });
});
```
---


# Feature: Linking Bank Account or Card

## Scenario: User Links Bank Account Successfully

### Given:
- The user has logged into their account and completed KYC Verification
- The user has a valid mobile number registered with their bank.

### When:
- The user selects their bank from the available list, and the app verifies the user's bank account using the registered mobile number.
- The user enters their debit card details (if required) to authenticate the bank account.
- The user sets up or links an existing UPI ID and creates a UPI PIN for secure transactions.

### Then:
- The user's bank account is linked successfully.
- The user can now make transactions using their linked bank account.

---

## BankAuth.js Code

```javascript
const validator = require('assert');
const bankLinkingPage = require('../pages/bankLinkingPage');

describe('Linking Bank Account', function() {
  it('should link the user’s bank account successfully', function() {
    // Open the bank linking page
    bankLinkingPage.open();

    // Select a bank from the list
    bankLinkingPage.selectBank('State Bank of India');

    // Verify bank account via mobile number
    bankLinkingPage.verifyBankAccount('9876543210');

    // Authenticate using debit card details
    bankLinkingPage.enterDebitCardDetails({
      cardNumber: '1234-5678-9876-5432',
      expiryDate: '12/26',
      cvv: '123'
    });

    // Set up UPI ID and PIN
    bankLinkingPage.setupUPI({
      upiID: 'john.sbi@upi',
      pin: '123456'
    });

    // Validate success message
    const successMessage = bankLinkingPage.getSuccessMessage();
    validator.strictEqual(successMessage, 'Bank account linked successfully', 'Success message mismatch');

    // Validate the account appears in linked accounts
    const linkedAccounts = bankLinkingPage.getLinkedAccounts();
    validator.ok(linkedAccounts.includes('State Bank of India'), 'Bank account not listed in linked accounts');
  });
});
```
---


# Feature: Money Transfer

## Scenario: User Transfers Money Successfully

### Given:
- The user has a linked bank account or card in the app and logged into their account
- The user has sufficient balance in their linked bank account or card.

### When:
- The user navigates to the "Money Transfer" section.
- The user enters the recipient's details (e.g., bank account/UPI ID), specifies the transfer amount, and confirms the transaction.
- The user enters the required authentication (e.g., UPI PIN or OTP).

### Then:
- The transaction is processed successfully and a confirmation message is displayed to the user.
- The recipient receives the transferred amount.
- The transaction appears in the user’s transaction history.

---

## 

```javascript
const validator = require('assert');
const moneyTransferPage = require('../pages/moneyTransferPage');

describe('Money Transfer', function() {
  it('should transfer money successfully', function() {
    moneyTransferPage.open();
    moneyTransferPage.enterRecipientDetails({
      upiID: 'recipient@bank',
      accountNumber: '1234567890',
      ifscCode: 'BANK0001234'
    });

    moneyTransferPage.enterTransferAmount(500);

    moneyTransferPage.confirmTransaction();

    moneyTransferPage.authenticateTransaction('123456'); // Example PIN

    const successMessage = moneyTransferPage.getSuccessMessage();
    validator.strictEqual(successMessage, 'Transaction successful', 'Success message mismatch');

    //Validate transaction history
    const transactionHistory = moneyTransferPage.getTransactionHistory();
    const recentTransaction = transactionHistory[0];
    validator.strictEqual(recentTransaction.amount, 500, 'Transaction amount mismatch');
    validator.strictEqual(recentTransaction.status, 'Completed', 'Transaction status mismatch');
  });
});
```
---

# Feature: QR Code Payments

## Scenario: User Makes Payment Using QR Code

### Given:
- The user is logged into their account.
- The user has a linked bank account or payment method.
- The merchant or recipient has generated a valid QR code for payment.

### When:
- The user navigates to the "QR Code Payments" section in the app, and scans the QR code provided by the merchant or recipient.
- The app retrieves the payment details (amount, recipient information) from the QR code.
- The user confirms the payment details, and enters any required authentication (e.g., UPI PIN, OTP).

### Then:
- The payment is processed successfully.
- The transaction is reflected in the user’s transaction history.
- The recipient receives the payment.

---

## QRCodePayment.js Code

```javascript
const validator = require('assert');
const qrPaymentPage = require('../pages/qrPaymentPage');

describe('QR Code Payments', function() {
  it('should make payment successfully using a QR code', function() {
    qrPaymentPage.open();
    qrPaymentPage.scanQRCode('/path/to/qr_code_image.png');

    qrPaymentPage.confirmPayment({
      amount: 500,
      recipient: 'merchant@upi'
    });

    qrPaymentPage.authenticatePayment('123456');

    const successMessage = qrPaymentPage.getSuccessMessage();
    validator.strictEqual(successMessage, 'Payment successful', 'Success message mismatch');

    const transactionHistory = qrPaymentPage.getTransactionHistory();
    const recentTransaction = transactionHistory[0];
    validator.strictEqual(recentTransaction.amount, 500, 'Transaction amount mismatch');
    validator.strictEqual(recentTransaction.status, 'Completed', 'Transaction status mismatch');
  });

  it('should display an error message if QR code is invalid or scan fails', function() {
    qrPaymentPage.scanQRCode('/path/to/invalid_qr_code.png');

    const errorMessage = qrPaymentPage.getErrorMessage();
    validator.strictEqual(errorMessage, 'Invalid QR code, please try again', 'Error message mismatch');
  });
});

```
---


# Feature: Bank Account Balance

## Scenario: User Checks Bank Account Balance

### Given:
- The user has a linked bank account and is logged into their account.
 
### When:
- The user navigates to the "Bank Account Balance" section.
- The app fetches the current balance from the linked bank account.

### Then:
- The user sees the current balance of their linked bank account.
- A confirmation message or error message is displayed if the balance fetch fails.

---

## BankAccountBalance.js

```javascript
const validator = require('assert');
const bankAccountPage = require('../pages/bankAccountPage');

describe('Bank Account Balance', function() {
  it('should display the correct bank account balance', function() {
    bankAccountPage.open();

    const balance = bankAccountPage.getBankAccountBalance();

    validator.ok(balance >= 0, 'Balance should be a non-negative number');
    console.log(`Current balance: ₹${balance}`);

    const currentBalance = bankAccountPage.getBankAccountBalance();
    validator.strictEqual(balance, currentBalance, 'Bank balance was not updated correctly');
  });

  it('should display an error message if unable to fetch balance', function() {
    bankAccountPage.simulateNetworkIssue();

    bankAccountPage.open();

    const errorMessage = bankAccountPage.getErrorMessage();
    validator.strictEqual(errorMessage, 'Unable to fetch balance, please try again later', 'Error message mismatch');
  });
});


```
---

# Feature: Transaction History

## Scenario: User Views Transaction History

### Given:
- The user has performed at least one transaction (either send or receive money).
- The user is logged into their account and navigates to the "Transaction History" section in the app.

### When:
- The user selects the "Transaction History" option in the app.
- The app fetches and displays the user's past transactions.
- The user is able to filter transactions by date, amount, or type (debit/credit).

### Then:
- The transaction history is displayed with details such as date, transaction type, amount, and status (successful, pending, failed).
- The user can scroll through previous transactions or search specific ones.
- The user can view detailed information about each transaction, including transaction ID and recipient.

---

## TransactionHistory.js

```javascript
const validator = require('assert');
const transactionHistoryPage = require('../pages/transactionHistoryPage');

describe('Transaction History', function() {
  it('should display correct transaction history details', function() {
    transactionHistoryPage.open();

    const transactions = transactionHistoryPage.getTransactionHistory();

    validator.ok(transactions.length > 0, 'Transaction history is empty');
    
    const recentTransaction = transactions[0]; 
    validator.ok(recentTransaction.date, 'Date is missing in transaction');
    validator.ok(recentTransaction.amount, 'Amount is missing in transaction');
    validator.ok(recentTransaction.status, 'Status is missing in transaction');

    const filteredTransactions = transactionHistoryPage.filterTransactionsByDate('2024-11-01');
    validator.ok(filteredTransactions.length > 0, 'No transactions found for the selected date');

    const debitTransactions = transactionHistoryPage.filterTransactionsByType('Debit');
    validator.ok(debitTransactions.length > 0, 'No debit transactions found');
  });

  it('should display an error message if unable to fetch transaction history', function() {
    transactionHistoryPage.simulateNetworkIssue();

    transactionHistoryPage.open();

    const errorMessage = transactionHistoryPage.getErrorMessage();
    validator.strictEqual(errorMessage, 'Unable to fetch transaction history, please try again later', 'Error message mismatch');
  });
});
