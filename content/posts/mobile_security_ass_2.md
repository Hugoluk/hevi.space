---
title: "Analysis of Dating Apps"
url: /posts/"
summary: Mobile Security Assignment 2
tags:
    - Mobile Security
    - Assignment 2
    - Frontpage
---
## Intro

As mobile dating apps become increasingly popular, the threat of leaking very personal data with these apps is getting more and more serious as it affects more people. Therefore a student colleague and I  picked the topic “Analysis of Dating Apps” for the second assignment for the practical part of the lecture "Mobile Security". These reports contain are our results of our research, where we analyzed 8 of the most popular ones for leaks and exploits. 

The reports of the apps are divided separately and linked.

Apps we consider to analyze:
1. [Tinder]({{< ref "/tinder/mobile_security_tinder.md" >}} "Tinder report")
2. [Plenty of Fish]({{< ref "/pof/mobile_security_pof.md" >}} "Plenty Of Fish report")
3. [OkCupid]({{< ref "/okcupid/mobile_security_okcupid.md" >}} "OkCupid report")
4. [Lovoo]({{< ref "/lovoo/mobile_security_lovoo.md" >}} "Lovoo report")
5. [Her]({{< ref "/her/mobile_security_her.md" >}} "Her report")
6. [Badoo]({{< ref "/badoo_and_bumble/mobile_security_badoo_bumble.md" >}} "Badoo report")
7. [Bumble]({{< ref "/badoo_and_bumble/mobile_security_badoo_bumble.md" >}} "Bumble report")
8. [Happn]({{< ref "/happn/mobile_security_happn.md" >}} "Happn report")

## Checklist

1. Inspecting the registration process
2. Inspecting the login process
3. Inspecting the liking process
4. Inspecting loading process of other users
5. Inspecting the data sent by clicking on a user
6. Inspecting public profile
7. Inspecting tracking requests
8. Intercepting requests to modify
9. Modifying requests and injecting data
10. Inspecting encrypted dat

## Testing setup

To research apps, we have set two testing setups apps that support x86 platform was tested in Android studio, virtual device manager. Some Bumble, Badoo and Her do not support x86 platforms so had to find an alternative. Performance of arm emulating in Android studio vritual device manager was too slow on our computers so we've resorted to using a real hardware. Urban had an old Huawei P9 lite which was not used anymore so we've installed apps there.

Huawei P9 Lite can't be easily rooted which caused some problems. Mostly with ADB permissions. It was not possible to download split apps from the phone. We had to resort to alternative online apk providers such as apk pure and apk mirror to get application apks to patch. 

Target app apks were patched using apk-mitm tool which automates the use of apktool and uber-APK signer. Traffic was intercepted either by MITM-proxy or with Burp Suite. Modifying requests and injecting data was done with Burp Suite.

## Tools

### Apktool

A tool decoding decompiling and rebuilding Android apps. It can decode resources to nearly original form and rebuild them after making some modifications. We have used apktool to change app certificate policies and disable certificate pinning to enable us to read encrypted HTTPS communication.

https://ibotpeaches.github.io/Apktool/

### Uber Apk Signer

Uber Apk Signer is a Android apk signer. Non-signed apks will not install Android. We have used it to sign out patched apk.

https://github.com/patrickfav/uber-apk-signer

### apk-mitm

Apk-mitm automates decompiling, patching, rebuilding, and signing of Android apks for HTTPS inspection. Apk-mitm automates the use of apktool, allowing user certificates, disabling certificate pinning, and uber-APK signer.

We have used it to streamline our process of preparing apps for examination.

https://github.com/shroudedcode/apk-mitm

### MITM proxy

MITM proxy is an interactive TLS-capable intercepting HTTP proxy for Windows, Linux, and Mac. We have decided to use it because it provides an effective method of intercepting communication without modifying the device.

https://mitmproxy.org/

### Burp suite
Burpsuite is a web application testing tool, which allows us to do a MITM and collect traffic. It also allows us to intercept requests and modify them. We can use the repeater function to modify and repeat any request to the API. The decoder function allows us to decode strings in e.g. base64 on the fly.

https://portswigger.net/burp

## App research

