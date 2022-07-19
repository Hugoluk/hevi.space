---
title: "Mobile Security: Lovoo report"
url: /lovoo/"
summary: Analysis of Lovoo
tags:
    - Mobile Security
    - Assignment 2
    - Lovoo
---

## Description
Lovoo is a popular dating app especially in Austria and Germany. It is geo location based and has the typical matching functions, people near you and a streaming function. 

Source: https://about.lovoo.com/

**Device used:** Android emulator Pixel 4 Android 9 API level 28, x86

## Structure of report
1. Description
2. Registration process
3. Login process
6. Obtaining other users data
7. Direct profile access
8. Investigating premium functions
9. Liking Process
10. Tracking
11. Conclusion

## Registration process
In the registration process of this app there wasn't anything interesting be found.

## Login process
The first thing the app does after starting up is to load the users data with a initial get request
```
GET /init HTTP/2
Host: api.lovoo.com
Cache-Control: no-cache
Accept: application/json
Kissapi-App-Version: 12300
Kissapi-Version: 1.36.0
Kissapi-Device-Os: 28
Kissapi-Device-Model: AOSP on IA Emulator
Tz: Europe/Vienna
Kissapi-Device: android
Kissapi-App-Package-Id: net.lovoo.android
Kissapi-Android-Fingerprint: google/sdk_gphone_x86_arm/generic_x86_arm:9/PSR1.180720.117/5875966:user/release-keys
Kissapi-App: lovoo
Kissapi-Apptype: google
User-Agent: LOVOO/12300 Dalvik/2.1.0 (Linux; U; Android 9; AOSP on IA Emulator Build/PSR1.180720.117) 4.9.1
Kissapi-Android-Id: 7eaa55c7260aeb8f
Kissapi-App-Id: 682f302f-e535-4ca9-889c-d462ffe2b58b?identifier=lovoo.prod.firebase
Kissapi-Gpsa-Id: 682f302f-e535-4ca9-889c-d462ffe2b58b?identifier=lovoo.prod.firebase
Kissapi-Gpsa-On: true
Accept-Language: en-US
Wifi: 1
Kissapi-Mac: e3f5536a141811db40efd6400f1d0a4e
Kissapi-Ad-Id: f8738acc8d7372f0dd5af125bfae4c9e
Kissapi-Ad-Name: Organic
Authorization: Bearer {Bearer Token}
Accept-Encoding: gzip, deflate
```
The response has a lot of data, but the first part looks pretty interesting
```=json
{
    "response":{
        "user":{
            "_type":"user",
            "id":"6266cd58b5e1341bb476f697",
            "name":"JeffBayzoss",
            "gender":1,
            "age":23,
            "lastOnlineTime":1654364115,
            "whazzup":"",
            "freetext":"I enjoy pina coladas, getting caught in the rain, and making love at midnight.",
            "subscriptions":[
            ],
            "isVip":0,
            "flirtInterests":[
                "frie",
                "chat"
            ],
            "options":{
                "profileShareable":1
            },
            "compatibilityQuestionsAnswered":0,
            "counts":{
                "v":45,
                "l":1,
                "pp":83,
                "p":1,
                "m":1,
                "ib":0
            },
            "credits":6,
            "locations":{
                "home":{
                    "city":"Vienna",
                    "country":"AT",
                    "lat":48.18633,
                    "lon":16.323064
                },
                "current":{
                    "city":"Graz",
                    "country":"AT",
                    "lat":47.0707133,
                    "lon":15.4395033
                },
                "billing":{
                    "country":"US"
                }
            },
            "isNew":0,
            "isOnline":1,
            "isMobile":1,
            "isHighlighted":0,
            "picture":"62767fb02a175046ef7c7350",
            "images":[
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/image.jpg",
                    "width":365,
                    "height":481
                },
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/image_l.jpg",
                    "width":365,
                    "height":481
                },
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/image_m.jpg",
                    "width":365,
                    "height":481
                },
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/image_s.jpg",
                    "width":243,
                    "height":320
                },
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/thumb_xl.jpg",
                    "width":320,
                    "height":320
                },
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/thumb_l.jpg",
                    "width":160,
                    "height":160
                },
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/thumb_m.jpg",
                    "width":120,
                    "height":120
                },
                {
                    "url":"https:\/\/img.lovoo.com\/users\/pictures\/62767fb02a175046ef7c7350\/thumb_s.jpg",
                    "width":80,
                    "height":80
                }
            ],
            "email":"jeff.bayzoss@gmail.com",
            "birthday":"30.08.1998",
            "isConfirmed":0,
            "registerDate":1650904408,
            "apps":[
                "lovoo"
            ],
            "interests":[
                "frie",
                "chat"
            ],
            "genderLooking":2,
            "languages":[
                "en",
                "de"
            ],
            "promoconsent":0,
            "settings":{
                "screensaver":0,
                "share_profile_disabled":0,
                "radar_disabled":0,
                "match_disabled":0,
                "ads_gps_disabled":0,
                "ads_personalized_disabled":0,
                "push_intensity":"all",
                "gps":1,
                "sounds":1,
                "push":1,
                "push_msg":1,
                "push_visit":1,
                "push_match":1,
                "push_info":1,
                "push_comments":1,
                "push_likes":1,
                "push_follow":1,
                "push_match_vote":1,
                "push_reply":1,
                "message_preview":1,
                "push_video_nearby":1,
                "push_video_favorite":1,
                "push_video_favorite_blast":1,
                "push_best_picks":1
            },
            "searchSettings":{
                "ageFrom":18,
                "ageTo":25,
                "radius":500,
                "matchRadius":0,
                "gender":2
            },
            "app":"12601",
            "verifications":{
                "facebook":0,
                "verified":0,
                "confirmed":0
            },
            "verificationStatus":0,
            "resources":{
                "icebreaker":{
                    "slotsLeft":3,
                    "slotLimit":3,
                    "refillInterval":86400,
                    "refillTime":0,
                    "slotsExtra":0,
                    "slotsNotify":0
                },
                "boost":0,
                "boost_refill_time":0
            }
        }
    }
}
```
It looks like the app has saved the "home" location and tracks the current location. In the last part of the response is a tag "homeLocation":1.

