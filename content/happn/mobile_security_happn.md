---
title: "Mobile Security: Happn report"
url: /happn/"
summary: Analysis of Happn
tags:
    - Mobile Security
    - Assignment 2
    - Happn
---

## Description

Happn is a Paris-based dating app and has been around since 2014. Happn helps you connect with people you have crossed paths with in real life. 

Source : https://www.eu-startups.com/2022/02/10-european-startups-helping-you-find-love/

**Device used:** Android emulator Pixel 4 Android 10 API level 29, Platform x86

## Structure of the report

1. Registration process
2. Log in process
3. Public profile structure
4. Obtaining other users data
5. Other ways of obtaining user data
6. Tracking
7. Conclusion
8. Future work


### Registration process


### Log in process

Log in procedure is ferly simple. Every request, including the initial(log-in) includes an authorisation token.

```
authorization: OAuth="eyJhbGciOiJIUzI1NiJ9.eyJzY29wZSI6WyJ1c2VyX2RlbGV0ZSIsInVzZXJfcmVwb3J0X3JlYWQiLCJ1c2VyX3RyYWl0X2Fuc3dlcl93cml0ZSIsInVzZXJfdXBkYXRlIiwiYm9vc3RfY3JlYXRlIiwiYm9vc3RfcmVhZCIsInVzZXJfc29jaWFsX2RlbGV0ZSIsInVzZXJfY29udmVyc2F0aW9uX3JlYWQiLCJ1c2VyX2FjY2VwdGVkX3JlYWQiLCJ1c2VyX2NvbnZlcnNhdGlvbl9jcmVhdGUiLCJhbGxfdXNlcl90cmFpdF9hbnN3ZXJfcmVhZCIsInVzZXJfcmVqZWN0ZWRfY3JlYXRlIiwidXNlcl9ibG9ja2VkX3JlYWQiLCJzaG9ydGxpc3RfcmVhZCIsInVzZXJfcmVwb3J0X3VwZGF0ZSIsInVzZXJfYWNoaWV2ZW1lbnRfcmVhZCIsInVzZXJfYWNoaWV2ZW1lbnRfZGVsZXRlIiwidXNlcl9yZXBvcnRfZGVsZXRlIiwidXNlcl9hdWRpb2NhbGxfY3JlYXRlIiwidXNlcl9hY2hpZXZlbWVudF91cGRhdGUiLCJ1c2VyX3ZpZGVvY2FsbF91cGRhdGUiLCJ1c2VyX2FwcGxpY2F0aW9uc19yZWFkIiwidXNlcl9ibG9ja2VkX2RlbGV0ZSIsInVzZXJfc3Vic2NyaXB0aW9uX2NyZWF0ZSIsInBhY2tfcmVhZCIsInVzZXJfb3JkZXJfdXBkYXRlIiwidXNlcl9yZWFkIiwibm90aWZpY2F0aW9uX3R5cGVfcmVhZCIsInVzZXJfYWNoaWV2ZW1lbnRfY3JlYXRlIiwidXNlcl9tZXNzYWdlX3JlYWQiLCJ1c2VyX2ltYWdlX2NyZWF0ZSIsInVzZXJfY29udmVyc2F0aW9uX2RlbGV0ZSIsInVzZXJfc29jaWFsX3VwZGF0ZSIsInVzZXJfZGV2aWNlX2RlbGV0ZSIsInVzZXJfYWNjZXB0ZWRfY3JlYXRlIiwic3Vic2NyaXB0aW9uX3R5cGVfcmVhZCIsInVzZXJfcG9rZV9jcmVhdGUiLCJ0cmFpdF9yZWFkIiwidXNlcl9hcHBsaWNhdGlvbnNfdXBkYXRlIiwidXNlcl9yZXBvcnRfY3JlYXRlIiwidXNlcl9vcmRlcl9jcmVhdGUiLCJ1c2VyX2RldmljZV91cGRhdGUiLCJ1c2VyX3Nob3BfcmVhZCIsImFyY2hpdmVfY3JlYXRlIiwidXNlcl9yZWplY3RlZF9yZWFkIiwidXNlcl9hcHBsaWNhdGlvbnNfZGVsZXRlIiwidXNlcl9zdWJzY3JpcHRpb25fZGVsZXRlIiwidXNlcl9hdWRpb2NhbGxfcmVhZCIsInVzZXJfc3Vic2NyaXB0aW9uX3JlYWQiLCJ1c2VyX3ZpZGVvY2FsbF9yZWFkIiwidXNlcl9ibG9ja2VkX2NyZWF0ZSIsInVzZXJfc3Vic2NyaXB0aW9uX3VwZGF0ZSIsInVzZXJfbWVzc2FnZV9jcmVhdGUiLCJ1c2VyX21lc3NhZ2VfZGVsZXRlIiwidXNlcl9tb2RlX3JlYWQiLCJ1c2VyX3NvY2lhbF9jcmVhdGUiLCJ1c2VyX2ltYWdlX3VwZGF0ZSIsImxvY2FsZV9yZWFkIiwidXNlcl9ub3RpZmljYXRpb25zX3JlYWQiLCJhY2hpZXZlbWVudF90eXBlX3JlYWQiLCJzZWFyY2hfdXNlciIsInVzZXJfaW1hZ2VfZGVsZXRlIiwidXNlcl9kZXZpY2VfcmVhZCIsImFsbF91c2VyX3JlYWQiLCJ1c2VyX3NvY2lhbF9yZWFkIiwiYXJjaGl2ZV9yZWFkIiwidXNlcl9kZXZpY2VfY3JlYXRlIiwidXNlcl9wb3NpdGlvbl9yZWFkIiwicGF5bWVudF9wb3J0YWxfcmVhZCIsInVzZXJfYWNjZXB0ZWRfZGVsZXRlIiwidXNlcl9tZXNzYWdlX3VwZGF0ZSIsInVzZXJfYXVkaW9jYWxsX3VwZGF0ZSIsInVzZXJfb3JkZXJfcmVhZCIsInVzZXJfdmlkZW9jYWxsX2NyZWF0ZSIsImxhbmd1YWdlX3JlYWQiLCJhbGxfaW1hZ2VfcmVhZCIsInVzZXJfY29udmVyc2F0aW9uX3VwZGF0ZSIsInVzZXJfaW1hZ2VfcmVhZCIsImNoZWNrb3V0X2NyZWF0ZSIsInVzZXJfcmVqZWN0ZWRfZGVsZXRlIiwicmVwb3J0X3R5cGVfcmVhZCIsInVzZXJfcG9zaXRpb25fdXBkYXRlIl0sImp0aSI6ImRlZGNlMzZkLTliOWQtNDEzOS04YmIyLTZjZDE2ZGU0ZDc3OSIsInN1YiI6IjhiY2QzNzFjLWIwOWYtNGFlNi05MWI0LTczNmEzYTcyNDU5ZCIsImF1ZCI6IkZVRS1pZFNFUC1mN0FxQ3l1TWNQcjJLLTFpQ0lVX1lsdkstTS1pbTNjIiwiZXhwIjoxNjU0Njg0ODcxLCJpYXQiOjE2NTQ1OTg0NzF9.SbhjSxIzjfZknKYEGC9XMKrfwyw01bYvP4kfQoqTfNM"
```

