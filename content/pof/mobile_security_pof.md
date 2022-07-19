---
title: "Mobile Security: Plenty of Fish report"
url: /Spof/"
summary: Analysis of Plenty of Fish
tags:
    - Mobile Security
    - Assignment 2
    - Plenty of Fish
---

## Description
Plenty of Fish is a Canadian dating app with the typical like/dislike charts, but also has an area, where users can watch a live stream of other users. It has a lot of recommendation of users in nearly every tab. Without upgrading (paying them some money) the user can like/dislike the charts, write a message to other users and watch a stream. 

Source: https://en.wikipedia.org/wiki/POF_(dating_website)

**Device used:** Android emulator Pixel 4 Android 9 API level 28, x86

## Structure of report
1. Description
2. Registration process
3. Login process
6. Obtaining other users data
7. Direct profile access
9. Liking Process
10. Tracking
11. Conclusion

## Registration process
Inspecting the registration process, showed nothing suspicious. A number is required to register. Skipping that didn't work.

## Login process
Logged in we see that most of the communication of the app is encrypted. But some requests and responses are still in clear text.

At some early point in the research of the communication, burpsuit captured the following request. The API seems to send keys and also an encryption key.
Request:
```
POST /V2/Instance HTTP/1.1
Accept: text/json
Content-Type: application/json; charset=utf-8
User-Agent: Dalvik/2.1.0 (Linux; U; Android 9; AOSP on IA Emulator Build/PSR1.180720.117)
Host: pofapi.sinch.com
Connection: close
Accept-Encoding: gzip, deflate
Content-Length: 325

{
    "ApplicationKey":"d61c01ea-111d-4805-b662-d47cc14320a1",
    "Capabilities":[
        "ice-restart.1",
        "p2p",
        "push",
        "push.2",
        "push.3",
        "push.4",
        "srtp.1",
        "voip.1"
    ],
    "DeviceId":"0f10eeb6-01e6-40ad-8576-f3f391a704d2",
    "DeviceType":2,
    "PushData":"",
    "SdkVersion":"3.17.4",
    "Seed":"0",
    "Signature":"D5K4JWZbFNZxAKFZxmPPWsdcbcM=",
    "UserId":"316992311"
}
```
The Response contains this data
```=json
{
    "Data":{
        "Instance":{
            "UserId":"316992311",
            "ApplicationKey":"d61c01ea-111d-4805-b662-d47cc14320a1",
            "InstanceId":"d26ecbbd-f106-420b-9f4e-9cdeca242e84"
        },
        "Config":{
            "BroadcastChannel":"3c57058e-b8cd-45fb-85ec-3e8654e71f23B",
            "SignalChannel":"3c57058e-b8cd-45fb-85ec-3e8654e71f23S",
            "EncryptionKey":"jzIfVbDioSzztQpun9hqmQ==",
            "BroadcastSubscribeKey":"sub-c-c5e52f20-d446-11e3-b488-02ee2ddab7fe",
            "BroadcastPublishKey":"pub-c-491d2c47-7cf0-4cde-bc39-f282dcec788e",
            "SignalSubscribeKey":"sub-c-56224c36-d446-11e3-a531-02ee2ddab7fe",
            "SignalPublishKey":"pub-c-1ba05dee-92cb-49b5-83e2-96bec2103751",
            "PubSubUri":"rebtelsdk.pubnub.com",
            "Stun":"stun.l.google.com:19302",
            "Turn":"",
            "GcmSenderId":"1017500357356",
            "PubSubSsl":true
        }
    },
    "Result":200,
    "Message":"InstanceCreated"
}
```
Repeating the request gave the same result.

## Obtaining other users data

