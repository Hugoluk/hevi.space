---
title: "Mobile Security Tinder Report"
url: /posts/"
summary: Analysis of Tinder
tags:
    - Mobile Security
    - Assignment 2
    - Tinder
---

## Description
Tinder is the most popular or better most common dating app nowadays. The name Tinder comes from an easily combustible material used to start a fire. It advertises with the simple method of swiping left or right on a users profile if they like them or dislike them. If both users like each other a so called match is made and they can start a conversation.
It's very well made and also very simple in use. Because it has grown so big we didn't expect to find much on this app. But for completeness we have investigated this app as well.

Source: https://tinder.com/about-tinder

**Device used:** Android emulator Pixel 4 Android 10 API level 29, x86

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
12. Future work

## Registration process
In the registration process was nothing noticeable to be found besides that the Russian phone number doesn't work anymore.

## Login process
Starting up the app makes some init requests with collecting some data about the device. One of them has a lot of interesting tags in it:
```=json
POST /v1/open HTTP/2
Host: api2.branch.io
...
{
    "device_fingerprint_id":"1062755633515839194",
    "identity_id":"1062755634115628367",
    "hardware_id":"bca0d57693dc1b8b",
    "is_hardware_id_real":true,
    "brand":"Google",
    "model":"Android SDK built for x86",
    "screen_dpi":440,
    "screen_height":1977,
    "screen_width":1080,
    "wifi":true,
    "ui_mode":"UI_MODE_TYPE_NORMAL",
    "os":"Android",
    "os_version":29,
    "country":"US",
    "language":"en",
    "local_ip":"10.0.2.15",
    "app_version":"13.6.1",
    "facebook_app_link_checked":false,
    "is_referrable":1,
    "debug":false,
    "update":1,
    "latest_install_time":1654617540261,
    "latest_update_time":1654617540261,
    "first_install_time":1654617540261,
    "previous_update_time":1654617540261,
    "environment":"FULL_APP",
    "cd":{
        "mv":"-1",
        "pn":"com.tinder"
    },
    "metadata":{
    },
    "google_advertising_id":"d104807b-7db9-4aa8-b9af-47d3efcde938",
    "lat_val":0,
    "instrumentation":{
        "v1\/open-qwt":"0"
    },
    "sdk":"android4.0.0",
    "branch_key":"key_live_mhkKfK7Br0UHcrNnmV6CVhbosDoGS8JH",
    "retryNumber":0
}
```
Besides the fingerprints of the device it tracks "is_hardware_id_real", if it's connected to the wifi, "local_ip", "latest_install_time", "first_install_time", "latest_update_time" and "previous_update_time".

After that the app sends the current location to the API.
```
POST /v2/meta HTTP/2
Host: api.gotinder.com
...
{"lat":47.0707133,"lon":15.4395033,"force_fetch_resources":true}
```
## Obtaining other users data
Clicking on the "main" tab, where the user can vote sends following request to load the user cards in.
```
GET /v2/recs/core?locale=en HTTP/2
Host: api.gotinder.com
```
The response to this gives us some data about the user:
```=json
{
    "type":"user",
    "user":{
        "_id":"62923183cc00110100309cee",
        "badges":[
        ],
        "bio":"running & \uD83C\uDF55",
        "birth_date":"1994-06-10T16:21:50.584Z",
        "name":"Anita",
        "photos":[
        ],
        "gender":1,
        "jobs":[
        ],
        "schools":[
            {
                "name":"Karl-Franzens-Universität Graz"
            }
        ],
        "city":{
            "name":"Graz"
        },
        "is_traveling":false,
        "show_gender_on_profile":true,
        "recently_active":true,
        "online_now":false,
        "selected_descriptors":[
        ]
    },
    "facebook":{
        "common_connections":[
        ],
        "connection_count":0,
        "common_interests":[
        ]
    },
    "spotify":{
    },
    "distance_mi":1,
    "content_hash":"6P8UoMck7HLF0pIa5f3LHbJI7bcl2CLMTaIPzcLhm9hp1",
    "s_number":1883739694839039,
    "teaser":{
        "type":"school",
        "string":"Karl-Franzens-Universität Graz"
    },
    "teasers":[
        {
            "type":"school",
            "string":"Karl-Franzens-Universität Graz"
        }
    ],
    "experiment_info":{
    },
    "is_superlike_upsell":true,
    "tappy_content":[
    ]
}
```
In this data is the name, birthdate, school but also the distance in miles. More intersting are the tags "is_traveling", "recently_active" and "online_now". But besides that, it doesn't show much. 

## Direct profile access