When users first log in into *Happn*, an API call is made to populate all fields in their profile. Answers to personal questions, like cooking preferences and smoking, which are usually not sent with the basic profile in other profiles, are also included.

`GET https://api.happn.fr/api/users/8bcd371c-b09f-4ae6-91b4-736a3a72459d`

```
fields: id,first_name,gender,age,referal,login,workplace,job,profiles.mode(0).width(220).height(220).fields(id,is_default,mode,url,width,height,is_default),unread_conversations,unread_notifications.types(471,524,525,526,529,530,531,565,791,792),register_date,social_synchronization.fields(instagram),is_premium,user_balance,mysterious_mode_preferences.fields(hide_age, hide_distance, hide_location, hide_last_activity_date),location_preferences.fields(hide_location),traits,residence_city,audios,proximity_id,matching_preferences.fields(matching_traits.fields(enabled))
```

Response:
```=json
{
    "data": {
        "age": 25,
        "audios": [],
        "birth_date": "1997-04-19",
        "first_name": "Janez",
        "gender": "male",
        "id": "8bcd371c-b09f-4ae6-91b4-736a3a72459d",
        "is_premium": false,
        "job": null,
        "location_preferences": {
            "hide_location": false
        },
        "login": null,
        "matching_preferences": {
            "age_max": 40,
            "age_min": 18,
            "distance": 0,
            "female": 1,
            "male": 0,
            "matching_traits": {
                "enabled": false
            }
        },
        "mysterious_mode_preferences": {
            "hide_age": false,
            "hide_distance": false,
            "hide_last_activity_date": false
        },
        "nb_photos": 1,
        "profiles": [
            {
                "height": 320,
                "id": "52e54190-e275-11ec-b746-19d23e968232",
                "is_default": false,
                "mode": 0,
                "url": "https://images.happn.fr/resizing/8bcd371c-b09f-4ae6-91b4-736a3a72459d/52e54190-e275-11ec-b746-19d23e968232.jpg?width=320&height=320&mode=0",
                "width": 320
            }
        ],
        "proximity_id": null,
        "referal": {
            "sponsor_link": {
                "code": "ah2WY92N1Ui",
                "creation_date": "2022-06-08T10:11:20+00:00",
                "destination": "https://happn.com/r/ah2WY92N1Ui",
                "id": "86f7ae229a3fbb2f96d219cbde0efa4f",
                "redirect_url": "https://happn.com/r/ah2WY92N1Ui",
                "status": 1
            },
            "texts": {
                "crush_share_text_facebook": "I've just had my Crush #{CRUSH_N} on happn :D",
                "crush_share_text_mail": "I've just had my Crush #{CRUSH_N} on happn :D",
                "crush_share_text_texto": "I've just had my Crush #{CRUSH_N} on happn :D",
                "crush_share_text_twitter": "I've just had my Crush #{CRUSH_N} on @happn_app :D",
                "sponsor_share_text_facebook": "Check out happn, the app that helps you find the people you’ve crossed paths with {LINK}",
                "sponsor_share_text_mail": "Hey, try out happn, you'll be able to find all the people you’ve crossed paths with, it's amazing {LINK}",
                "sponsor_share_text_texto": "Try out happn, it’s amazing {LINK}",
                "sponsor_share_text_twitter": "Check out @happn_app, the app that helps you find the people you’ve crossed paths with {LINK}"
            }
        },
        "register_date": "2022-06-02T12:48:18+00:00",
        "residence_city": {
            "city": "San Jose",
            "country": "United States",
            "county": "California",
            "id": "place.9685595429165690",
            "modification_date": "2022-06-02T13:14:08",
            "position": {
                "latitude": 37.33619,
                "longitude": -121.89058
            }
        },
        "role": "CLIENT",
        "social_synchronization": null,
        "traits": [
            {
                "answer": {
                    "single": {
                        "default_label": "I’ll know when I find it",
                        "id": "5efb1e20-772d-11e9-9403-ab4bdd6fe9b1",
                        "label_localized": [
                            {
                                "tags": [],
                                "value": "I’ll know when I find it"
                            }
                        ]
                    },
                    "type": "SINGLE"
                },
                "default_emoji": "🔎",
                "default_label": "What are you looking for on happn?",
                "default_short_label": "Looking for",
                "emoji_localized": [
                    {
                        "tags": [],
                        "value": "🔎"
                    }
                ],
                "id": "73210140-772c-11e9-9403-ab4bdd6fe9b1",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "What are you looking for on happn?"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Looking for"
                    }
                ]
            },
            {
                "answer": {
                    "float_range": {
                        "metric": "length",
                        "value": 1.87
                    },
                    "type": "FLOAT_RANGE"
                },
                "default_emoji": "😊",
                "default_label": "How tall are you?",
                "default_short_label": "Height",
                "emoji_localized": [
                    {
                        "tags": [
                            "MALE_ME"
                        ],
                        "value": "👨"
                    }
                ],
                "id": "a23938b0-77f6-11e9-b0dc-35a91441a495",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "How tall are you?"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Height"
                    }
                ]
            },
            {
                "answer": {
                    "single": {
                        "default_label": "Occasional exercise",
                        "id": "27afc720-77e8-11e9-b4c2-c3a9c0a73afd",
                        "label_localized": [
                            {
                                "tags": [
                                    "MALE_ME"
                                ],
                                "value": "Occasional exercise"
                            }
                        ]
                    },
                    "type": "SINGLE"
                },
                "default_emoji": "💪",
                "default_label": "What are your exercise habits?",
                "default_short_label": "Exercise",
                "emoji_localized": [
                    {
                        "tags": [],
                        "value": "💪"
                    }
                ],
                "id": "bae69d90-77e6-11e9-b4c2-c3a9c0a73afd",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "What are your exercise habits?"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Exercise"
                    }
                ]
            },
            {
                "answer": {
                    "single": {
                        "default_label": "I’m a microwave master",
                        "id": "090f5350-77eb-11e9-b4c2-c3a9c0a73afd",
                        "label_localized": [
                            {
                                "tags": [],
                                "value": "I’m a microwave master"
                            }
                        ]
                    },
                    "type": "SINGLE"
                },
                "default_emoji": "🍴",
                "default_label": "Which answer best describes your cooking skills?",
                "default_short_label": "Cooking",
                "emoji_localized": [
                    {
                        "tags": [
                            "MALE_ME"
                        ],
                        "value": "👨‍🍳"
                    }
                ],
                "id": "d61867c0-77f4-11e9-b43e-ed07d0af7b4d",
                "label_localized": [
                    {
                        "tags": [
                            "MALE_ME"
                        ],
                        "value": "Which answer best describes your cooking skills?"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Cooking"
                    }
                ]
            },
            {
                "answer": {
                    "single": {
                        "default_label": "Deckchair & sunscreen",
                        "id": "b5e0a890-77eb-11e9-b4c2-c3a9c0a73afd",
                        "label_localized": [
                            {
                                "tags": [],
                                "value": "Deckchair & sunscreen"
                            }
                        ]
                    },
                    "type": "SINGLE"
                },
                "default_emoji": "✈",
                "default_label": "What two words best describe your ideal vacation?",
                "default_short_label": "Travel",
                "emoji_localized": [
                    {
                        "tags": [],
                        "value": "✈️"
                    }
                ],
                "id": "98aac8a0-77eb-11e9-b4c2-c3a9c0a73afd",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "What two words best describe your ideal vacation?"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Travel"
                    }
                ]
            },
            {
                "answer": {
                    "single": {
                        "default_label": "I’m a night owl",
                        "id": "47948430-91e3-11e9-86f7-9119d852bbdd",
                        "label_localized": [
                            {
                                "tags": [],
                                "value": "I’m a night owl"
                            }
                        ]
                    },
                    "type": "SINGLE"
                },
                "default_emoji": "🎉",
                "default_label": "When it comes to the nightlife…",
                "default_short_label": "Partying",
                "emoji_localized": [
                    {
                        "tags": [],
                        "value": "🎉"
                    }
                ],
                "id": "f5ce5f90-91e2-11e9-86f7-9119d852bbdd",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "When it comes to the nightlife…"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Partying"
                    }
                ]
            },
            {
                "answer": {
                    "single": {
                        "default_label": "Not a fan, but whatever",
                        "id": "e03db520-7ef1-11ea-9cbc-072a91dcea22",
                        "label_localized": [
                            {
                                "tags": [],
                                "value": "Not a fan, but whatever"
                            }
                        ]
                    },
                    "type": "SINGLE"
                },
                "default_emoji": "🚬",
                "default_label": "Your opinion on smoking?",
                "default_short_label": "Smoking",
                "emoji_localized": [
                    {
                        "tags": [],
                        "value": "🚬"
                    }
                ],
                "id": "79c98710-7ef1-11ea-9cbc-072a91dcea22",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "Your opinion on smoking?"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Smoking"
                    }
                ]
            },
            {
                "answer": {
                    "single": {
                        "default_label": "Thanks, but no thanks",
                        "id": "3edb7e30-7ef9-11ea-9cbc-072a91dcea22",
                        "label_localized": [
                            {
                                "tags": [],
                                "value": "Thanks, but no thanks"
                            }
                        ]
                    },
                    "type": "SINGLE"
                },
                "default_emoji": "👶",
                "default_label": "What about kids?",
                "default_short_label": "Kids",
                "emoji_localized": [
                    {
                        "tags": [],
                        "value": "👶"
                    }
                ],
                "id": "31454f40-7ef3-11ea-9cbc-072a91dcea22",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "What about kids?"
                    }
                ],
                "sensitive_trait": false,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Kids"
                    }
                ]
            },
            {
                "default_emoji": "🍽",
                "default_label": "What are your eating habits?",
                "default_short_label": "Eating habits",
                "emoji_localized": [
                    {
                        "tags": [],
                        "value": "🍽"
                    }
                ],
                "id": "e8c129da-6f12-11ec-90d6-0242ac120003",
                "label_localized": [
                    {
                        "tags": [],
                        "value": "What are your eating habits?"
                    }
                ],
                "sensitive_trait": true,
                "short_label_localized": [
                    {
                        "tags": [],
                        "value": "Eating habits"
                    }
                ]
            }
        ],
        "type": "client",
        "unread_conversations": 2,
        "unread_notifications": 0,
        "user_balance": [
            {
                "cooldown_period": null,
                "cooldown_time_left": null,
                "permanent": 3,
                "renewable": 0,
                "renewable_per_period": 0,
                "total": 3,
                "type": "credit"
            },
            {
                "cooldown_period": null,
                "cooldown_time_left": null,
                "permanent": 0,
                "renewable": 0,
                "renewable_per_period": 0,
                "total": 0,
                "type": "video"
            },
            {
                "cooldown_period": 43200,
                "cooldown_time_left": 10675,
                "permanent": 0,
                "renewable": 28,
                "renewable_per_period": 30,
                "total": 28,
                "type": "like"
            },
            {
                "cooldown_period": null,
                "cooldown_time_left": null,
                "permanent": 0,
                "renewable": 0,
                "renewable_per_period": 0,
                "total": 0,
                "type": "boost"
            }
        ],
        "workplace": null
    },
    "error": null,
    "error_code": 0,
    "status": 200,
    "success": true
}
```

