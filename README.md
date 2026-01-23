# **Change Scenario: Add Mobile Money Payments in Uganda**
## 1. Which parts of the app would need changes?
Adding mobile money is not just adding a new button. It affects multiple layers of the system.
### a) User Interface (UI)
Changes needed:  
- New payment option screens: MTN MoMo, Airtel Money, etc.  
- Phone number input instead of card details.  
- Status screens for:
  - Waiting for approval on your phone  
  - Payment pending  
  - Payment failed / reversed
- Error messaging tailored to Mobile Money (timeouts, insufficient balance, user cancelled).

Why:  
Mobile Money flows are interactive and asynchronous, unlike instant card payments.  

### b) Business Logic
Major changes here include:  
- Payment state management (pending → successful → failed).
- Subscription activation logic must wait for confirmation from telecoms.
- Retry & timeout handling (users may approve late or not at all).
- Currency handling (UGX instead of USD/EUR).
- Partial payments & reversals logic (common in MoMo systems).

Why:  
Unlike cards, mobile money does not confirm instantly.  

### c) Backend / APIs
Changes include:  
- Integration with:
  - MTN MoMo API
  - Airtel Money API
  - Possibly a payment aggregator (Flutterwave, Paystack, etc.)
- Webhook listeners to receive payment confirmation asynchronously.
- Fraud and duplicate transaction protection.

Why:  
Mobile Money payments don’t complete in a single request–response cycle.  

### d) Data Storage
New data must be stored:  
- Mobile money transaction IDs
- Payment status (pending, successful, failed)
- Provider-specific references
- Audit logs for disputes and refunds  

This data must be consistent and reliable, especially for financial records.  

## 2. What existing features could break?
### a) Instant Premium Access
Problem:  
- Spotify grants Premium immediately after payment success.
- Mobile Money payments can take minutes (or fail after initiation).

Risk:
- Users get Premium without paying.
- Or users pay but don’t get Premium.

### b) Subscription Renewal Logic  
Mobile money recurring payments are unreliable:  
-	Users change SIM cards
-	Wallets run out of balance (Statistically, mobile money balances hit zero far more often than card-linked accounts.)
-	Telecoms may require user approval every month.
- Providers fail silently (The user must actively approve each payment. If the wallet has no balance, nothing happens. For cards, the system pulls money from the bank. Retries can happen automatically. Users can go negative or have grace periods. So, with mobile money, payment fails silently unless the user intervenes.)

Auto-renewals may:
-	Fail without clear feedback
-	Incorrectly downgrade users  
### c) Offline Downloads
Problem:
-	Offline access depends on an active subscription flag.
-	Payment delays may incorrectly deactivate Premium.

Risk:
-	Users lose offline music while they actually paid.

## 3. Why would this change be difficult to implement?
This change is difficult because it involves technical, business, and regional challenges at the same time.
### a) Asynchronous & Unreliable Payment Flow
Card payment:
>Pay → Success → Done

Mobile Money payment:
>Initiate → Wait → User approves → Telecom confirms → Webhook → Verify → Activate

So:
-	Confirmation may take seconds or minutes
-	Sometimes confirmation never arrives

The system must:
-	Handle timeouts
-	Retry safely
-	Avoid double charging

This increases complexity dramatically.  

This breaks:
-	Simple payment assumptions
-	Existing subscription workflows
### b) Fragmented Payment Ecosystem
Uganda has:
-	Multiple providers (MTN, Airtel, others)
-	Different APIs, error codes, and behaviours

Supporting all of them means:
-	More integrations
-	More testing
-	More edge cases

You’re not adding one payment method — you’re adding multiple mini-systems.
### c) Reliability & Network Issues
Common in Mobile Money:
-	Delayed callbacks
-	Duplicate confirmations
-	Partial failures
-	Timeouts

Spotify-scale systems are built for high reliability, and Mobile Money introduces instability.