Looking at the communication when clicking on a user shows a response with almost equal data, with not much revealing data of the user.
```=json
"status":200,
"results":{
    "common_friends":[
    ],
    "common_friend_count":0,
    "spotify_top_artists":[
    ],
    "distance_mi":1,
    "connection_count":0,
    "common_connections":[
    ],
    "bio":"\uD83D\uDC83\uD83C\uDFFC\uD83C\uDFC3\uD83C\uDFFC‍",
    "birth_date":"1994-06-10T16:53:44.966Z",
    "name":"Melanie",
    "jobs":[
    ],
    "schools":[
        {
            "name":"University of Graz",
            "displayed":false
        }
    ],
    "teasers":[
        {
            "type":"sameSchool",
            "string":"University of Graz"
        }
    ],
    "gender":-1,
    "show_gender_on_profile":false,
    "birth_date_info":"fuzzy birth date active, not displaying real birth_date",
    "ping_time":"2014-12-09T00:00:00.000Z",
    "badges":[
    ],
    "photos":[],
    "user_interests":{
        "selected_interests":[
            {
                "id":"it_4",
                "name":"Running"
            },
            {
                "id":"it_28",
                "name":"Reading"
            },
            {
                "id":"it_2016",
                "name":"Dancing"
            },
            {
                "id":"it_10",
                "name":"Brunch"
            },
            {
                "id":"it_7",
                "name":"Travel"
            }
        ]
    },
    "common_likes":[
    ],
    "common_like_count":0,
    "common_interests":[
    ],
    "s_number":3805960890940599,
    "_id":"62817714cfd03201005c2335",
    "is_tinder_u":false
}
```

## Investigating premium functions

The app regularly makes following request where it checks if the user is "boosting" (becomes more suggested to other users).
```
POST /updates?is_boosting=false&boost_cursor=0 HTTP/2
Host: api.gotinder.com
...
{"last_activity_date":"2022-06-07T16:20:00.046Z"}
```
The response has some interesting fields in it with matches, harassing_messages, blocks, etc. ...
```=json
{
    "matches":[
    ],
    "blocks":[
    ],
    "inbox":[
    ],
    "liked_messages":[
    ],
    "harassing_messages":[
    ],
    "lists":[
    ],
    "goingout":[
    ],
    "deleted_lists":[
    ],
    "matchmaker":[
    ],
    "squads":[
    ],
    "last_activity_date":"2022-06-07T16:20:00.046Z",
    "poll_interval":{
        "standard":2000,
        "persistent":120000
    }
}
```
In combination with the request when clicking on the boost icon:
```
POST /boost HTTP/2
Host: api.gotinder.com
```
I thought that could be manipulated to get an effect.
So I tried to change the request before to
```
POST /updates?is_boosting=true&boost_cursor=1 HTTP/2
```
everytime the app would send it and intercepting and changing the response from the boost icon like this.
```=json
{
    "duration":1800000,
    "allotment":1,
    "allotment_used":0,
    "allotment_remaining":1,
    "internal_remaining":1,
    "purchased_remaining":1,
    "remaining":1,
    "boost_refresh_amount":1,
    "boost_refresh_interval":1,
    "boost_refresh_interval_unit":"m",
    "out_of_boost":false
}
```
Repeating this some time trying to trick the app into thinking we have purchased a boost, gave on time a successful popup!
![](https://i.imgur.com/6a4MplE.png)

After that the app made some of these requests over some time:
```
GET /v2/profile?include=boost HTTP/2
Host: api.gotinder.com
```
But besides that we didn't have an indicator to see if it really worked.
Some time later Tinder locked the account because of supicious activity until we verify our profile.

## Liking process
The liking process on this app is really straight forward. With a request to this endpoint, the app sends how the user liked the other user.
```=json
POST /like/6289d98ccfd03201005ee2e4 HTTP/2
Host: api.gotinder.com
...
{
    "photoId":"30e94e1c-463d-4c80-90b9-389574ecf2a7",
    "content_hash":"RX8iwbIl2HZhMbhx2SZ5i5qHE3c93cDbheMUZQhXzi5rtmN",
    "super":0,
    "fast_match":0,
    "top_picks":0,
    "undo":0,
    "s_number":7248806679023904
}
```
The app gets a response with a status, a tag if a match happend and the remaining likes.
```
"status":200,"match":false,"likes_remaining":100,"X-Padding":...
```
The response on the other hand is to a other endpoint but with the info in the parameters. 
```
GET /pass/5e2c8af6f057db0100f5f9b9?photoId=4a09f78d-6b36-4e1f-9621-8b0ef2890cb4&content_hash=RX3CGUrjIaEt2pcxOfZlHVFEwFGS8VTghdeCrXuRf55&s_number=5848852989094555 HTTP/2
Host: api.gotinder.com
```
Other then that here isn't really anything interesting to be found within the liking process.

## Tracking
The app regularly checks if it's in background.
```
GET /v2/device-check/android?background=0 HTTP/2
Host: api.gotinder.com
```
It also makes POST requests with users coordinates to update them.
```
POST /v2/meta HTTP/2
Host: api.gotinder.com
...
{"lat":47.0707133,"lon":15.4395033,"force_fetch_resources":true}
```
This request, described above, is really regularly made. Maybe related to the boosting function, which is time based (half an hour once activated).
```
POST /updates?is_boosting=false&boost_cursor=0 HTTP/2
```
This request is made to a marketing service. I think for tracking purposes.
```
POST /api/v6.3/androidevent?app_id=com.tinder&buildnumber=6.3.1 HTTP/2
Host: inapps.appsflyer.com
```
## Conclusion
The app is really well made and we didn't find that much on this app. Not much of user data is leaked to other users especially in comparison to other dating apps. There is still some strange tracking with coordinates, "is_traveling" tag and the data pulled out of the device after login.

## Future work
A deeper investigation of the boost activation with request could be interesting. A comparison how the app acts, when a boost is purchased, and how its visible for other user is necessary.