### Public profile structure

A basic user profile in JSON looks like this. `id` might help us to track user through direct API calls. `has_charmed_me` is used to note if someone has swipe/liked our profile. Having access to `has_charmed_me` gives us an unfair advantage and bypasses a premium/pay-only feature. Access to user `modification_data` can give us how active is a certain user. `distance` could enable us to track other users.

Happn had a scandal where location of other users could be tracked so it is possible that distance is capped at `9999` or that this field is a legacy leftover set to `9999`.

```=json
"user": {
    "about": "",
    "age": 30,
    "audios": [],
    "distance": 9999,
    "first_name": "Jones Ann",
    "gender": "female",
    "has_charmed_me": false,
    "id": "bedf3f9e-155a-4332-b035-dca40cbbbd61",
    "is_charmed": false,
    "modification_date": "2022-05-30T05:43:05",
    "my_relations": {},
    "nb_photos": 6
    }
```

### Obtaining other users data

When entering the app to start swiping for new matches, information about other users needs to be obtained by the app. App sends an API call to get the next 18 users to show. In `fields` app specifies what information about users should be fetched.


```
GET https://api.happn.fr/api/v1/users/8bcd371c-b09f-4ae6-91b4-736a3a72459d/recommendations
```

Query:
```
scroll_id_from: eyJPUFBPUlRVTklUWSI6IjMwYTUzMTEwLWU3MTMtMTFlYy1iMzY4LWFiMTg4ODZiYmEzMDoxMSIsIkNST1NTSU5HIjoiNzEwNjgwOTQzNDI5MzI0ODcwNyIsIkJPT1NURUQiOm51bGwsIk5FV19SRUciOiIzMGJjZmVkMC1lNzEzLTExZWMtYjM2OC1hYjE4ODg2YmJhMzA6NCJ9
limit:          18
fields:         type,content.fields(user.fields(id,type,job,school,workplace,about,my_relations,distance,modification_date,gender,is_charmed,nb_photos,first_name,age,has_charmed_me,profiles.mode(1).width(1080).height(1977).fields(id,mode,url,width,height),traits,spotify_tracks,verification.fields(status),social_synchronization.fields(instagram),clickable_profile_link,is_moderator,residence_city,audios),position.fields(lat,lon),last_meet_date,crossing_nb_times)
```