When clicking on the live stream tab, the app requests the streaming users with:
```
POST /1/functions/sns-video:getBroadcastsByNearbyMarquee HTTP/2
Host: video-api.gateway.pof.com
X-Parse-Session-Token: r:106d3f67bf0096b7b42aed87d7ef8774
X-Parse-Application-Id: sns-video
X-Parse-App-Build-Version: 1501955
X-Parse-App-Display-Version: 4.66.0.1501955
X-Parse-Os-Version: 9
X-Parse-Installation-Id: cf64fa12-ddc9-45ca-89d2-132a1e2b6b21
X-Parse-Client-Key: com.pof.android
User-Agent: Parse Android SDK 1.19.0 (com.pof.android/1501955) API Level 28
Content-Type: application/json
Content-Length: 64
Accept-Encoding: gzip, deflate

{"score":"0","nearMyAge":false,"gender":"female","pageSize":100}
```
The parameters here can be changed an effects the loaded in users. The score is the position in the loaded list and the pageSize is the number of users loaded in. So it does not really change the result. 
The response shows some interesting info about the users loaded in:
```=json
HTTP/2 200 OK
Date: Wed, 01 Jun 2022 06:49:42 GMT
Content-Type: application/json; charset=utf-8
Set-Cookie: AWSALB=I8EWtteIbhi22vDe81k4AZy6u3YzSGsHF35QcmuUfUFA2SH9x5OW6hut8z6CQZMd+Cka0Wh9VJPrmDVixdgKYslUsLjdTbPxN8o2EU/0cCCTdbKeuEToLoIwJPmL; Expires=Wed, 08 Jun 2022 06:49:42 GMT; Path=/
Set-Cookie: AWSALBCORS=I8EWtteIbhi22vDe81k4AZy6u3YzSGsHF35QcmuUfUFA2SH9x5OW6hut8z6CQZMd+Cka0Wh9VJPrmDVixdgKYslUsLjdTbPxN8o2EU/0cCCTdbKeuEToLoIwJPmL; Expires=Wed, 08 Jun 2022 06:49:42 GMT; Path=/; SameSite=None; Secure
Server: nginx
Vary: Accept-Encoding
X-Powered-By: Express
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET,PUT,POST,DELETE,OPTIONS
Access-Control-Allow-Headers: X-Parse-Master-Key, X-Parse-REST-API-Key, X-Parse-Javascript-Key, X-Parse-Application-Id, X-Parse-Client-Version, X-Parse-Session-Token, X-Requested-With, X-Parse-Revocable-Session, Content-Type
Etag: W/"2de2-5VUYajM9MfBbl0gefcDp0VXrTKo"

{

    "result":{
        "more":false,
        "score":"6",
        "broadcasts":[
            {
                "createdAt":"2022-06-01T04:48:12.484Z",
                "updatedAt":"2022-06-01T06:49:12.721Z",
                "activeUntil":{
                    "__type":"Date",
                    "iso":"2022-06-01T06:50:12.716Z"
                },
                "reports":[
                    {
                        "userId":"wSDYGOqhEj",
                        "reportedAt":1654063055515
                    }
                ],
                "socialNetwork":{
                    "__type":"Pointer",
                    "className":"SNSSocialNetwork",
                    "objectId":"gBkJOk6EBS"
                },
                "language":"en",
                "broadcasterAge":32,
                "userDetails":{
                    "createdAt":"2001-01-01T00:00:00.0Z",
                    "updatedAt":"2001-01-02T00:00:00.0Z",
                    "profilePic":{
                        "large":"https://pics.pof.com/thumbnails/size480/1186/75/59/4633dd5ee-4bc9-4972-9ccd-ea5071f66b3b.jpg",
                        "square":"https://pics.pof.com/thumbnails/size220/1186/75/59/4633dd5ee-4bc9-4972-9ccd-ea5071f66b3b.jpg"
                    },
                    "birthDate":
...
                    {"id":"fgisiSujdL",
                    "distanceInKm":0,
                    "isBattle":false,
                    "isPoll":false,
                    "isBlindModeActivated":false,
                    "isNextGuest":false,
                    "isNextDateGame":false,
                    "isDateNightModeActivated":false
                },
                {"id":"WBPFgGdBD2",
                "distanceInKm":0,
                "isBattle":false,
                "isPoll":false,
                "isBlindModeActivated":false,
                "isNextGuest":false,
                "isNextDateGame":false,
                "isDateNightModeActivated":false
            },
            {
                "id":"FU92vqVftf",
                "distanceInKm":0,
                "isBattle":false,
                "isPoll":false,
                "isBlindModeActivated":false,
                "isNextGuest":false,
                "isNextDateGame":false,
                "isDateNightModeActivated":false
            },
            {
                "id":"mLqTdSzYxL",
                "distanceInKm":0,
                "isBattle":false,
                "isPoll":false,
                "isBlindModeActivated":false,
                "isNextGuest":false,
                "isNextDateGame":false,
                "isDateNightModeActivated":false
            },
            {
                "id":"0N6EmEjgCP",
                "distanceInKm":0,
                "isBattle":false,
                "isPoll":false,
                "isBlindModeActivated":false,
                "isNextGuest":false,
                "isNextDateGame":false,
                "isDateNightModeActivated":false
            },
            {
                "id":"I0BAAnisdJ",
                "distanceInKm":0,
                "isBattle":false,
                "isPoll":false,
                "isBlindModeActivated":false,
                "isNextGuest":false,
                "isNextDateGame":false,
                "isDateNightModeActivated":false
            }
        ]
    },
    "correlation":{
        "id":"getNearByMarqueeVideos-pof:user:guest-1654066182368",
        "source":"search"
    }
}
```
There are also static links to the profile pictures, but in this case, it seems that the link is not directly related to the user id.

