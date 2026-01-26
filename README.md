# software-construction
Spotify: Behind the App
Course: Software Construction
Assignment: Behind the App – Thinking Like Software Engineers

Group members
Kisuze GAreth Neville (S23B23/029)
Nziriga Isaac Nickson (S23B23/046)
Andrew Ogwang (S23B23/050)
Katende Derrick (S23B23/024)
Mutumba Benjamin Mubeezi (S23B23/010)


PART A: UNDERSTANDING THE APP
1. APP OVERVIEW
What problem does spotify solve?
  Solves the problem of accessing and discovering music easily. allows users stream millions of songs, podcasts and audio content without needing to store music files on their devices.

Primary Users;
 -music listeners
 -podcast listeners
 -free users(ad-supported)
 -premium subscribers

2.Core features
 1.User Authentication(sign up/login)
 2.Music Search and discovery
 3.Notifications(new releases,recommendations)
 4.Offline downloads (premium feature)
 5.Payments(to access premium services)
 6.music streaming(play,skip,pause)

Part B Thinking behind the scenes

Based on the app we picked (Spotify) which is mainly a music streaming application, the features talked about earlier like logging in, song selection, payments, notifications and song search.

The features above were implemented using various software components, having done abit of research these are my findings on what features used what software components:

1.For logging in for example, APIs are used and this software component just means that when someone is filling in login information the api helps with comparison basically to make sure that the information provided is accurate so as to allow the user access their account profile.

2.Song selection, this being a music streaming application, when picking a song the most useful way of conveying the information would be by using a visual method and an interactive method and for this a unique User Interface was used. The UI uses rows and tiles that show the albums and songs that are in the app, for a user to select a song they want the hover over the tile and click the song that the want to listen to.

3. Payments, for this business logic is implemented, where by the app has different features depending on the payment plan that the user has. For example, a free user gets a finite amount of skips on a song while a premium user doesn't, so the payment system is what controls this. when someone pays for the premium the are opened up to more features on the application, this makes people pay money for more services which helps the business.

4.Notifications, for notifications to be pushed tokens are used, token are basically strings of information that hold the message that will be sent as the notification, when one allows notifications on the app, when an event is triggered, the notification will be pushed in form of the token to the backend which will then be passed on until it pops up on ones phone.

5.Song search, this a feature where one searches the database using keywords like genre or even song title, all the tracks are stored using lets say a database. When a person inputs certain keywords that are mapped to the songs in the database they are retrieved and shown to the user to see if that is what they had searched for.


This being a streaming application it means that it heavily relies on the availability of internet connectivity but thanks to the payment feature a person who pays for the premium option has abit more freedom than the free version. 
For example for the premium version due to a download feature, one can search for a song as long as they downloaded the songs prior, so for that specific feature of searching for a song it works offline for premium users but doesn't for free users.
Basically all of the Spotify features work offline unless one has paid for the premium version 

**PART C**
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

Part D: Software Construction Challenges

Maintaining a global platform like Spotify involves juggling millions of concurrent users, massive data pipelines, and a highly complex microservices architecture. Here are five significant engineering challenges involved in maintaining and improving the app:

1. Scalability and Low-Latency Streaming
With over 600 million users, Spotify must ensure that when a user hits "play," the music starts almost instantly, regardless of where they are in the world. This requires a massive, distributed Content Delivery Network (CDN) and sophisticated backend load balancing.

The Challenge: Engineering teams must prevent "cascading failures" where one overloaded server causes a chain reaction that brings down the entire streaming service during high-traffic events, such as a major album release.

2. Cross-Platform Consistency and Fragmentation
Spotify exists on an enormous range of hardware: iPhones, Android devices, Windows/Mac desktops, smart TVs, gaming consoles, and even car dashboards.

The Challenge: Each platform has different hardware capabilities, screen ratios, and OS constraints. Maintaining feature parity (ensuring a new feature like "Jam" works identically across all these devices) requires rigorous cross-platform testing and often necessitates building shared C++ libraries to reuse core logic across different operating systems.

3. Personalization at Scale (Big Data)
Spotify’s "Discover Weekly" and "Wrapped" features are powered by complex machine learning models that analyze billions of user interactions (likes, skips, shares).

The Challenge: Processing petabytes of data to provide real-time recommendations without compromising app performance is difficult. Engineers must build robust data pipelines that can ingest user behavior data, process it through AI models, and push updates back to the user's interface without lag.

4. Microservices and Decoupling
Spotify famously uses a "Squads" and "Tribes" engineering model, where hundreds of small teams own specific features (e.g., the Search bar, the Payment gateway, or the Playlist UI).

The Challenge: These features are often built as independent microservices. If these services are too "tightly coupled," a bug in the Search service might accidentally break the Home screen. Engineers must maintain strict "API contracts" to ensure that teams can update their specific features without crashing the rest of the application.

5. Reliability Under Poor Network Conditions
A significant portion of Spotify's user base listens while commuting, underground, or in areas with unstable 3G/4G connections.

The Challenge: The app must be engineered for graceful degradation. This involves intelligent caching (pre-downloading the next song in the background) and adaptive bitrate streaming, which automatically lowers the audio quality to prevent buffering when the signal strength drops.

Part E: Group Reflection 

1) What surprised our group most about the complexity behind this app?
We were surprised that Spotify isn’t “just playing music.” Behind one tap, it has to identify the user, check their subscription status, match the right audio file version, manage copyrights/region rules, pick a streaming quality based on network speed, and still keep the app smooth. Even features that look simple—like search, playlists, or “Liked Songs”—involve huge data handling, real-time syncing across devices, and recommendation systems that constantly learn from user behavior.

2) Why is writing “working code” not enough for software systems at this scale?
Because at Spotify’s scale, code must be maintainable, reliable, secure, and scalable over time. “Working code” might function today, but it can fail under heavy traffic, break on certain phones, drain battery, or become impossible to update safely. Spotify also needs strong testing, monitoring, and deployment practices so changes don’t crash millions of users at once. Plus, the system must handle messy real-world problems—slow internet, offline mode, different devices, payment issues, and continuous feature updates—without becoming unstable.

3) What did we learn about teamwork from this exercise?
We learned that teamwork is not optional in large software—it’s the only way it works. Different people naturally notice different things: one focuses on user experience, another on backend systems, another on risks and failures. To get a solid answer, we had to divide tasks, agree on assumptions, keep our explanations consistent, and combine everyone’s ideas into one clear document. We also realized that good collaboration means communicating early, keeping work organized in GitHub, and making sure everyone contributes meaningfully—not just one person doing everything.

Contributions
Part A-Kisuze
Part B-Mutumba
Part C-Ogwang
Part D-Nziriga
Part E-Katende