Response:
```=json
{
    "data": [
        {
            "content": {
                "position": {
                    "lat": 37.412243,
                    "lon": -121.94107
                },
                "user": {
                    "about": "",
                    "age": 30,
                    "audios": [],
                    "distance": 9999,
                    "first_name": "Jones Ann",
                    "gender": "female",
                    "has_charmed_me": false,
                    "id": "bedf3f9e-155a-4332-b035-dca40cbbbd61",
                    "is_charmed": false,
                    "modification_date": "2022-05-30T05:43:05",
                    "my_relations": {},
                    "nb_photos": 6,
                    "profiles": [
                        {
                            "height": 853,
                            "id": "1b652c90-dfdb-11ec-a2ed-d716fb20c509",
                            "mode": 1,
                            "url": "https://images.happn.fr/resizing/bedf3f9e-155a-4332-b035-dca40cbbbd61/1b652c90-dfdb-11ec-a2ed-d716fb20c509.jpg?width=640&height=1136&mode=1",
                            "width": 640
                        },
                        {
                            "height": 853,
                            "id": "1cc90250-dfdb-11ec-a2ed-d716fb20c509",
                            "mode": 1,
                            "url": "https://images.happn.fr/resizing/bedf3f9e-155a-4332-b035-dca40cbbbd61/1cc90250-dfdb-11ec-a2ed-d716fb20c509.jpg?width=640&height=1136&mode=1",
                            "width": 640
                        },
                        {
                            "height": 853,
                            "id": "1e183ea0-dfdb-11ec-b746-19d23e968232",
                            "mode": 1,
                            "url": "https://images.happn.fr/resizing/bedf3f9e-155a-4332-b035-dca40cbbbd61/1e183ea0-dfdb-11ec-b746-19d23e968232.jpg?width=640&height=1136&mode=1",
                            "width": 640
                        },
                        {
                            "height": 853,
                            "id": "1fa71c00-dfdb-11ec-bb6f-7ff10cdfa7cf",
                            "mode": 1,
                            "url": "https://images.happn.fr/resizing/bedf3f9e-155a-4332-b035-dca40cbbbd61/1fa71c00-dfdb-11ec-bb6f-7ff10cdfa7cf.jpg?width=640&height=1136&mode=1",
                            "width": 640
                        },
                        {
                            "height": 854,
                            "id": "2130a230-dfdb-11ec-a2ed-d716fb20c509",
                            "mode": 1,
                            "url": "https://images.happn.fr/resizing/bedf3f9e-155a-4332-b035-dca40cbbbd61/2130a230-dfdb-11ec-a2ed-d716fb20c509.jpg?width=640&height=1136&mode=1",
                            "width": 640
                        },
                        {
                            "height": 853,
                            "id": "22b657d0-dfdb-11ec-bb6f-7ff10cdfa7cf",
                            "mode": 1,
                            "url": "https://images.happn.fr/resizing/bedf3f9e-155a-4332-b035-dca40cbbbd61/22b657d0-dfdb-11ec-bb6f-7ff10cdfa7cf.jpg?width=640&height=1136&mode=1",
                            "width": 640
                        }
                    ],
                    "traits": [
                        {
                            "answer": {
                                "single": {
                                    "default_label": "A relationship",
                                    "id": "1c90dc00-772d-11e9-9403-ab4bdd6fe9b1",
                                    "label_localized": [
                                        {
                                            "tags": [],
                                            "value": "A relationship"
                                        }
                                    ]
                                },
                                "trait_id": "73210140-772c-11e9-9403-ab4bdd6fe9b1",
                                "type": "SINGLE"
                            },
                            "default_emoji": "🔎",
                            "default_label": "What are you looking for on happn?",
                            "default_short_label": "Looking for",
                            "emoji_localized": [
                                {
                                    "tags": [],
                                    "value": "🔎"
                                }
                            ],
                            "id": "73210140-772c-11e9-9403-ab4bdd6fe9b1",
                            "label_localized": [
                                {
                                    "tags": [],
                                    "value": "What are you looking for on happn?"
                                }
                            ],
                            "sensitive_trait": false,
                            "short_label_localized": [
                                {
                                    "tags": [],
                                    "value": "Looking for"
                                }
                            ]
                        },
                        {
                            "answer": {
                                "float_range": {
                                    "metric": "length",
                                    "value": 1.69
                                },
                                "trait_id": "a23938b0-77f6-11e9-b0dc-35a91441a495",
                                "type": "FLOAT_RANGE"
                            },
                            "default_emoji": "😊",
                            "default_label": "How tall are you?",
                            "default_short_label": "Height",
                            "emoji_localized": [
                                {
                                    "tags": [
                                        "FEMALE_ME"
                                    ],
                                    "value": "👩"
                                }
                            ],
                            "id": "a23938b0-77f6-11e9-b0dc-35a91441a495",
                            "label_localized": [
                                {
                                    "tags": [],
                                    "value": "How tall are you?"
                                }
                            ],
                            "sensitive_trait": false,
                            "short_label_localized": [
                                {
                                    "tags": [],
                                    "value": "Height"
                                }
                            ]
                        },
                        {
                            "answer": {
                                "single": {
                                    "default_label": "All exercise all the time",
                                    "id": "45f1e5a0-7956-11e9-8eb2-d3c69ddd8234",
                                    "label_localized": [
                                        {
                                            "tags": [
                                                "FEMALE_ME"
                                            ],
                                            "value": "All exercise all the time"
                                        }
                                    ]
                                },
                                "trait_id": "bae69d90-77e6-11e9-b4c2-c3a9c0a73afd",
                                "type": "SINGLE"
                            },
                            "default_emoji": "💪",
                            "default_label": "What are your exercise habits?",
                            "default_short_label": "Exercise",
                            "emoji_localized": [
                                {
                                    "tags": [],
                                    "value": "💪"
                                }
                            ],
                            "id": "bae69d90-77e6-11e9-b4c2-c3a9c0a73afd",
                            "label_localized": [
                                {
                                    "tags": [],
                                    "value": "What are your exercise habits?"
                                }
                            ],
                            "sensitive_trait": false,
                            "short_label_localized": [
                                {
                                    "tags": [],
                                    "value": "Exercise"
                                }
                            ]
                        },
                        {
                            "answer": {
                                "single": {
                                    "default_label": "Deckchair & sunscreen",
                                    "id": "b5e0a890-77eb-11e9-b4c2-c3a9c0a73afd",
                                    "label_localized": [
                                        {
                                            "tags": [],
                                            "value": "Deckchair & sunscreen"
                                        }
                                    ]
                                },
                                "trait_id": "98aac8a0-77eb-11e9-b4c2-c3a9c0a73afd",
                                "type": "SINGLE"
                            },
                            "default_emoji": "✈",
                            "default_label": "What two words best describe your ideal vacation?",
                            "default_short_label": "Travel",
                            "emoji_localized": [
                                {
                                    "tags": [],
                                    "value": "✈️"
                                }
                            ],
                            "id": "98aac8a0-77eb-11e9-b4c2-c3a9c0a73afd",
                            "label_localized": [
                                {
                                    "tags": [],
                                    "value": "What two words best describe your ideal vacation?"
                                }
                            ],
                            "sensitive_trait": false,
                            "short_label_localized": [
                                {
                                    "tags": [],
                                    "value": "Travel"
                                }
                            ]
                        }
                    ],
                    "type": "client",
                    "verification": {
                        "status": "unverified"
                    }
                }
            },
            "type": 3
        },
        
        ... snip ...snip
```
### Other ways of obtaining user data