## Obtaining other users data

When going to the match section the app sends a request to load in user charts for voting. The request contains a filter like gender, age, but also the current location.
```
GET /matches?gender=2&ageFrom=18&ageTo=25&lat=47.0707133&long=15.4395033&limit=30 HTTP/2
Host: api.lovoo.com
```

The API then responds with users, who match the filter and sends their data.
```=json
{
    "response":{
        "result":[
            {
                "_type":"user",
                "id":"514bf0cb150ba0e941000331",
                "name":"Victoria",
                "gender":2,
                "age":24,
                "lastOnlineTime":1654224749,
                "whazzup":"Bundesheer? Bitte, danke",
                "subscriptions":[
                ],
                "isVip":0,
                "flirtInterests":[
                    "date",
                    "frie"
                ],
                "options":{
                    "profileShareable":1
                },
                "counts":{
                    "p":15,
                    "m":10
                },
                "possibleMatch":0,
                "locations":{
                    "home":{
                        "city":"Graz",
                        "country":"AT",
                        "distance":2.7
                    },
                    "current":{
                        "city":"Graz",
                        "country":"AT",
                        "distance":1.2
                    },
                    "billing":{
                        "country":"AT"
                    }
                },
                "isNew":0,
                "isOnline":0,
                "isMobile":1,
                "isHighlighted":0,
                "picture":"62250c4c515cd339521aa842",
                "images":[
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/image.jpg",
                        "width":960,
                        "height":1280
                    },
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/image_l.jpg",
                        "width":720,
                        "height":960
                    },
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/image_m.jpg",
                        "width":480,
                        "height":640
                    },
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/image_s.jpg",
                        "width":240,
                        "height":320
                    },
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/thumb_xl.jpg",
                        "width":320,
                        "height":320
                    },
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/thumb_l.jpg",
                        "width":160,
                        "height":160
                    },
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/thumb_m.jpg",
                        "width":120,
                        "height":120
                    },
                    {
                        "url":"https:\/\/img.lovoo.com\/users\/pictures\/62250c4c515cd339521aa842\/thumb_s.jpg",
                        "width":80,
                        "height":80
                    }
                ],
                "verifications":{
                    "facebook":1,
                    "verified":1,
                    "confirmed":1
                },
                "verificationStatus":1
            }
...
```
This response contains some interesting data that could be used maliciously.
Besides the userid and a possibleMatch prediction, we get the last online time "1654224749". Converting that from UNIX Timestamp with units in seconds, we get "Fri 3 June 2022 02:52:29 UTC".
The API sends the home and current location with the actual distance to the suggested user:
```=json
"locations":{
            "home":{
                    "city":"Graz",
                    "country":"AT",
                    "distance":2.7
                   },
           "current":{
                      "city":"Graz",
                      "country":"AT",
                      "distance":1.2
                     },
          "billing":{
                      "country":"AT"
                    }
            }
```
Additionally the response contains tags like isNew, isOnline, isMobile, verification with facebook and the link to the picture.
At the end of the response it shows us the remaining votes count
```
"allCount":30,"votesLeft":30,"timeToNewVotes":1
```
Thereafter the app sends a POST request containing all the user ids it has loaded with the request before. 
```
POST /users/6266cd58b5e1341bb476f697/connections_multi HTTP/2
Host: api.lovoo.com
```
The response shows the relationship to these users
```=json
"5f1ba612d1e9903275732b32":{
    "isMatch":0,
    "hasLiked":0,
    "icebreakerState":0,
    "hasContact":0
    }
```