In the live stream section several tabs. In one of them, the app made a request and the response had lat. and longt. of my device in it: 
```=json
HTTP/2 200 OK
Date: Wed, 01 Jun 2022 08:25:05 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 441
Set-Cookie: AWSALB=dYbhTsmIKnBG+GGjJjbBAQie4Q1q4Mon7qnBZTV9jvRzgs5QMY0p+uFNRh3gM/Di1pU7aHSoQ5aqlA3JisQEt5FYyifTrdSLbrn6EWO9t7gKB6EN6S4XRa0ZyD05; Expires=Wed, 08 Jun 2022 08:25:05 GMT; Path=/
Set-Cookie: AWSALBCORS=dYbhTsmIKnBG+GGjJjbBAQie4Q1q4Mon7qnBZTV9jvRzgs5QMY0p+uFNRh3gM/Di1pU7aHSoQ5aqlA3JisQEt5FYyifTrdSLbrn6EWO9t7gKB6EN6S4XRa0ZyD05; Expires=Wed, 08 Jun 2022 08:25:05 GMT; Path=/; SameSite=None; Secure
Server: nginx
X-Powered-By: Express
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET,PUT,POST,DELETE,OPTIONS
Access-Control-Allow-Headers: X-Parse-Master-Key, X-Parse-REST-API-Key, X-Parse-Javascript-Key, X-Parse-Application-Id, X-Parse-Client-Version, X-Parse-Session-Token, X-Requested-With, X-Parse-Revocable-Session, Content-Type
Etag: W/"1b9-vggWPuhsLr+dI/M0yBAA2g4i//s"

{
    "objectId":"ZLYetyGZzl",
    "createdAt":"2022-06-01T08:25:00.241Z",
    "updatedAt":"2022-06-01T08:25:00.241Z",
    "username":"user_351791324@pof.net",
    "email":"user_351791324@pof.net",
    "birthDate":{
        "__type":"Date",
        "iso":"2001-01-01T08:00:00.000Z"
    },
    "locale":"en-US",
    "latitude":47.1,
    "longitude":15.4,
    "ACL":{
        "*":{
            "read":true
        },
        "ZLYetyGZzl":{
            "read":true,
            "write":true
        }
    },
    "__type":"Object",
    "className":"_User",
    "sessionToken":"r:0d0afaccdf02a64ba34189703ec72ce1"
}
```
But e.g. in the "nearby" tab the lat. and longt. were in the request.

## Direct profile access