Happn provides two other ways to see other users' profiles. A special trademark feature of Happn is to recommend Happn users with which you have "crossed" paths. This is done by sending a geobox by coordinated to the API and in return, the app receives users that share the same general location. Some of this data might be used to track when a certain user leaves a certain location.

Further dynamics of this were hard to test since there is not many Happn users in Graz area.


`GET https://api.happn.fr/api/users/8bcd371c-b09f-4ae6-91b4-736a3a72459d/maps`

Query:
```
top_left_lat:     37.42882743829329
top_left_lon:     -121.95238083601
bottom_right_lat: 37.39565572166751
bottom_right_lon: -121.92976143211128
clusters_types:   crossings
fields:           geo_bounding_box,clusters.fields(id,size,crossings.fields(notifier.fields(id,profiles.mode(1).width(154).height(154).fields(id,mode,url,width,height).limit(1))),position)
```

Response:

```=json
{
    "data": [
        {
            "clusters": [
                {
                    "crossings": [
                        {
                            "id": "8bcd371c-b09f-4ae6-91b4-736a3a72459d_d0d7dc6a-1eee-4eb3-84cf-a0377eb8d8fa",
                            "notifier": {
                                "id": "d0d7dc6a-1eee-4eb3-84cf-a0377eb8d8fa",
                                "nb_photos": 1,
                                "profiles": [
                                    {
                                        "height": 475,
                                        "id": "23632780-b637-11ec-9bf6-f95662717f2d",
                                        "mode": 1,
                                        "url": "https://images.happn.fr/resizing/d0d7dc6a-1eee-4eb3-84cf-a0377eb8d8fa/23632780-b637-11ec-9bf6-f95662717f2d.jpg?width=320&height=480&mode=1",
                                        "width": 320
                                    }
                                ],
                                "role": "CLIENT",
                                "type": "client"
                            }
                        },
                        {
                            "id": "8bcd371c-b09f-4ae6-91b4-736a3a72459d_cc9ceb96-3070-4a6a-bb22-4caa14092917",
                            "notifier": {
                                "id": "cc9ceb96-3070-4a6a-bb22-4caa14092917",
                                "nb_photos": 1,
                                "profiles": [
                                    {
                                        "height": 476,
                                        "id": "7ef5d210-e6d3-11ec-ad09-7fd7ee1025cf",
                                        "mode": 1,
                                        "url": "https://images.happn.fr/resizing/cc9ceb96-3070-4a6a-bb22-4caa14092917/7ef5d210-e6d3-11ec-ad09-7fd7ee1025cf.jpg?width=320&height=480&mode=1",
                                        "width": 320
                                    }
                                ],
                                "role": "CLIENT",
                                "type": "client"
                            }
                        }
                    ],
                    "id": "OXE5a2M0LDhiY2QzNzFjLWIwOWYtNGFlNi05MWI0LTczNmEzYTcyNDU5ZCxjcm9zc2luZw==",
                    "position": {
                        "lat": 37.412242842838,
                        "lon": -121.94107063115
                    },
                    "size": 2
                }
            ],
            "geo_bounding_box": {
                "bottom_right": {
                    "lat": 37.369995117188,
                    "lon": -121.904296875
                },
                "top_left": {
                    "lat": 37.452392578125,
                    "lon": -121.97021484375
                }
            },
            "id": "NWRjZDY3MjAtZTcxMy0xMWVjLWIxMDQtYWQzYWM2YzFkMTZj"
        }
    ],
    "error": null,
    "error_code": 0,
    "status": 200,
    "success": true
}
```