## Direct profile access

When clicking on a profile of another user the app makes a few requests:
It makes a POST request with the id it wants to load
```
POST /users/6266cd58b5e1341bb476f697/connections_multi HTTP/2
Host: api.lovoo.com
...
ids=5ffdfaedd31a33034b422abd
```
Then loads some facts about the user where the app gets some data.
```
GET /users/5ffdfaedd31a33034b422abd/facts HTTP/2
Host: api.lovoo.com
```
In this data is the actual search setting age range of the user looking at, interests and data like height, home location, ...
```=json
{
    "response":{
        "gender_looking":"1",
        "searchsettings_age_from":19,
        "searchsettings_age_to":25,
        "locationhome_city":"Sankt P\u00f6lten",
        "locationhome_country":"AT",
        "locationhome_lat":0,
        "locationhome_long":0,
        "interests":[
            "chat"
        ],
        "whazzup":"",
        "languages":[
            "de",
            "en"
        ],
        "match_disabled":0,
        "interview_size":"s23",
        "interview_size_cm":162
    },
...
}
...
```
It also loads in more data with the request
```
GET /users/5ffdfaedd31a33034b422abd/feed?resultLimit=40&sort=distance HTTP/2
Host: api.lovoo.com
...
```
But the data in the response looks similar to that returned in the match request. With this request the app gets again the pictures and other basic facts (somehow it's an array with 7 times the same struct in it).

The app again loads data with the following two requests:

```
GET /users/5ffdfaedd31a33034b422abd/freetext HTTP/2
Host: api.lovoo.com
...
```
```
GET /prompts/5ffdfaedd31a33034b422abd HTTP/2
Host: api.lovoo.com
...
```
These just load the texts and question - answer prompts of the user.

Finally the app makes a POST request to the visit endpoint, to show the other user, that I clicked on the profile and where I did that.
```
POST /users/5ffdfaedd31a33034b422abd/visits HTTP/2
Host: api.lovoo.com
...
ref=match
```

This app links photos of the user staticly, but has uses instead of the user id a unrelated picture id
```=json
"id":"628e8f3ce42e4d62eb00ad6e"
"url":"https:\/\/img.lovoo.com\/users\/pictures\/628e8f40a5457d5e181ff973\/image.jpg"
```

## Investigating premium functions

On the app this can be watched in the "News" section. The feature only shows the profiles unblurred with an upgraded account. Looking at the response of the load request in this section showed that without an upgraded account, the app gets encrypted user ids, blurred images but still the home and current location (without the exact distance).
```=json
{
...
    "_type":"visit",
    "id":"CRYPKDc0t9vW+EPsWHs70PSaNhcLpSTPJbUhBeAFBIro4w=",
    "user":{
        "_type":"user",
        "id":"CRYPKDc0t9vW+EPsWHs70PSaNhcLpSTPJbUhBeAFBIro4w=",
        "name":"Ceci",
        "gender":2,
        "age":20,
        "lastOnlineTime":1654511814,
        "whazzup":"",
        "freetext":"Ich mag Pizza, Sushi und Harry Potter. \n\nWenn du ein Hund oder eine Katze hast, oder T\u00e4towierer bist, hast du schon gewonnen!",
        "subscriptions":[
        ],
        "isVip":0,
        "flirtInterests":[
            "frie"
        ],
        "options":{
            "profileShareable":1
        },
        "counts":{
            "p":1,
            "m":4
        },
        "isLocked":1,
        "locations":{
            "home":{
                "city":"Kapfenberg",
                "country":"AT"
            },
            "current":{
                "city":"Deuchendorf",
                "country":"AT"
            },
            "billing":{
                "country":"AT"
            }
        },
        "isNew":0,
        "isOnline":0,
        "isMobile":1,
        "isHighlighted":0,
        "picture":"28912190f25ee452c9baa29819d8be3d",
        "images":[
            {
                "url":"https:\/\/img.lovoo.com\/users\/pictures\/28912190f25ee452c9baa29819d8be3d\/thumb_xl.jpg",
                "width":320,
                "height":320
            },
            {
                "url":"https:\/\/img.lovoo.com\/users\/pictures\/28912190f25ee452c9baa29819d8be3d\/thumb_l.jpg",
                "width":160,
                "height":160
            },
            {
                "url":"https:\/\/img.lovoo.com\/users\/pictures\/28912190f25ee452c9baa29819d8be3d\/thumb_m.jpg",
                "width":120,
                "height":120
            },
            {
                "url":"https:\/\/img.lovoo.com\/users\/pictures\/28912190f25ee452c9baa29819d8be3d\/thumb_s.jpg",
                "width":80,
                "height":80
            }
        ],
        "verifications":{
            "facebook":0,
            "verified":0,
            "confirmed":1
        },
        "verificationStatus":0
    },
    "unlocked":0,
    "time":1654501242

},
...}
```
In this data are "isLocked" and "unlocked" tags. Intercepting the response and changing these lets skipping the upgrading and tries to load the profile. But the user ids are still encrypted and therefore the load requests fail with a unknown user error message. Investigating the "likes you" section reveals the same issue.

## Liking process
The match request to vote contains the target user id. Trying to change the values to get some interesting results didn't work.
```
POST /matches/629cedf7e6166b0f82556935 HTTP/2
Host: api.lovoo.com
...
vote=1&ref=direct%2Cmatch&dwell_time=1959
```
So the liking process on this app seems to be straight forward.

## Tracking

To track user activity for reasons like marketing, the app sends following requets with encrypted data to the so called "AppLovin" service.
```
POST /1.0/event/load?id=99ed804848a284ccc2c5ed1c1036cc7c5f90432c&load_time_ms=223&postback_ts=1654701969116 HTTP/2
Host: prod-ms.applovin.com
```
```
POST /1.0/event/load?id=c0f8b73a85d500b3ee038b0e5884f24eb30d7d71&load_time_ms=60&postback_ts=1654701992235 HTTP/2
Host: stage-ms.applovin.com
```
```
POST /1.0/mediate?p=1%3A96943fdea087a1d759e08734fce0068af23ef96e%3AWGUTRJff5vD55Paf-9cSLJ84TV6pnUas3JefM3thUQJ6QpVbKwF4Ly%3AMMPK3XoTuUjbcwDnQ9MFGeYLFPqCWyE7FrXUHjD-J4KOB8wezjR0WZIIrA-B6LRMSaskbRjPWiDXrtaGbCyT_g** HTTP/2
Host: ms4.applovin.com
```
AppLovin is a marketing and advertising service which helps to analyze user behaviour.

Source: https://en.wikipedia.org/wiki/AppLovin

## Conclusion
Lovoo gives away some information about its users. Looking at the data the app loads from a user, we know their location, if the user is online at the moment, the last time online, their search settings and so on. 
Around 6 years ago a user created a tool to calculate users location with requests to the API. This could easily be adapted and used for malicious reasons with state of the communication in this point of time.

Source: https://github.com/posixpascal/lovoo-data-breach