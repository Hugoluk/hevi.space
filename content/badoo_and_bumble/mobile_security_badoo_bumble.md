---
title: "Mobile Security: Badoo and Bumble report"
url: /badoo_and_bumble/"
summary: Analysis of Badoo and Bumble
tags:
    - Mobile Security
    - Assignment 2
    - Badoo
    - Bumble
---

## Bumble
Bumble is an online dating application. Profiles of potential matches are displayed to users, who can "swipe left" to reject a candidate or "swipe right" to indicate interest. In heterosexual matches, only female users can make the first contact with matched male users, while in same-sex matches either person can send a message first.

Source: https://en.wikipedia.org/wiki/Bumble

**Device used:** Huawei P9 lite, Android 7.0 API Level 24, arm64_v8a

## Badoo
Badoo is a dating-focused social network founded in 2006. It operates in 190 countries and is available in 47 different languages, making it the world's most widely used dating network.

Source: https://en.wikipedia.org/wiki/Badoo

**Device used:** Huawei P9 lite, Android 7.0 API Level 24, arm64_v8a


## Structure of the report

1. Description
2. Introduction
3. Registration process
4. Login process
5. Observed communication
9. Tracking
10. Conclusion
11. Future work

## Introduction

During examination od Bumble and Badoo we've noticed that a big part of the backend is essentially the same. After some additional research we've learned that although Bumble and Bado were founded by different people from different countries, USA and Russia, they are now both owned by Bumble inc.
Furthermore, both apps are very well written. By inspecting communication we were literally able to find nothing. Not even where  new profiles are acquired. Only downloads of photos being viewed are detectable. Other information must be sent by encrypting in metadata.
For sake of completeness we will try to document what we found or didn't found according to the established structure of the report where possible.

## Observed communication
From logging in to swiping, the only communication that could be seen were picture downloads. We have no real explanation why it is like this and from where do Bubmle and Badoo acquire lists of profiles or a least next use profile to be shown.

![](https://i.imgur.com/TK2kLiF.png)

One peculiarity were these pixelated photos. They were never shown in the app but were downloaded regularly. There is some information in the comment of jpeg metadata. Maybe some information is stored in these photos. But we don't really have an explanation for this.

![](https://i.imgur.com/0SjmQPH.png)


## Tracking

### App usage tracking
Badoo and Buble do employ some app usage tracking. Every time we opened a new app view there was an API call to `/hotpanel`. Information reported was more extensive than in case of other apps and included app version, device type, device id, user id and time spent on a particular app view.


`POST https://eu1.bumble.com/hotpanel/hotpanel.phtml?version=2.0 HTTP/1.1`

```json=
{
    "application":{
        "brand":4,
        "layout":1,
        "platform":3,
        "app_version":"5.271.1",
        "is_premium":false
    },
    "device":{
        "manufacturer":"HUAWEI",
        "model":"HUAWEI VNS-L21",
        "os_version":"7.0",
        "locale":"en_GB",
        "device_id":"3c24a4ec-e6dd-4b30-a0c7-a810d4e3934a"
    },
    "user":{
        "user_id":0,
        "gender":0,
        "country_id":2,
        "age":0,
        "encrypted_user_id":"zAhMACjE3NzAxNDA2NjUAIF0TmW8gJ-3vlP5oAcinpbKG-Ev9saN2uXBvIGTZw68k"
    },
    "session_id":"d1f8136d-aa53-0e31-3fba-556ad93079ee",
    "events":[
        {
            "name":49,
            "body":{
                "view_screen":{
                }
            },
            "ts":1654512495093,
            "tracking":{
                "screen_id":"15",
                "screen_name":399
            }
        }
    ],
    "ts_sent":1654512495223
```

### Commercial tracking

Bumble and Badoo are using appsflyer for outsourced marketing tracking. We were not able to figure what kind of information is being transmitted because the communication we've intercepted is in binary (and encrypted?) format.

`POST https://launches.appsflyer.com/api/v6.5/androidevent?app_id=com.bumble.app&buildnumber=6.5.1 HTTP/1.1`

```=
0000000000 b8 11 fb 31 51 59 f3 4d 31 2f 2c cf ee 9e 39 96   ...1QY.M1/,...9.
0000000010 e1 2b 6b da f8 c1 a9 b2 61 fb b4 b1 92 c4 e9 ff   .+k.....a.......
0000000020 a5 e0 10 55 22 86 9f 9c 7e 68 24 b3 5d 5d 10 ad   ...U"...~h$.]]..
0000000030 b5 64 74 46 7e b1 7f 3b b3 d6 9f 8b a0 34 2e d5   .dtF~..;.....4..
0000000040 0a 6d 8d 5c 3e e2 f0 f7 95 34 f5 1f 5e 72 0a 1f   .m.\>....4..^r..
0000000050 2e 20 58 0f da 8c 60 44 1b 1d 4b be 77 fd 66 2b   . X...`D..K.w.f+
0000000060 cf 2d c6 0a a0 17 76 35 d8 f2 00 e5 f0 df ca f5   .-....v5........
0000000070 4a 6c 82 d9 57 5f 9b 80 f2 05 97 2b 85 9f 05 f9   Jl..W_.....+....
0000000080 5f 9b d8 51 50 d5 9f b1 d6 f4 d8 7e db 1b 43 22   _..QP......~..C"
0000000090 95 10 47 86 71 8d 99 f8 15 9c 63 f6 3c 53 f6 42   ..G.q.....c.<S.B
```

## Conclusion

Bumble and Badoo are very well written dating apps. We think that users of this two apps can be reassured that their private information is safe.

## Future work
There is not much that could be done by examining communication. Any further research should be focused on static and dynamic analysis of the application.