### Tracking

Her dating app employs multiple user tracking methods. The device hardware is sent to app backend servers and to ad providers.


#### App usage tracking

When the user opens an app view this information is being sent to Happn tracking API. In some cases viewing time of a specific app view is also sent.


`POST https://a.happn.com/v1/bulk HTTP/2.0`

Query:
```=json
{
  "attributes": {
    "device": {
      "country": "US",
      "os": "android",
      "push_enabled": true,
      "language": "en",
      "id": "56476934-d09b-465e-977d-9f72f25bc77f",
      "source": null,
      "type": "mobile",
      "platform": "android_app",
      "mobile_token": null
    },
    "event": {
      "app_version": "26.13.0",
      "name": "a.open.app",
      "id": "2e270c19-8e61-49dd-9768-08112c57468a"
    },
    "session": {
      "duration": 0,
      "connection": null,
      "id": "07d6e827-3d13-432d-9837-66312341ffa1",
      "source": "springboard"
    },
    "user": {
      "gender": null,
      "register_date": null,
      "id": null,
      "first_name": null,
      "age": null
    }
  },
  "category": "click_stream",
  "created_ts": "2022-06-02T14:46:31.526+0200",
  "service": "mobile",
  "v": 0
}\xff{
  "attributes": {
    "device": {
      "country": "US",
      "os": "android",
      "push_enabled": true,
      "language": "en",
      "id": "56476934-d09b-465e-977d-9f72f25bc77f",
      "source": null,
      "type": "mobile",
      "platform": "android_app",
      "mobile_token": null
    },
    "event": {
      "app_version": "26.13.0",
      "name": "a.install.app",
      "id": "1e67e06e-c86b-4a28-8645-6d53c839ae97"
    },
    "session": {
      "duration": 0,
      "connection": null,
      "id": "07d6e827-3d13-432d-9837-66312341ffa1",
      "source": "springboard"
    },
    "user": {
      "gender": null,
      "register_date": null,
      "id": null,
      "first_name": null,
      "age": null
    }
  },
  "category": "click_stream",
  "created_ts": "2022-06-02T14:46:31.582+0200",
  "service": "mobile",
  "v": 0
}
```