### Tinder
Tinder is the most popular or better most common dating app nowadays. It advertises with the simple method of swiping left or right on a users profile if they like them or dislike them. If both users like each other a so called match is made and they can start a conversation.
(Source: https://tinder.com/about-tinder)

Report is available at:
[Mobile Security: Tinder report]({{< ref "/tinder/mobile_security_tinder.md" >}} "Tinder report")

HackMD link available: https://hackmd.io/OTQmFT4DQt-WuDyfkQy43g

### Plenty of Fish
Plenty of Fish is a canadian dating app with the typical like/dislike charts, but also has a area, where user can watch a live stream of other users.
(Source: https://en.wikipedia.org/wiki/POF_(dating_website))

Report is available at:
[Mobile Security: Plenty of Fish report]({{< ref "/pof/mobile_security_pof.md" >}} "Plenty of Fish report")

HackMD link available: https://hackmd.io/cWuYII2pTOCso2cZF7-1yA

### OkCupid
OK Cupid is also a very popular dating app. It has the typical matches, where you can like or dislike suggested users. But also tabs where the app suggests you users with the most "match percentages", recommendations, users who like you and "Cupid's picks".

Report is available at:
[Mobile Security: OKCupid report]({{< ref "/okcupid/mobile_security_okcupid.md" >}} "OKCupid report")

HackMD link available: https://hackmd.io/OlAWl8-BS9y0Q9x5bR5J7g

### Lovoo
Lovoo is a popular dating app especially in Austria and Germany. It is geo location based and has the typical matching functions, people near you and a streaming function. 
(Source: https://about.lovoo.com/)

Report is available at:
[Mobile Security: Lovoo report]({{< ref "/lovoo/mobile_security_lovoo.md" >}} "Lovoo report")

HackMD link available: https://hackmd.io/JK7TNpr8QzSsZbRriLqVVA

### Her

Her, formerly Dattch, is a geosocial networking app geared towards lesbian, queer, bisexual, and straight women and non-binary people.  Cisgender men are not allowed to create profiles on the platform. (Source: https://en.wikipedia.org/wiki/Her_(dating_app))

Report is available at:
[Mobile Security: Her report]({{< ref "/her/mobile_security_her.md" >}} "Her report")

HackMD link available: https://hackmd.io/2EZaeTdRTsS6q4MYUPX3JA

### Badoo and Bumble

Badoo is a dating-focused social network founded in 2006. It operates in 190 countries and is available in 47 different languages, making it the world's most widely used dating network.
(Source: https://en.wikipedia.org/wiki/Badoo)

Bumble is an online dating application. Profiles of potential matches are displayed to users, who can "swipe left" to reject a candidate or "swipe right" to indicate interest. In heterosexual matches, only female users can make the first contact with matched male users, while in same-sex matches either person can send a message first.
(Source: https://en.wikipedia.org/wiki/Bumble)

Since they share the same back-end-structure, we only made one report for these two apps.

Report is available at:
[Mobile Security: Badoo and Bumble report]({{< ref "/badoo_and_bumble/mobile_security_badoo_bumble.md" >}} "Badoo and Bumble report")

HackMD link available: https://hackmd.io/vzX2WogASCKK4urcQOyNMQ

### Happn
Happn is a Paris-based dating app and has been around since 2014. Happn helps you connect with people you have crossed paths with in real life.
(Source : https://www.eu-startups.com/2022/02/10-european-startups-helping-you-find-love/)

Report is available at:
[Mobile Security: Happn report]({{< ref "/happn/mobile_security_happn.md" >}} "Happn report")

HackMD link available: https://hackmd.io/1T8lIeyGRhqV2RR4RX5L3g?both


## Conclusion

Comparing it to the linked survey a few years ago, we found out that for most apps we tested, there is still a lot of data leaked. We discovered that one point in the survey got better at this point in time. On every app we tested we looked for the Facebook (or Instagram) id. Some used the Facebook login or used a tag if the user has Instagram. But no personal connection to that (except the user linked it themself) was found.

Besides that we found that a few app still leak a lot of personal data and exact locations to other users. One good example is Lovoo. We found a tool written by a user a long time ago, which allows us to track people with requests to the API. This would still function today because the data we get today still fits for this tool.
But one positive example is Tinder. It really got better over time (in comparison to the state of the app in the survey) and nowadays leaks not that much data of other users. It still reveals the distance of a user, but not much in detail to use it for malicious purposes. A little example would be the leak of the picture uploaded in open networks. The app nowadays encrypts in and sends it securely over the network.

On Her and OKCupid we also found a lot of data leaked which isn't even visible and useful for the end user. On OKCupid it's also possible to skip the whole phone number verification, which could lead to automatization and spam accounts.
Bumble and Badoo proved to be the most diligent in protecting user data. Other than signs of commercial tracking we were not able to find anything of significance.

In conclusion, it can be said that a lot of apps are still leaking data and therefore state of dating apps didn't get much better. Some apps (the most popular ones) improved, but stalking could be still an issue nowadays. The end users should be aware of this when using such apps. And should consider which they use and if they should use such apps in the first place.