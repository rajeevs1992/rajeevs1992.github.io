---
layout: post
title:  "I ride an Uber"
date:   2016-03-13 16:16:00 +0530
categories: tech code blackberry
---

I own a BlackBerry. Its a great, nah, a good phone, and I have been using it for almost two years and I was sort of happy with it. The greatest problem for the BlackBerry 10 OS is the lack of apps, which the RIM does not care at all. You can install Android APKs on BB10, but not apps that use Google Play Services. So I am denied the luxury of booking my own cabs to get home from work. And that was a usually a strong point against me in my usual anti android arguments. That was when I discovered that Uber offered public API to book cabs, and a few SDKs for using it.

I decided to make my own Uber app. I first thought of making a native BB application, using C++ and Qt, but then decided against it, and decided to use my favourite stack, Django. I set up an environment and started my project. The first obstacle was that Uber requires you to verify your phone number to unlock your account, which can be done only using the app. I had to contact support, and they manually verified my number in a few hours.

I thought of using the Uber python SDK, but the sample code in the docs was so simple that I felt an SDK would be an overkill. I started of by designing a simple workflow for the app, and a list of features to be supported.

The workflow was decided to be as simple and basic as possible. Here is the summarized workflow for the app.

![Uber workflow](/img/uber/uber.png)

Another very important design concern was that the site must use as little data as possible, as I usually use only 2G data and I wanted the site work great for me. I avoided JQuery and any CSS themes. I was able to come up with a site that loads with just **one request for every page**. This design desicion proved to be heavily advantageous in terms of data as well as loading times.

After about a total of 20 hours, I was able to come up with a fully functional application for Uber. The last hurdle was that Uber requires the application endpoints to be either HTTPS or localhost. Luckily, heroku provides free HTTPS sites, so that too was solved.

Summarizing the features of my app:

- Uses very little data, ~2kb per page
- One request per page
- Save co ordinates for commonly used places and book cab without GPS
- Find the source from current location using GPS, or use saved locations
- Get a stack trace by mail on crash (no uber app has that feature :-P)

#A few screenshots

#Login screen
![Login](/img/uber/login.png)

#Check for rides
![Check for rides](/img/uber/book2.png)

#Select ride
![Select ride](/img/uber/select.png)

#Ride confirmation and status
![Ride confirmation and status](/img/uber/status.png)
