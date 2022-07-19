---
title: "Mobile Security: Her report"
url: /her/"
summary: Analysis of Her
tags:
    - Mobile Security
    - Assignment 2
    - Her
---

## Description

Her, formerly Dattch, is a geosocial networking app geared towards lesbian, queer, bisexual, and straight women and non-binary people.  Cisgender men are not allowed to create profiles on the platform. (Source: https://en.wikipedia.org/wiki/Her_(dating_app))

From a technical standpoint it is a typical dating app with swiping left and right for liking or ignoring a potential match. 

**Device used:** Huawei P9 lite, Android 7.0 API Level 24, arm64_v8a

## Structure of the report

1. Description
2. Registration process
3. Login process
5. Public profile structure
6. Obtaining other users data
7. Direct profile access
8. Other ways of getting user profiles
9. Tracking
10. Conclusion
11. Future work

**CORRECT!!**

## Registration process

Let's first look into registration process.
One can register into *Her dating app* with phone number, Facebook or Instagram. Our registration was done with a phone number.
On the API side this looks this:

`POST https://api.weareher.com/v4/login/phonenumber/start HTTP/2.0`
Query:
```=json
{
    "phone_number": "+4367764289***" #Omited for author privacy reasons
}
```
Response:
```=json
true
```

And then checking the code sent by SMS to the phone.

`POST https://api.weareher.com/v4/login/phonenumber/confirm HTTP/2.0`
Query:
```=json
{
    "phone_number": "+4367764289912",
    "verification_code": 8341
}
```

 *Her* backend already makes a user account. (This is speculation but based on our experience highly likely.) From here on out, registration enters the *"Pre user"* mode. More data for registration is collected.

`PATCH https://api.weareher.com/v4/login/preusers/update HTTP/2.0`
Query:
```=json
{
    "dob": 861408016,
    "email": "lightning5.test@gmail.com",
    "name": "Gaja Novak"
}
```
In response we see how our public user account looks now
Response:
```=json
{
    "dob": 861408016,
    "email": "lightning5.test@gmail.com",
    "name": "Gaja Novak",
    "preuser": true,
    "profile_dynamic": {
        "available": false,
        "distance": 0,
        "friend_count": 0,
        "friendship_status": "",
        "future_event_count": 0,
        "id": 0,
        "liked_by_user": false,
        "matched": false,
        "moderator": false,
        "name": "",
        "online": false,
        "past_event_count": 0,
        "username": ""
    },
    "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjo1NDIxMjQxLCJleHAiOjE2NTQ3ODQ4NjV9.dF3OQcGeqVLKbO7iFbrEofwDWuroGo89zk7lRcpifK39Ip7c4zktE7UcXyCGBsZD_1N3ej3nYp96nhv1_0Erj4FM_umz94yGtskd--R8ctR43sfo6keQ86SEnw90orw4uN9-p1wLektAkXRs4qPQeOKZN6CEO68D9vGngsb4pZG0daVZNqfbuAjfy7aDlMBIhvJXVxE4bR3h-YOYbc2nGtseU3TKLKmWthoOyhr7sVv5qH6CTncWbUJ18jy6vysiQj0lqwJT9AYoaiWgrs6AJH6AJFwDWAQs_qHmjecaw03SByXq_NoBRMXu-xgb7A5aghwH7TVQUtGpRQh-zE3p2w"
}
```

At the end of the registration process, there are some questions that are available on the public profile and for the *Her* algorithm to recommend new matches. 
This part is omitted since it doesn't contain any interesting information.

No vulnerabilities were found during the registration process.


## Log in
Log in is simply made with an auth token. In response, we get our profile data.


`GET https://api.weareher.com/v4/login/profile HTTP/2.0`

x-authorization:
```
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjo5NzkwMzg4LCJleHAiOjE2ODYwODUzNTB9.bmoV1Z3TFH6r9oKm39a9N-UTDqfCgGQBTCI3zcSoKrD7hz3NPAu8UyxMlrRgkRfpzQCh-ICzrlxa290rNQy2AfidBjpFanzdJAFqKoYhFXCJZHosyea_mbzWEAjHa4TKUo79hhV8-epmxz2gVxsFPu0Hhb1QhWUY_5ftkypfoZc
```

Response
```
{
    "completeness": 52,
    "consumables_inventory": {
        "boosts": 0
    },
    "data_access": 1,
    "dob": 865555200,
    "email": "...REDACTED FOR AUTHOR PRIVACY... (confirm address to apply change)",
    "email_change_request": {
        "email": "...REDACTED FOR AUTHOR PRIVACY..."
    },
    "has_password": false,
    "phone_number": "",
    "profile_dynamic": {
        "about": "",
        "age": 25,
        "available": true,
        "distance": 0,
        "feed_post_count": 0,
        "friend_count": 0,
        "friendship_status": "none",
        "future_event_count": 0,
        "height": 63.385826,
        "id": 9790388,
        "liked_by_user": false,
        "matched": false,
        "moderator": false,
        "name": "Nika",
        "online": true,
        "past_event_count": 0,
        "profile_image": {
            "id": 77358906,
            "url": "https://cdnimages.weareher.com/p/5423457_p_1654548810_cz5uA3esk7qGBTahIKBmffMqlos2sSx7XP3nkpGV_img.jpeg"
        },
        "properties": [
            {
                "category_key": "identity",
                "for_filter": true,
                "id": 2,
                "key": "gender",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Gender Fluid",
                        "id": 13
                    }
                ]
            },
            {
                "category_key": "identity",
                "for_filter": true,
                "id": 4,
                "key": "sexuality",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Bisexual",
                        "id": 31
                    }
                ]
            },
            {
                "category_key": "identity",
                "for_filter": true,
                "id": 6,
                "key": "pronoun",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "She/her",
                        "id": 1
                    }
                ]
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_relationshipstatus.png",
                "id": 3,
                "key": "relationship_status",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Single",
                    "id": 50
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_height.png",
                "id": 1,
                "key": "height",
                "selection": "single",
                "type": "number",
                "value": 63.4
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_lookingfor.png",
                "id": 8,
                "key": "looking_for",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Monogamous relationship",
                        "id": 56
                    },
                    {
                        "display": "Polyamorous relationship",
                        "id": 57
                    },
                    {
                        "display": "Something casual",
                        "id": 58
                    },
                    {
                        "display": "New friends",
                        "id": 59
                    }
                ]
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_drinking.png",
                "id": 9,
                "key": "drinking",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Socially",
                    "id": 64
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_smoking.png",
                "id": 10,
                "key": "cigarettes",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Socially",
                    "id": 67
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_weed.png",
                "id": 11,
                "key": "cannabis",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "No",
                    "id": 70
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_astrologicalsign.png",
                "id": 15,
                "key": "star_sign",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Gemini",
                    "id": 106
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_pets.png",
                "id": 16,
                "key": "pets",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Dogs",
                        "id": 113
                    },
                    {
                        "display": "Cats",
                        "id": 114
                    }
                ]
            }
        ],
        "spotify": {
            "artists": null,
            "auth_state": "initial",
            "username": ""
        },
        "username": "0GE8DVX1WEND"
    },
    "push_notifications": [
        {
            "category_identifier": 1,
            "category_subtitle": "",
            "category_title": "Community + Events",
            "name": "Friends request",
            "param": "friend-requests",
            "should_display_pref_as_sub_category": false,
            "subcategory": "",
            "value": true
        },
        {
            "category_identifier": 1,
            "category_subtitle": "",
            "category_title": "Community + Events",
            "name": "Post comments & replies",
            "param": "post-comments-replies",
            "should_display_pref_as_sub_category": false,
            "subcategory": "",
            "value": true
        },
        {
            "category_identifier": 1,
            "category_subtitle": "",
            "category_title": "Community + Events",
            "name": "Event updates",
            "param": "event-updates",
            "should_display_pref_as_sub_category": false,
            "subcategory": "",
            "value": true
        },
        {
            "category_identifier": 2,
            "category_subtitle": "",
            "category_title": "App Updates",
            "name": "Important app news",
            "param": "app-news",
            "should_display_pref_as_sub_category": false,
            "subcategory": "",
            "value": true
        },
        {
            "category_identifier": 3,
            "category_subtitle": "",
            "category_title": "Discounts",
            "name": "Discounts and offers from HER",
            "param": "discounts-and-offers",
            "should_display_pref_as_sub_category": false,
            "subcategory": "",
            "value": true
        },
        {
            "category_identifier": 4,
            "category_subtitle": "Dating Push Settings",
            "category_title": "Dating",
            "name": "Messages",
            "param": "messages",
            "should_display_pref_as_sub_category": true,
            "subcategory": "Dating preferences",
            "value": true
        },
        {
            "category_identifier": 4,
            "category_subtitle": "Dating Push Settings",
            "category_title": "Dating",
            "name": "Matches",
            "param": "matches",
            "should_display_pref_as_sub_category": true,
            "subcategory": "Dating preferences",
            "value": true
        },
        {
            "category_identifier": 4,
            "category_subtitle": "Dating Push Settings",
            "category_title": "Dating",
            "name": "Likes",
            "param": "likes",
            "should_display_pref_as_sub_category": true,
            "subcategory": "Dating preferences",
            "value": true
        }
    ],
    "signup": false,
    "spotify": {
        "artists": null,
        "auth_state": "initial",
        "username": ""
    },
    "status": "approved",
    "test_user": false,
    "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjo5NzkwMzg4LCJleHAiOjE2ODYwODUzNTB9.bmoV1Z3TFH6r9oKm39a9N-UTDqfCgGQBTCI3zcSoKrD7hz3NPAu8UyxMlrRgkRfpzQCh-ICzrlxa290rNQy2AfidBjpFanzdJAFqKoYhFXCJZHosyea_mbzWEAjHa4TKUo79hhV8-epmxz2gVxsFPu0Hhb1QhWUY_5ftkypfoZc",
    "verified_status": {
        "challenge_image_url": "https://cdnimages.weareher.com/static/challenge_hI4UpWQ04rC8sU4Ag4m42rwZFz3mMlfxtBYE8VQ1.jpg",
        "show_initial_alert": true,
        "status": "initial"
    }
}
```



### Public profile structure

Every user on *Her* has a so-called dynamic profile. This are the things that are publicly available about every user you encounter (more on that later). It contains static information such as id, name, height, as well as data that changes such as online status, liked_by_user, and even data that changes from the perspective of a viewer, such as distance.

```=json
{
	"profile_dynamic": {
        "about": "",
        "age": 25,
        "available": true,
        "distance": 0,
        "feed_post_count": 0,
        "friend_count": 0,
        "friendship_status": "none",
        "future_event_count": 0,
        "height": 63.385826,
        "id": 9790388,
        "liked_by_user": false,
        "matched": false,
        "moderator": false,
        "name": "Nika",
        "online": true,
        "past_event_count": 0,
        "profile_image": {
            "id": 77358906,
            "url": "https://cdnimages.weareher.com/p/5423457_p_1654548810_cz5uA3esk7qGBTahIKBmffMqlos2sSx7XP3nkpGV_img.jpeg"
       }
}
```

Out of available data `liked_by_user` might interest us, to guarantee an instant match. Another hidden attribute that might give an advantage in getting more dates is `friend_count` to see how "experienced"/versed is a user that we are talking to.
Knowing if we are talking to a `moderator`, might help a malicious/abusive user to evade detection. `online` and `distance` can be used to track a person or get more personal data.

Using for example a GPS spoofer could enable us to obtain the distance between us and a user can enable us to triangulate the approximate location of the user. `Distance` is measured in 0,1 of a mile.

**add somewhere**
Height is in inches


### Obtaining other users data

When entering the app to start swiping for new matches, information of other users needs to be obtained by the app. Search parameters (min_age, max_age, max_distance) are sent to *Her* to the API. API returns dynamic profiles (mentioned in the previous chapter) of *all* users that conform to the search parameters.
The problem in this response is that we don't get access to one or ten users that we might encounter during swiping, but literally all of them. The response is 42 kb and contains all users within a 5-mile radius of the testing phone. Information of all users can be processed and mined. In case location tracking is possible (not tested), mass tracking of every user in the radius could be feasible.

`GET https://api.weareher.com/v4/profiles?min_age=18&max_age=33&max_distance=50 HTTP/2.0`

Request:
```=json
min_age:      18
max_age:      33
max_distance: 50
```

Response:
~42 kb of data

Shortened example response
```=json
[
    {
        "about": "",
        "age": 18,
        "available": true,
        "distance": 15,
        "feed_post_count": 0,
        "friend_count": 0,
        "friendship_status": "none",
        "future_event_count": 0,
        "height": 68.89764,
        "id": 9781125,
        "images": [
            {
                "id": 77306000,
                "url": "https://cdnimages.weareher.com/p/5413183_p_1654431397_5k3lgjWLa55WDLfRxkwTR5LW7QZzmgyABbcdTsL7_img.jpeg"
            },
            {
                "id": 77306001,
                "url": "https://cdnimages.weareher.com/p/5413183_p_1654431411_ypYMdfTwwMaejJRT4JF3Dbouy5COyhkRdSHqLVMq_img.jpeg"
            }
        ],
        "liked_by_user": false,
        "matched": false,
        "moderator": false,
        "name": "Lisa",
        "online": false,
        "past_event_count": 0,
        "profile_image": {
            "id": 77305999,
            "url": "https://cdnimages.weareher.com/p/5413183_p_1654431381_IjrMDgk9iNAc1k5IRgWr7htLumJdu8iVBaFnpWr4_img.jpeg"
        },
        "properties": [
            {
                "category_key": "identity",
                "for_filter": true,
                "id": 2,
                "key": "gender",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Woman",
                        "id": 142
                    }
                ]
            },
            {
                "category_key": "identity",
                "for_filter": true,
                "id": 4,
                "key": "sexuality",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Questioning",
                        "id": 37
                    }
                ]
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_relationshipstatus.png",
                "id": 3,
                "key": "relationship_status",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Single",
                    "id": 50
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_height.png",
                "id": 1,
                "key": "height",
                "selection": "single",
                "type": "number",
                "value": 68.9
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_lookingfor.png",
                "id": 8,
                "key": "looking_for",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Something casual",
                        "id": 58
                    }
                ]
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_drinking.png",
                "id": 9,
                "key": "drinking",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Occasionally",
                    "id": 63
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_smoking.png",
                "id": 10,
                "key": "cigarettes",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Regularly",
                    "id": 68
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_weed.png",
                "id": 11,
                "key": "cannabis",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "No",
                    "id": 70
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_astrologicalsign.png",
                "id": 15,
                "key": "star_sign",
                "selection": "single",
                "type": "integer",
                "value": {
                    "display": "Gemini",
                    "id": 106
                }
            },
            {
                "category_key": "fun_facts",
                "for_filter": true,
                "icon_url": "https://cdnimages.weareher.com/static/funfacts_pets.png",
                "id": 16,
                "key": "pets",
                "selection": "multiple",
                "type": "integer",
                "values": [
                    {
                        "display": "Dogs",
                        "id": 113
                    },
                    {
                        "display": "Cats",
                        "id": 114
                    }
                ]
            }
        ],
        "recommender": "recommender2",
        "spotify": {
            "artists": null,
            "auth_state": "initial",
            "username": ""
        },
        "username": "3oKyAQqg6KVl"
    }, {and so on ... snip ...} ]
```

### Direct profile access

After digging deeper we also found an API call that gives information about a specific user. To get specific users' information we provide user ID, which is available in `/profiles` API call.


`GET https://api.weareher.com/v4/profiles/9433981 HTTP/2.0`

```=json
{
    "about": " Nähe Graz 🇦🇹🏳️‍🌈 REDACTED\n",
    "age": 18,
    "answers": [
        {
            "answer": "Löwe, Zwilling und Stier ",
            "id": 23,
            "question": "My sun, moon, and rising signs"
        },
        {
            "answer": "Kuscheln, zungen piercing",
            "id": 56,
            "question": "Current obsession"
        }
    ],
    "available": true,
    "distance": 13,
    "feed_post_count": 0,
    "friend_count": 2,
    "friendship_status": "none",
    "future_event_count": 0,
    "height": 76.77165,
    "id": 9433981,
    }
    ... snip ... 
```

### Other ways of getting user profiles

From what we saw app mostly works by passing lists of user profiles. Getting my profile, profiles in radius and direct profile access return the same profile format. As implied further inspection of API showed that this is the case most of the time. In this section, we will show some more examples. Responses will be omitted since they are in the same format.



#### Who liked me

The dating app includes a premium feature in which you can see who liked your profile. If a premium subscription is not bought, the user can see only blurred photos but these photos are blurred on the client-side. A call to `/profiles_liked_me` returns a list of *all* user profiles that have liked our profile. By inspecting communication or by patching the app one can get this information without subscribing to premium.


`GET https://api.weareher.com/v4/profiles_liked_me?offset=0 HTTP/2.0`

#### Profiles online

While using the app user can see if other users are online. By calling `profiles_online` one can get a list of online user profiles. We were not able to determine on what criteria these user profiles were selected. The list at the time was around 8 kb, which is too much for matches and by number looks closer to a number of online users in a certain radius. 



`GET https://api.weareher.com/v4/profiles_online?offset=0&limit=10 HTTP/2.0`

## Tracking 

Her dating app employs multiple user tracking methods. The device hardware is sent to app backend servers and to ad providers.


### App usage tracking

When a user opens an app view this information is being sent to Her tracking API. In some cases, viewing time of a specific app view is also sent.

`POST https://api.weareher.com/v4/track HTTP/2.0`

Query when new view is opened.
```=json
{
    "name": "open-login"
}
```
With viewing time.
```=json
{
    "additional": {
        "time": 34
    },
    "name": "exit-meet"
}
```

### Commercial tracking

Her dating app is using Braze for external data collection and processing. Braze collects a lot of device data such as: Phone model, Android version, screen size, screen DPI etc. More concerning data points are: phone hardware ID, identity ID, real hardware ID, WiFi usage and internal private IP address of the phone.

During app research, we have run into a problem when our device was banned because of "suspicious activity". New accounts would terminate in the middle of the registration process (during the pre-user stage). An educated guess would be that our hardware ID was banned.

In our personal opinion tracking internal private IP and WiFi usage is too much. It reveals the internal structure of someone's private network which "should" not be a security issue but it is unneeded.

In the next section, there are two of the most common tracking API calls.

`POST https://sdk.iad-01.braze.com/api/v3/data HTTP/1.1`
```=json
{
    "api_key": "1b6116a1-126a-4c57-9483-0109adb7e23d",
    "app_version": "3.13.6",
    "app_version_code": "694.0.0.0",
    "attributes": [
        {
            "push_token": "fEsilxgERtCvMsBmAl-3cS:APA91bEtXiFvjYPfKGxChkKfyG4MqArTxfFCveCq6YK1X033lL82_8H2Q1W693hfpAcz55EbF1X6zQ_7zJvZGKoLF_8cOxdrbAODjMAHdlg5wXcE0Deh3tP7H1XWvICp5ES8JLmmTcxu"
        }
    ],
    "device": {
        "ad_tracking_enabled": true,
        "android_is_background_restricted": false,
        "google_ad_id": "6ce480fe-376e-4fc4-9cc9-fc3ed16edde2",
        "locale": "en_GB",
        "model": "HUAWEI VNS-L21",
        "os_version": "24",
        "remote_notification_enabled": true,
        "resolution": "1080x1812",
        "time_zone": "Europe/Vienna"
    },
    "device_id": "288d96b7-0d4d-4ad3-af68-0ec7efad001b",
    "events": [
        {
            "data": {},
            "name": "ss",
            "session_id": "d7d4d735-9d50-492d-9555-42cdfcde0603",
            "time": 1654525620.981
        }
    ],
    "respond_with": {
        "config": {
            "config_time": 1652381375
        },
        "triggers": true
    },
    "sdk_version": "15.0.0",
    "time": 1654525621
}
```

`POST https://api2.branch.io/v1/open HTTP/1.1`

```=json
{
    "advertising_ids": {
        "aaid": "6ce480fe-376e-4fc4-9cc9-fc3ed16edde2"
    },
    "app_version": "3.13.6",
    "branch_key": "key_live_bdnGY11GPAUIkCEibh6z1adlCzbm09Vf",
    "brand": "HUAWEI",
    "build": "VNS-L21C432B506",
    "connection_type": "wifi",
    "country": "GB",
    "cpu_type": "aarch64",
    "debug": false,
    "device_fingerprint_id": "1062360689068353309",
    "environment": "FULL_APP",
    "facebook_app_link_checked": false,
    "first_install_time": 1654477874489,
    "google_advertising_id": "6ce480fe-376e-4fc4-9cc9-fc3ed16edde2",
    "hardware_id": "dcb1a83c78115124",
    "identity_id": "1062460432424437176",
    "instrumentation": {
        "v1/open-qwt": "0"
    },
    "is_hardware_id_real": true,
    "is_referrable": 0,
    "language": "en",
    "lat_val": 0,
    "latest_install_time": 1654477874489,
    "latest_update_time": 1654477874489,
    "local_ip": "192.168.88.86",
    "locale": "en_GB",
    "metadata": {},
    "model": "HUAWEI VNS-L21",
    "os": "Android",
    "os_version": 24,
    "os_version_android": "7.0",
    "previous_update_time": 1654477874489,
    "retryNumber": 0,
    "screen_dpi": 480,
    "screen_height": 1812,
    "screen_width": 1080,
    "sdk": "android5.0.3",
    "ui_mode": "UI_MODE_TYPE_NORMAL",
    "update": 1,
    "wifi": true
}
```

## Conclusion

*Her* showed to be one of the most vulnarable apps that we tested. Sending a batch of all profiles in a certain radius presents an unacceptable risk to personal infromation. Sending smaller batches of 10 to 20 profiles, like many other apps are practising, with no way for an attacker to know how these profiles were chosen, would drastically improve privacy of app users.
Sending distance between users is a hard to get right. More tests would need to be done to determine how exploitable is this information. But from what we have seen mass survailance of users in a region could be possible.
In general *Her* is riddled with bad programming practices and would need a major overhaul to protect its users private infromation.


### Future work
In the future more work should be done in automated processing of available data and testing if, with a help of GPS spoofing, mass location leakega is possible.
