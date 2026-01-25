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












