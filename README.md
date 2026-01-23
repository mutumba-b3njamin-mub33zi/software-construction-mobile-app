# software-construction
Spotify: Behind the App
Course: Software Construction
Assignment: Behind the App – Thinking Like Software Engineers

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