#### Commercial tracking 

Happn is using Braze under the name of *appboy.eu* and *adjust.net.in* for external data collection and processing. 



#### appboy eu

`POST https://hapselli.api.appboy.eu/api/v3/data HTTP/1.1`

```=json
{
    "api_key": "0d5a1a3c-8fce-44aa-8b31-4637b2a9d3a6",
    "app_version": "26.13.0",
    "app_version_code": "877.0.0.0",
    "attributes": [
        {
            "push_token": "dBqcPVGKSVSs5ivy35_LCZ:APA91bHQTcT3CQnTB71sCSOc_OynODlaKVhvACLQRNL-VcmcnIzYEk8hWLPCptcw5FdxVwPHpH0d-oTe4ZIXsX8aYKNhEEyyOuSsVoQWYU9V3-VFtdM27x5NjurXDfLw8-NGxfb2dLIq",
            "user_id": "8bcd371c-b09f-4ae6-91b4-736a3a72459d"
        }
    ],
    "device": {
        "android_is_background_restricted": false,
        "carrier": "Android",
        "locale": "en_US",
        "model": "AOSP on IA Emulator",
        "os_version": "28",
        "remote_notification_enabled": true,
        "resolution": "1080x1977",
        "time_zone": "Europe/Budapest"
    },
    "device_id": "f20606a6-f98a-40ff-a8f1-eecb5ca37b7c",
    "events": [
        {
            "data": {
                "d": 31323
            },
            "name": "se",
            "session_id": "c20cf4ae-ac6d-412a-867d-3d3ebfbd6be9",
            "time": 1654681730.841,
            "user_id": "8bcd371c-b09f-4ae6-91b4-736a3a72459d"
        },
        {
            "data": {},
            "name": "ss",
            "session_id": "ced1ff73-ced4-431a-9ee5-ee67414cca9c",
            "time": 1654681730.846,
            "user_id": "8bcd371c-b09f-4ae6-91b4-736a3a72459d"
        }
    ],
    "respond_with": {
        "config": {
            "config_time": 1649254857
        },
        "triggers": true,
        "user_id": "8bcd371c-b09f-4ae6-91b4-736a3a72459d"
    },
    "sdk_version": "13.1.2",
    "time": 1654681730
}
```


