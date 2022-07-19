---
title: "Second"
layout: "baseof"
url: /posts/"
summary: second
---
# Mobile Security Assignment 2

Urban Suhadolnik 12127980
Daniel Hevesy-Szettyan 11807776

As mobile dating apps become increasingly popular, the threat of leaking very personal data with these apps is getting more and more serious as it affects more people. Therefore we picked the topic “Analysis of Dating Apps”, where we research previous leaks of dating apps and analyze 8 of them. 

Apps we consider to analyze:
1. Tinder
2. Plenty Of Fish
3. OkCupid
4. Lovoo
5. Her
6. Happn
7. Badoo
8. Bumble

## Checklist

1. Description
2. Inspecting the registration process
3. Inspect communication (MITM-Proxy, burp suite)
4. Inspect liking (process)
5. Are they staticly linking photos or other personal data (can we get more data about a specific user?) E.g. https://img.lovoo.com/users/pictures/62767fb02a175046ef7c7350/image.jpg where 6266cd58b5e1341bb476f697 is the ID of the user (my ID in this case)
6. Decompile and reverse app code
7. Inspect(debug) while the app is running (and what things are loaded in memory)

Advanced:
6. Reverse and document API



## Testing set up

To research apps we have set two testing seatups apps that support x86 platform were tested in Android studio vritual device manager. Some Bumble, Badoo and Her do not support x86 platform so had to find an alternative. Performance of arm emulating in Android studio vritual device manager was too slow on our computers so we've resorted to using a real hardware. Urban had an old Huawei P9 lite which was not used anymore so we've installed apps there.

Huawei P9 Lite can't be easily rooted which coused some problems. Mostly with adb permissions. It was not possible to download split apks from the phone. We had to resort to alternative online apk prvider such as apk pure and apk mirror to get application apks to patch.


## Tools

### adb

### apk-mitm

https://github.com/shroudedcode/apk-mitm

### MITM proxy


### Burp suite
Burpsuite is a web application testing tool, which allows us to do a MITM and collect traffic. It also allows us to intercept requests and modify them. We can use the repeater function to modify and repeat any request to the API. The decoder function allows us to decode strings in e.g. base64 on the fly.



# App research

### Tinder
Tinder is the most popular or better most common dating app nowadays. It advertises with the simple method of swiping left or right on a users profile if they like them or dislike them. If both users like each other a so called match is made and they can start a conversation.
(Source: https://tinder.com/about-tinder)

Report is available at:
https://hackmd.io/OTQmFT4DQt-WuDyfkQy43g

### Planty of fish
Plenty of Fish is a canadian dating app with the typical like/dislike charts, but also has a area, where user can watch a live stream of other users.
(Source: https://en.wikipedia.org/wiki/POF_(dating_website))

Report is available at:
https://hackmd.io/cWuYII2pTOCso2cZF7-1yA

### OkCupid
OK Cupid is also a very popular dating app. It has the typical matches, where you can like or dislike suggested users. But also tabs where the app suggests you users with the most "match percentages", recommendations, users who like you and "Cupid's picks".

Report is available at:
https://hackmd.io/OlAWl8-BS9y0Q9x5bR5J7g

### Lovoo
Lovoo is a popular dating app especially in Austria and Germany. It is geo location based and has the typical matching functions, people near you and a streaming function. 
(Source: https://about.lovoo.com/)

Report is available at:
https://hackmd.io/JK7TNpr8QzSsZbRriLqVVA

### Her

Her, formerly Dattch, is a geosocial networking app geared towards lesbian, queer, bisexual, and straight women and non-binary people.  Cisgender men are not allowed to create profiles on the platform. (Source: https://en.wikipedia.org/wiki/Her_(dating_app))

Report is available at:
https://hackmd.io/2EZaeTdRTsS6q4MYUPX3JA

### Bumble

Bumble is an online dating application. Profiles of potential matches are displayed to users, who can "swipe left" to reject a candidate or "swipe right" to indicate interest. In heterosexual matches, only female users can make the first contact with matched male users, while in same-sex matches either person can send a message first.
(Source: https://en.wikipedia.org/wiki/Bumble)

Report for Bumble and Badoo is available at:
https://hackmd.io/vzX2WogASCKK4urcQOyNMQ

### Badoo

Badoo is a dating-focused social network founded in 2006. It operates in 190 countries and is available in 47 different languages, making it the world's most widely used dating network.
(Source: https://en.wikipedia.org/wiki/Badoo)

Report for Bumble and Badoo is available at:
https://hackmd.io/vzX2WogASCKK4urcQOyNMQ

### Happn
Happn is a Paris-based dating app and has been around since 2014. Happn helps you connect with people you have crossed paths with in real life.
(Source : https://www.eu-startups.com/2022/02/10-european-startups-helping-you-find-love/)

Report is available at:
https://hackmd.io/1T8lIeyGRhqV2RR4RX5L3g?both