To get users data the app sends following request:
```
GET /profile/users/pof:user:351791324 HTTP/2
Host: api.gateway.pof.com
Authorization: Bearer {Bearer Token}
User-Agent: pof/1501955 (id=com.pof.android) android/28 (9) sns/4.24.7 (release) okhttp/???
Accept-Language: en-US
Accept-Encoding: gzip, deflate
```
351791324 is my userid in this case.
The Response shows following:
```=json
HTTP/2 200 OK
Date: Wed, 01 Jun 2022 08:25:09 GMT
Content-Type: application/json
Content-Length: 1215
Set-Cookie: AWSALB=vpTA+JCypYbSVnJgVQqDtc+ks6yPbxuO5EOjL33ih2YRiaJiMfDPxEcUGrWwJ7+xPn3fLgA7w6go6Csidp09wqfvuM336aRwCjlqANzggahGVmXIHEST8f6Y3WJI; Expires=Wed, 08 Jun 2022 08:25:09 GMT; Path=/
Set-Cookie: AWSALBCORS=vpTA+JCypYbSVnJgVQqDtc+ks6yPbxuO5EOjL33ih2YRiaJiMfDPxEcUGrWwJ7+xPn3fLgA7w6go6Csidp09wqfvuM336aRwCjlqANzggahGVmXIHEST8f6Y3WJI; Expires=Wed, 08 Jun 2022 08:25:09 GMT; Path=/; SameSite=None; Secure
Set-Cookie: AWSALB=Z58VQloOFLlbskqgwbpOALVl9lS3Ts2cLuPahp4x1TAtcn2ri47xcFn7B0eNKJZwSBmM3rz1UsvI3tEDke6lIW1H+wssFrJtTdbEAPxC2nKd0J8sUatv1m95sKm4; Expires=Wed, 08 Jun 2022 08:25:09 GMT; Path=/
Set-Cookie: AWSALBCORS=Z58VQloOFLlbskqgwbpOALVl9lS3Ts2cLuPahp4x1TAtcn2ri47xcFn7B0eNKJZwSBmM3rz1UsvI3tEDke6lIW1H+wssFrJtTdbEAPxC2nKd0J8sUatv1m95sKm4; Expires=Wed, 08 Jun 2022 08:25:09 GMT; Path=/; SameSite=None; Secure
Vary: Accept-Encoding
Server: TMG-Gateway/2.0.21

{
    "about":"What is love?\n\nSurfing, traveling, films, good food",
    "bodyType":[
        "athletic"
    ],
    "covidVaccineStatus":null,
    "displayName":"JeffBayzoss1",
    "education":"some_college",
    "ethnicity":[
    ],
    "firstName":"JeffBayzoss1",
    "gender":"male",
    "hasChildren":"not_specified",
    "height":1830,
    "id":"pof:user:351791324",
    "images":[
        {
            "id":null,
            "square":"https://pics.pof.com/thumbnails/size220/1187/70/38/209b67a05-e67c-4e19-bf79-22bee43bb467.jpg",
            "large":"https://pics.pof.com/thumbnails/size480/1187/70/38/209b67a05-e67c-4e19-bf79-22bee43bb467.jpg"
        }
    ],
    "interestedIn":"women",
    "interests":[
    ],
    "languages":null,
    "lastName":null,
    "lastSeen":1654071516963,
    "liveAbout":"What is love?\n\nSurfing, traveling, films, good food",
    "locale":"en-US",
    "location":{
        "city":"Graz",
        "state":"Styria",
        "country":"AT"
    },
    "lookingFor":[
        "dating",
        "friendship"
    ],
    "network":"pof",
    "privacySettings":null,
    "registrationTs":1654065715680,
    "relationshipStatus":null,
    "religion":"not_specified",
    "searchGender":"male",
    "settings":null,
    "smoker":"not_specified",
    "verificationBadges":[
    ],
    "age":21,
    "relations":{
        "id":"pof:user:351791324",
        "following":false,
        "blocked":false,
        "$id":"/users/pof:user:351791324/relations",
        "$type":"resource"
    },
    "$type":"resource",
    "$id":"/users/pof:user:351791324"
}
```
It works also with other user ids, but the Bearer Token, which changes from time to time, needs to be valid. And it also shows nothing to revealing ...
There is also a similar request to the video api:
```
GET /1/users/313614240 HTTP/2
Host: video-api.gateway.pof.com
```
It shows similar response but in this case, making a request to another user gives an error:
```
HTTP/2 403 Forbidden
```
## Liking process
The liking process in this app is also encrypted. 

## Tracking
Inspecting the communication further showed, that the app logs what tab the user visits and what tab was previous visited:
```
POST /event-ingest/log HTTP/2
Host: api.gateway.pof.com
Authorization: Bearer {Bearer Token}
User-Agent: pof/1501955 (id=com.pof.android) android/28 (9) sns/4.24.7 (release) okhttp/???
Accept-Language: en-US
Content-Type: application/json; charset=UTF-8
Content-Length: 196
Accept-Encoding: gzip, deflate

{
    "events":[
        {
            "body":{
                "selected_tab":"new",
                "previous_tab":"for_you"
            },
            "event":"s_mobile_tmglive_ui_tab_selected",
            "version":2,
            "timestamp":1654096835661,
            "uuid":"d53bf710-aaef-431e-aeed-4c95aa095ea6"
        }
    ]
}
```
It also has some log requests to the API, but these are as well encrpyted.

## Conclusion
For this app it can be said that it does a good job in preventing user data leaked. Besides encrypting a lot of the traffic sent and received, it makes e.g. exposure of the distance harmless, because it's rounded presented in km (which would be a big area to find a person). 