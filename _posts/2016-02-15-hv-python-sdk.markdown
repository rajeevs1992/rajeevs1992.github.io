---
layout: post
title:  "HealthVault Python SDK"
date:   2016-02-15 11:52:00 +0530
categories: python healthvault 
---

It has been some time (more than a year) I have written something. A lot has been happening in life, tech and non tech, but never really got in a mindset to write a post.

This is one of my first post since me joining Get Real Health, apart from the GSoC stuff. I can say for sure that my code has tremendously improved since I joined GRH, and I now know for sure what enterprise quality code really means, which I felt as a fancy term used by muggles during my college days.

Of the many new tools I came across while working at GRH, one that interested me greatly was the Microsoft HealthVault. HealthVault is a health data repository and API provided by Microsoft, and is almost the only complete health API available on the internet. The development is largely done via the .Net/C# SDK provided by Microsoft, which by itself is a piece of work. I was assigned major role in GRH's new product CHBase, which involved tasks that ask for in depth knowledge of the HealthVault architecture and APIs.

It was then I stumbled upon the python SDK for Healthvault, which was mentioned in the SDKs page of HealthVault. The code was hosted in [Google Code][pyhealthvault-google-code] and was in a very bad state, but worked in a very crude way. The development was stalled and the whole SDK was written into a single file. The HealthVault API is an XML API, and the python SDK did not use any XML libraries in the SDK, so you can guess the state of it. It was just a bunch of string substitutions to create a XML request and some dom manipulations to read the output.

The good thing was that it covered the tricky authorization part of the SDK. The HealthVault uses signed requests based on a key pair to authenticate the application against the API. The public key is uploaded to HealthVault as part of application configuration and the hash of top few nodes (header) of the xml request is encrypted using the private key and appended with the request. The API server decrypts the signature to get the hash, using the uploaded public key. Then calculates the hash of the header nodes and verifies the equality of the hashes. I was seeing this kind of genius for the first time in my life, and I am clearly impressed.

I decided to begin working on revamping the python SDK. I had worked on the HealthVault Java SDK, so I was pretty confident about the architecture to follow. The methods will all come under a single module, and the user will have to instantiate the method to execute it, pretty straightforward, but not as cute as C# SDK. Categorising methods and creating abstractions is one of the major tasks in my TODO list.

It was during this project that I began using some cool features and tools. The greatest one was adding my project into pip, I always thought adding project to pip would be a hell of a nightmare and would include extensive code reiview and standards check (ahem), now I know that any code can make into pip (my code is good :-/) and one must be careful in installing unknown packges from pip. I learnt how to make a release in Github, using tags. I was also able to make Sphinx finally work the way I wished it would. I was already using TDD in my GSoC, so that is not anything new, but my tests and code now seem so mature.

Links to the above mentioned stuff:

- [HealthVault Python SDK][pyhealthvault]
- [pip pyhealthvault][pyhealthvault-pip]

[pyhealthvault]: https://github.com/rajeevs1992/pyhealthvault
[pyhealthvault-pip]: https://pypi.python.org/pypi/pyhealthvault
[pyhealthvault-google-code]: https://code.google.com/p/pyhealthvault