#### adjust net
`POST https://app.adjust.net.in/sdk_click HTTP/1.1`

```
gps_adid_attempt:        1
country:                 US
api_level:               28
event_buffering_enabled: 0
hardware_name:           PSR1.180720.117
app_version:             26.13.0
app_token:               kykk6dnw927d
installed_at:            2022-06-02T14:42:39.167Z+0200
session_length:          0
created_at:              2022-06-02T14:46:46.095Z+0200
device_type:             phone
language:                en
gps_adid:                26176913-187b-48b1-a66b-6c46dd77e397
referrer_api:            google
source:                  install_referrer
connectivity_type:       1
mcc:                     310
device_manufacturer:     Google
display_width:           1080
time_spent:              0
device_name:             AOSP on IA Emulator
needs_response_details:  1
os_build:                PSR1.180720.117
updated_at:              2022-06-02T14:42:39.167Z+0200
cpu_type:                x86
screen_size:             normal
screen_format:           long
gps_adid_src:            service
subsession_count:        1
mnc:                     260
os_version:              9
google_play_instant:     0
android_uuid:            fbe42653-ff65-4220-911d-7ce8f2bee07d
referrer:                utm_source=google-play&utm_medium=organic
environment:             production
screen_density:          high
attribution_deeplink:    1
install_begin_time:      2022-06-01T16:24:13.000Z+0200
session_count:           1
display_height:          1977
package_name:            com.ftw_and_co.happn
os_name:                 android
network_type:            13
tracking_enabled:        1
sent_at:                 2022-06-02T14:46:46.145Z+0200
```

### Conclusion
Happn is an interesting dating app that tries to innovate in the area of location-based matching in its "cross paths" feature. As with any location sharing that is a slippery slope. A negligent implementation approach can result in location being leaked users and result in location tracking. From what we have seen geobox could be used to track when a user leaves a certain location.
Data provided for normal swiping usage is currently limited to next 18 profiles but contains too much profile information.

### Future work
In the future we would be interested to hypothesis that location could be tracked by "cross paths" feature. Next step would be using multiple user accounts to test if we can detect each other accounts.

For that we would need multiple phones, phones numbers and photos of real people. An alternative would be to use multiple emulators but or computers currently don't support more than one virtual device.

