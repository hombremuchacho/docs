---
title: Turnstyle API Reference

language_tabs:
  - http

toc_footers:
  - <a href='https://getturnstyle.com'>Learn about Turnstyle</a>
  - <a href='https://login.getturnstyle.com'>Login to Turnstyle</a>
  - <a href='https://getturnstyle.com'>Check out our Engineering Blog</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Turnstyle's APIs provide access to the same data and metrics available on our 
dashboard through programmatic means. This is a living document so please be 
ure to check back frequently for updates. Our APIs are *only* available to active
Turnstyle customers. 

If you are interested in purchasing Turnstyle please contact sales@getturnstyle.com

If you have questions about our documentation please contact
support@getturnstyle.com 


# Authentication

> Headers

```raw

Content-type:application/json

Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=

```
> Body

```json
{
  "grant_type": "client_credentials"
}
```

> Response

```json
[
  {
    "access_token": "1746d9a0eba9afe5f210f8143aa27f5ebc845f63",
    "expires_in": 86400,
    "token_type": "bearer",
    "scope": "data user user-venues user-regions user-widgets navizon-site navizon-jack navizon-hub user-venues-list venue"
  }
] 
```

Before any requests can be made, you must first request an access token. 

Turnstyle uses OAuth 2.0 Authentication. Turnstyle requires the Id/Secret 
to be encoded using base64 encoding (id:secret). The access tokens expire 
every 24 hours. 

Turnstyle does 'leaky bucket' request throttling. If you require loosened 
throttling restrictions please contact support@getturnstyle.com

### HTTPS Request

`POST https://api-general.getturnstyle.com/access`


# Visitor Analytics

## List of Venues

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
[
  {
    "id": "4235675",
    "name": "14134",
    "address": "22 Wing Hornell Heights",
    "latitude": "0",
    "longitude": "0",
    "phone": "705-494-2011x 2286",
    "website": "",
    "city": "North Bay",
    "country": "Canada",
    "rss_range": "-69",
    "tz": "111",
    "tz_index": "14",
    "twitter_id": "",
    "facebook_id": "248132900755",
    "duration_threshold": "120",
    "start_of_day": "07:00:00",
    "is_updating": "0",
    "rss_campaign": "-90",
    "session_timeout": "4500",
    "raw_data": "0",
    "campaign_duration": "60",
    "rss_walkby": "-110",
    "visit_duration_keep_fraction": "0.8",
    "brand_colour": "",
    "logo": "https://s3.amazonaws.com/static.getturnstyle.com/venues/ed9fe4d9d66d150a770d6cd7eaa8b3d07f089975.png",
    "time_zone": "America/Toronto",
    "read_only": "0"
  },
  {
    "id": "4235676",
    "name": "14475",
    "address": "32 Government Rd.,",
    "latitude": "0",
    "longitude": "0",
    "phone": "705-337-5100",
    "website": "",
    "city": "Kapuskasing",
    "country": "Canada",
    "rss_range": "-69",
    "tz": "111",
    "tz_index": "14",
    "twitter_id": "",
    "facebook_id": "248132900755",
    "duration_threshold": "120",
    "start_of_day": "07:00:00",
    "is_updating": "0",
    "rss_campaign": "-90",
    "session_timeout": "4500",
    "raw_data": "0",
    "campaign_duration": "60",
    "rss_walkby": "-110",
    "visit_duration_keep_fraction": "0.8",
    "brand_colour": "",
    "logo": "https://s3.amazonaws.com/static.getturnstyle.com/venues/ed9fe4d9d66d150a770d6cd7eaa8b3d07f089975.png",
    "time_zone": "America/Toronto",
    "read_only": "0"
  }
]
```

A list of IDs corresponding to the venues that are currently owned by the account
that was authenticated.


### HTTPS Request

`GET https://api-general.getturnstyle.com/venues?access_token=ACCESS_TOKEN`

URI Parameters| Description                       | Example
------------  | --------------------------------- | ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth      | 0281a718b3a033f01dda311fab7cfe59066bbb73


## Active Visitors

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "4235666": [
    {
      "mac_id": 42727343,
      "wifi_uid": null,
      "first_seen": "2016-03-22T21:07:10.000Z",
      "last_seen": "2016-03-22T21:08:12.000Z",
      "max_rssi": -77,
      "latest_rssi": -83,
      "frames": 15
    },
    {
      "mac_id": 178827125,
      "wifi_uid": null,
      "first_seen": "2016-03-22T21:07:10.000Z",
      "last_seen": "2016-03-22T21:07:10.000Z",
      "max_rssi": -69,
      "latest_rssi": -69,
      "frames": 1
    }
  ],
  "4235671": [
    {
      "mac_id": 207211473,
      "wifi_uid": null,
      "first_seen": "2016-03-22T21:06:44.000Z",
      "last_seen": "2016-03-22T21:06:44.000Z",
      "max_rssi": -75,
      "latest_rssi": -75,
      "frames": 1
    },
    {
      "mac_id": 45279924,
      "wifi_uid": null,
      "first_seen": "2016-03-22T21:06:44.000Z",
      "last_seen": "2016-03-22T21:06:47.000Z",
      "max_rssi": -86,
      "latest_rssi": -90,
      "frames": 2
    }
  ]
}
```

A lists active vistors who currently have open sessions with a 'venue. 
Note: Session timeout length can be defined under venue settings in the 
dashboard.


### HTTPS Request

`GET https://api-general.getturnstyle.com/data/active-visitors?id=ID&access_token=ACCESS_TOKEN`

URI Parameters| Description                       | Example
------------  | --------------------------------- | ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth      | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue id, comma separated, string | 450007,45008


## Visitor Count -- By Day

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": [
    "1425358800"
  ],
  "length": 6,
  "request_time": 0.030459880828857,
  "has_data": true,
  "data": {
    "4234970": {
      "1425358800": [
        {
          "key": "2015-03-03",
          "values": {
            "total": 77,
            "new": 20
          }
        },
        {
          "key": "2015-03-04",
          "values": {
            "total": 4,
            "new": 1
          }
        },
        {
          "key": "2015-03-05",
          "values": {
            "total": 0,
            "new": 0
          }
        },
        {
          "key": "2015-03-06",
          "values": {
            "total": 54,
            "new": 16
          }
        }
      ]
    }
  }
}
```

The number of visitors seen at a particular venue. This is broken out by new 
visitors and total visitors. New visitors are visitors who have never been 
seen at the venue previously.


### HTTPS Request

`GET https://api-general.getturnstyle.com/data/visitors?id=ID&start=START&length=LENGTH&type=TYPE&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the first day of data returned | 1425358800
LENGTH        | Number of days since start date to return                  | 7
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Individual Visitors -- By Entry and Exit Time

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": [
    "1433822400"
  ],
  "length": 1,
  "request_time": 0.01253604888916,
  "has_data": true,
  "data": {
    "1433822400": [
      {
        "key": 0,
        "values": {
          "event_date": "2015-06-09",
          "mac_id": "325040",
          "venue_id": "4235668",
          "first_seen": "2015-06-09 21:26:29",
          "last_seen": "2015-06-09 21:59:27",
          "max_rssi": -47
        }
      },
      {
        "key": 1,
        "values": {
          "event_date": "2015-06-09",
          "mac_id": "373383",
          "venue_id": "4235668",
          "first_seen": "2015-06-09 12:22:21",
          "last_seen": "2015-06-09 13:24:00",
          "max_rssi": -55
        }
      },
      {
        "key": 2,
        "values": {
          "event_date": "2015-06-09",
          "mac_id": "379339",
          "venue_id": "4235668",
          "first_seen": "2015-06-09 15:52:17",
          "last_seen": "2015-06-09 16:02:37",
          "max_rssi": -54
        }
      }
    ]
  }
}

```

A lists of each individual user (as specified by a MAC ID), their entry time 
into the venue, their maximum detected RSSI, and their exit time from the venue.
Note: MAC ID is a unique device identifier, but it is not equal to the visitor's 
hardware MAC Address.


### HTTPS Request

`GET https://api-general.getturnstyle.com/data/visitor-data-condensed?id=ID&start=START&length=LENGTH&type=TYPE&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the first day of data returned | 1425358800
LENGTH        | Number of days since start date to return                  | 7
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Walk-By Count - By Day

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": [
    "1428292800"
  ],
  "length": 6,
  "request_time": 0.64939618110657,
  "has_data": true,
  "data": {
    "V4234970": {
      "1428292800": [
        {
          "key": "2015-04-06",
          "values": {
            "value": 317
          }
        },
        {
          "key": "2015-04-07",
          "values": {
            "value": 309
          }
        },
        {
          "key": "2015-04-08",
          "values": {
            "value": 268
          }
        }
      ]
    }
  }
}

```

The number of walk-bys detected by a venue by day. Walk-by traffic meets certain
criteria around RSSI and FRAMES to be counted as Walk-By (vs Visitors or Noise).


### HTTPS Request

`GET https://api-general.getturnstyle.com/data/walkby-growth?id=ID&start=start&length=LENGTH&type=type&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the first day of data returned | 1425358800
LENGTH        | Number of days since start date to return                  | 7
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Walk-By Count

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": "2015-01-25",
  "end": "2015-02-01",
  "length": 7,
  "request_time": 0.036996126174927,
  "target_data": [
    {
      "key": "Walkby",
      "values": {
        "value": 2444
      }
    }
  ],
  "cmp_data": [],
  "has_data": true
}

```

The number of walk-bys detected by a venue. Walk-by traffic meets certain criteria 
around RSSI and FRAMES to be counted as Walk-By (vs Visitors or Noise). This metric 
displays a summary of the walk-by traffic for the specified period and is not broken 
out by day.


### HTTPS Request

`GET https://api-general.getturnstyle.com/data/walkby?id=ID&start=start&length=LENGTH&type=type&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the first day of data returned | 1425358800
LENGTH        | Number of days since start date to return                  | 7
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Visit Duration

> Response

```raw

200

Content-Type:application/json

```

> Body

```json

{
  "start": "2015-01-25",
  "end": "2015-02-01",
  "length": 7,
  "request_time": 0.051873207092285,
  "target_data": [
    {
      "key": "5m",
      "values": {
        "value": 0
      }
    },
    {
      "key": "10m",
      "values": {
        "value": 0.028571428571429
      }
    },
    {
      "key": "30m",
      "values": {
        "value": 0.52380952380952
      }
    },
    {
      "key": "1h",
      "values": {
        "value": 0.41428571428571
      }
    },
    {
      "key": "2h",
      "values": {
        "value": 0.033333333333333
      }
    },
    {
      "key": "3h",
      "values": {
        "value": 0
      }
    },
    {
      "key": "4h",
      "values": {
        "value": 0
      }
    },
    {
      "key": "6h",
      "values": {
        "value": 0
      }
    },
    {
      "key": "9h",
      "values": {
        "value": 0
      }
    },
    {
      "key": ">12h",
      "values": {
        "value": 0
      }
    }
  ],
  "cmp_data": [],
  "has_data": true
}

```

The percentage of visitors in segmented time buckets, for the period specified. 
Time bucket are: <5m, 5-10m, 10-30m, 30-60m, 1-2h, 2-3h, 3-4h, 4-6h, 6-9h, 9-12h
and >12h.


### HTTPS Request

`GET https://api-general.getturnstyle.com/data/length-distro?id=ID&start=START&length=LENGTH&type=TYPE&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the first day of data returned | 1425358800
LENGTH        | Number of days since start date to return                  | 7
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Repeat Visitors

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": [
    "1425445200"
  ],
  "length": 6,
  "request_time": 0.08355188369751,
  "has_data": true,
  "data": {
    "4235676": {
      "1425445200": [
        {
          "key": "1",
          "values": {
            "value": 1335
          }
        },
        {
          "key": "2",
          "values": {
            "value": 110
          }
        },
        {
          "key": "3",
          "values": {
            "value": 33
          }
        },
        {
          "key": "4",
          "values": {
            "value": 9
          }
        },
        {
          "key": "5",
          "values": {
            "value": 7
          }
        },
        {
          "key": "6",
          "values": {
            "value": 8
          }
        },
        {
          "key": "7",
          "values": {
            "value": 2
          }
        },
        {
          "key": "8",
          "values": {
            "value": 5
          }
        },
        {
          "key": "9",
          "values": {
            "value": 4
          }
        },
        {
          "key": ">10",
          "values": {
            "value": 1
          }
        }
      ]
    }
  }
}

```

The number of visitors in 'visit frequency' buckets within the selected time 
period. Note: Visitors who have visited 10+ times are grouped into one visit-
frequency bucket.percentage of visitors in segmented time buckets, for the 
period specified. 

### HTTPS Request

`GET https://api-general.getturnstyle.com/data/repeat-distro?id=ID&start=START&length=LENGTH&type=TYPE&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the first day of data returned | 1425358800
LENGTH        | Number of days since start date to return                  | 7
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Intra-Day Visitors

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": [
    "1428292800"
  ],
  "length": 1,
  "timezones": [
    "America/Toronto"
  ],
  "request_time": 0.060209035873413,
  "has_data": true,
  "data": {
    "V4234970": {
      "1428292800": [
        {
          "key": "2015-04-06 04:00:00",
          "values": {
            "value": 0
          }
        },
        {
          "key": "2015-04-06 05:14:23",
          "values": {
            "value": 2
          }
        },
        {
          "key": "2015-04-06 05:42:36",
          "values": {
            "value": 3
          }
        },
        {
          "key": "2015-04-06 06:03:28",
          "values": {
            "value": 0
          }
        },
        {
          "key": "2015-04-06 10:27:43",
          "values": {
            "value": 3
          }
        },
        {
          "key": "2015-04-06 11:00:37",
          "values": {
            "value": 4
          }
        }
      ]
    }
  }
}

```

The number of visitors inside a venue at a specific time of day. The time 
increments whenever visitor(s) enter/exit *and* the AP reports data. This
metric returns data for the single day specified in the request, ie. 
2015-04-06. An additional request is required for each day of interest. 

### HTTPS Request

`GET https://api-general.getturnstyle.com/data/daily-visitors?id=ID&start=START&length=LENGTH&type=TYPE&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the day of data returned       | 1425358800
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Known Visitors

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": [
    "1425445200"
  ],
  "length": 1,
  "request_time": 0.066174983978271,
  "has_data": true,
  "data": {
    "4235676": {
      "1425445200": [
        {
          "key": 17408926,
          "values": {
            "first_name": "vimla",
            "last_name": "ranwani",
            "email": null,
            "gender": null,
            "facebook_name": null,
            "twitter_name": null,
            "phone": "+11234567890",
            "google_id": null,
            "birthday": null,
            "mac_id": 17408926,
            "device_os": "AndroidOS",
            "last_seen": "2015-03-05 19:55:31",
            "venue_id": 4235676,
            "visits": 2
          }
        },
        {
          "key": 69615390,
          "values": {
            "first_name": "Mike",
            "last_name": "anderson",
            "email": null,
            "gender": null,
            "facebook_name": null,
            "twitter_name": null,
            "phone": "+19991112222",
            "google_id": null,
            "birthday": null,
            "mac_id": 69615390,
            "device_os": "iOS",
            "last_seen": "2015-03-06 05:32:43",
            "venue_id": 4235676,
            "visits": 2
          }
        }
      ]
    }
  }
}

```

The details of known visitors (visitors who have a Turnstyle profile), who visited
the venue during the specified time period, including name, email, phone number,
Facebook/Google/Twitter ID and device-type. The 'key' is the same as the wifi_uid
in other end-points.

### HTTPS Request

`GET https://api-general.getturnstyle.com/data/social-wifi-metrics?id=ID&start=START&length=LENGTH&type=TYPE&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the day of data returned       | 1425358800
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V

## Visitor Network Trends

> Response

```raw

200

Content-Type:application/json

```

> Body

```json
{
  "start": [
    "1428292800"
  ],
  "length": 6,
  "request_time": 0.17561197280884,
  "has_data": true,
  "data": {
    "V4234970": {
      "1428292800": [
        {
          "key": "Cafes",
          "values": {
            "value": 48
          }
        },
        {
          "key": "Family/Casual Dining",
          "values": {
            "value": 11
          }
        },
        {
          "key": "Casual/Value Clothing",
          "values": {
            "value": 8
          }
        },
        {
          "key": "Mexican Dining",
          "values": {
            "value": 5
          }
        },
        {
          "key": "Pub",
          "values": {
            "value": 5
          }
        },
        {
          "key": "Fine Dining",
          "values": {
            "value": 5
          }
        },
        {
          "key": "Healthy Eating",
          "values": {
            "value": 2
          }
        }
      ]
    }
  }
}
```

The aggregrate profiles of visitors of a venue based on their attributes across
the Turnstyle network.

### HTTPS Request

`GET https://api-general.getturnstyle.com/data/network-trends?id=ID&start=START&length=LENGTH&type=TYPE&access_token=ACCESS_TOKEN`

URI Parameters| Description                                                | Example
------------  | -----------------------------------------------------------| ---------------------------------------
ACCESS_TOKEN  | the token generated in oauth                               | 0281a718b3a033f01dda311fab7cfe59066bbb73
ID            | venue/group id, comma separated, string                    | 450007,45008
START         | Unix timestamp representing the day of data returned       | 1425358800
TYPE          | What type of ID is being submitted, venue (V) or group (G) | V


# Custom Campaigns & Coupons

## Campaign Post URLs

> Post

```raw

https://api-general.getturnstyle.com/url_defined_in_campaign_portal/trigger/venue_id/mac_id/user_id/timestamp 

```

Campaign POST URLs can be set when creating or modifying a campaign (inside the
Turnstyle dashboard), in the message tab > Advanced (found using the gear in the 
top right of the modal window.

If a campaign has a POST URL set, then when the campaign would have normally just 
sent a message a webhook will instead first send a POST request to that URL. If 
there is no response with 3 seconds, the email/sms message will send. 

### HTTPS Request

`POST https://api-general.getturnstyle.com/url_defined_in_campaign_portal/trigger/venue_id/mac_id/user_id/timestamp`

URI Parameters| Description                                                            | Example
------------  | -----------------------------------------------------------------------| ------------
trigger   | The type of campaign that is sent, Real-time (R) or global (G)              | R
venue_id  | The venue that triggered the campaign, integer                              | 450007
mac_id    | The visitor's device ID that triggered the campaign, integer                | 1235421
user_id   | The visitors Turnstyle ID (or wifi_uid) that triggerd the campaign, integer | 69615390
timestamp | The time that the campaign was triggered, unix                              | 1425358800

## Custom Campaign and Coupon Response

> Headers

```raw

Content-Type: application/json

Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=

```

> Post URL 

```raw

https://api-general.getturnstyle.com/response_to_Turnstyle/send_bool/coupon_name/coupon_description/redeem_message/expiry_date/barcode_value/barcode_type/email_logo/email_subject/email_body/email_from/email_html_bool/tweets/sms_message` 

```


To tailor the message and/or coupon that Turnstyle delivers to the end-client,
you can specify the parameters to send via a RESPONSE to the POST Turnstyle 
sends.

The 'override' properties are optional. The campaign's message and coupon (if 
the campaign has one) will only be sent if 'send' is true or if a response is 
not provided. If the 'override' property is given, it will override properties 
of the campaign or coupon just for that message. Properties that are not specified 
will have the values given to the campaign in Turnstyle's application.

### HTTPS POST URL

`POST https://api-general.getturnstyle.com/response_to_Turnstyle/send_bool/coupon_name/coupon_description/redeem_message/expiry_date/barcode_value/barcode_type/email_logo/email_subject/email_body/email_from/email_html_bool/tweets/sms_message`

URI Parameters     | Description                                                                                         | Example
-----------------  | ----------------------------------------------------------------------------------------------------| ------------
send_bool          | Indicator if the message should be sent or not, boolean                                             | True
coupon_name        | The name of the coupon, displayed in the coupon ehader                                              | 450007
coupon_description | The content of the coupon                                                                           | 1235421
redeem_message     | The message that appears when the coupon redeem button is clicked. Not available if using a barcode | 69615390
exipiry_date       | The date the coupon expires, unix                                                                   | 1425358800
barcode_value      | The content of the barcode, disregard if barcode is not used                                        | 101231
bar_code_type      | The type of barcode displayed, disregard if barcode is not used                                     | UFA-1
email_logo         | The logo in the email, dispayed at the top of the message                                           | http://imgur.com/as123sa
email_subject      | The subject line of the email                                                                       | HELLO WORLD
email_body         | The content of the email                                                                            | Welcome to Turnstyle
email_from         | The from line of the email                                                                          | Turnstyle Solutions
email_html_bool    | Indicator if the email has html content (recommended), boolean, default enabled                     | True
tweets             | Content of the tweet                                                                                | Hello @World
sms_message        | Content of the text message                                                                         | Hello World

# Captive Portal Webhooks

## Captive Portal Webhook POST

> POST URL

```raw

https://api-general.getturnstyle.com/created_by_customer_success_team/mac_id/user_id/first_name/last_name/phone/email/gender/birthday/job/company/locale/facebook_id/twitter_name/twitter_id/google_id/linkedin_id 

```

Turnstyle has the capability of sending POST notifications when users sign in 
to specified access points. When a user signs into one of the associated venues, 
a POST request is made to the URL. If you would like to enable functionality, 
please contact support@getturnstyle.com 

Note: Not all of the user properties will be present, depending on what method 
the user used to authenticate, and what info they granted Turnstyle to have access 
to.

### Response 

Servers referenced in sign-in webhooks may respond with JSON of the form 
{"radiusAttributes": {"key", "value"}}. The key-value pairs in the "radiusAttributes" 
property will override RADIUS attribute values that would otherwise be sent to 
the user. For example, {"radiusAttributes": {"Session-Timeout": 600}} would 
override the Session-Timeout RADIUS attribute and restrict the user's session 
to 10 minutes. Attribute names are not case-sensitive. Allowed attributes are 
Session-Timeout, Idle-Timeout, WISPr-Bandwidth-Max-Up, WISPr-Bandwidth-Max-Down, 
ChilliSpot-Max-Output-Octets and ChilliSpot-Max-Input-Octets. If WISPr-Bandwidth-
Max-Up or WISPr-Bandwidth-Max-Down are set, analogous vendor-specific attributes 
will be set automatically.

If you do not wish to override any RADIUS attributes, you may simply respond 
with "OK" or {} (an empty JSON object).

You should give timely responses as Turnstyle's captive portal will wait up 
to several seconds for them before continuing to sign a user in. Note that 
additional fields may be present in the "user" object of the JSON sent 
depending on venue geography (example: AirMiles)

### HTTPS Request

`POST https://api-general.getturnstyle.com/created_by_customer_success_team/mac_id/user_id/first_name/last_name/phone/email/gender/birthday/job/company/locale/facebook_id/twitter_name/twitter_id/google_id/linkedin_id`


### RADIUS Settings 

Parameter                    | Description                                               | Example (Kilobytes)
---------------------------- | --------------------------------------------------------- | -------------------
Airtight-Download-Limit      | User download bandwidth limit                             | 46 (mB)
Airtight-Upload-Limit        | User upload bandwidth limit                               | 49 (mB)
ChilliSpot-Max-Input-Octets  | User download capcity                                     | 104857600 (bytes)
ChilliSpot-Max-Output-Octets | User upload capcity                                       | 214958080 (bytes)
Idle-Timeout                 | Inactive time on the network before a user's session ends | 300 (seconds)
Maximum-Data-Rate-Downstream | Download speed limit                                      | 4096 (kB)
Maximum-Data-Rate-Upstream   | Upload speed limit                                        | 4096 (kB)
Port-Limit                   | Number of simultaneous ports a user can be using          | 5 (ports)
Session-Timeout              | Time before the session ends                              | 600 (seconds)
WISPR-Bandwidth-Max-Down     | User download bandwidth limit                             | 320000 (bytes)
WISPR-Bandwidth-Max-Up       | User upload bandwidth limit                               | 320000 (bytes)

# Third-Party Captive Portal 

When posting user data, the access token will need to be provided in every 
request. Below, "ap_mac" means the access point's MAC address and "client_mac" 
means the MAC address of the user signing into that access point. The MAC 
addresses are not case sesnitive and insensitive to whether they contain colons, 
hyphens, periods or no delimiters. The "opt_in" boolean data parameter is 
required, if not included you will recieve a 400 response information.

To identify which Access Point a user is connecting on, you are required to 
send a device identifier. This can be the Access Point's MAC Address (ap_mac), 
or another unique identifier (ap_alias) which can be up to an 80 character string.

## Facebook Authentication 

> POST URL

```raw

https://wifi.getturnstyle.com/auth/facebook/third-party

```

> Header

```raw

Content-Type: application/json

```

> Body

```json

{
   "access_token": "abc123",
   "ap_mac": "ac:86:11:22:33:44",
   "ap_alias": "northwest basement",
   "client_mac": "00:18:11:22:33:44",
   "data": {
      "first_name": "Jane",
      "last_name": "Doe",
      "birthday": "1975-05-26",
      "gender": "F",
      "email": "jane.doe@gmail.com",
      "facebook_id": 1000000001,
      "interests": [
         "country music",
         "skiing",
         "tennis",
         "cooking"
      ],
      "opted_in": 1
   }
}

```

Each authentication method requires specific properties. If required properties
are not included, a 400 error will be given. If a property is not listed below
that property is not accepted for this authentication route. 

### HTTPS Request

`POST https://wifi.getturnstyle.com/auth/facebook/third-party`

Property     | Description                                     | Required
------------ | ------------------------------------------------| ------------
access_token | The token generated in oauth                    | Yes
ap_mac       | MAC address of the AP the user is connecting to | No, if ap_alias is provided
ap_alias     | Other identifier for the AP                     | No, if ap_mac provided 
client_mac   | User's device MAC adddress                      | Yes
first_name   | User's first name                               | No (note, if not provided emails will not have a personalized greeting)
last_name    | User's last name                                | No 
birthday     | User's birthday, yyyy-mm-dd                     | No
gender       | User's gender                                   | No 
email        | User's email                                    | No 
facebook_id  | User's Facebook profile ID                      | Yes 
interests    | Interests the user has                          | No 
opted_in     | Is the user opted-in for marketing, boolean     | Yes

## Google Authentication 

> POST URL

```raw

https://wifi.getturnstyle.com/auth/google/third-party

```

> Header

```raw

Content-Type: application/json

```

> Body

```json

{
  "access_token": "abc123",
  "ap_mac": "ac:86:11:22:33:44",
  "ap_alias": "northwest basement",
  "client_mac": "00:18:11:22:33:44",
  "data": {
    "first_name": "Jane",
    "last_name": "Doe",
    "birthday": "1975-05-26",
    "gender": "F",
    "email": "jane.doe@gmail.com",
    "google_id": 1000000001,
    "opted_in": 1
  }
}

```

Each authentication method requires specific properties. If required properties
are not included, a 400 error will be given. If a property is not listed below
that property is not accepted for this authentication route. 

### HTTPS Request

`POST https://wifi.getturnstyle.com/auth/google/third-party`

Property     | Description                                     | Required
------------ | ------------------------------------------------| ------------
access_token | The token generated in oauth                    | Yes
ap_mac       | MAC address of the AP the user is connecting to | No, if ap_alias is provided
ap_alias     | Other identifier for the AP                     | No, if ap_mac provided 
client_mac   | User's device MAC adddress                      | Yes
first_name   | User's first name                               | No (note, if not provided emails will not have a personalized greeting)
last_name    | User's last name                                | No 
birthday     | User's birthday, yyyy-mm-dd                     | No
gender       | User's gender                                   | No 
email        | User's email                                    | No 
google_id    | User's Google profile ID                        | Yes 
opted_in     | Is the user opted-in for marketing, boolean     | Yes

## Google Authentication 

> POST URL

```raw

https://wifi.getturnstyle.com/auth/twitter/third-party

```

> Header

```raw

Content-Type: application/json

```

> Body

```json

{
  "access_token": "abc123",
  "ap_mac": "ac:86:11:22:33:44",
  "ap_alias": "northwest basement",
  "client_mac": "00:18:11:22:33:44",
  "data": {
    "name": "Jane Doe",
    "twitter_name": "janedoe",
    "twitter_id": 2000000001,
    "opted_in": 1
  }
}

```

Each authentication method requires specific properties. If required properties
are not included, a 400 error will be given. If a property is not listed below
that property is not accepted for this authentication route. 

### HTTPS Request

`POST https://wifi.getturnstyle.com/auth/twitter/third-party`

Property     | Description                                     | Required
------------ | ------------------------------------------------| ------------
access_token | The token generated in oauth                    | Yes
ap_mac       | MAC address of the AP the user is connecting to | No, if ap_alias is provided
ap_alias     | Other identifier for the AP                     | No, if ap_mac provided 
client_mac   | User's device MAC adddress                      | Yes
name         | User's name as denoted by Twitter's API         | No (note, if not provided emails will not have a personalized greeting)
twitter_name | User's twitter name                             | Yes 
twitter_id   | User's Twitter profile ID                       | Yes 
opted_in     | Is the user opted-in for marketing, boolean     | Yes

## SMS Authentication 

> POST URL

```raw

https://wifi.getturnstyle.com/auth/sms/third-party

```

> Header

```raw

Content-Type: application/json

```

> Body

```json
{
  "access_token": "abc123",
  "ap_mac": "ac:86:11:22:33:44",
  "ap_alias": "northwest basement",
  "client_mac": "00:18:11:22:33:44",
  "data": {
    "first_name": "Jane",
    "last_name": "Doe",
    "phone": "+14159001010",
    "birthday": "1975-05-26",
    "gender": "F",
    "email": "jane.doe@gmail.com",
    "opted_in": 1
  }
}

```

Each authentication method requires specific properties. If required properties
are not included, a 400 error will be given. If a property is not listed below
that property is not accepted for this authentication route. 

### HTTPS Request

`POST https://wifi.getturnstyle.com/auth/sms/third-party`

Property     | Description                                     | Required
------------ | ------------------------------------------------| ------------
access_token | The token generated in oauth                    | Yes
ap_mac       | MAC address of the AP the user is connecting to | No, if ap_alias is provided
ap_alias     | Other identifier for the AP                     | No, if ap_mac provided 
client_mac   | User's device MAC adddress                      | Yes
first_name   | User's first name                               | No (note, if not provided emails will not have a personalized greeting)
last_name    | User's last name                                | No 
birthday     | User's birthday, yyyy-mm-dd                     | No
gender       | User's gender                                   | No 
email        | User's email                                    | No 
phone        | User's phone number                             | Yes 
opted_in     | Is the user opted-in for marketing, boolean     | Yes

## Email Authentication 

> POST URL

```raw

https://wifi.getturnstyle.com/auth/email/third-party

```

> Header

```raw

Content-Type: application/json

```

> Body

```json
{
  "access_token": "abc123",
  "ap_mac": "ac:86:11:22:33:44",
  "ap_alias": "northwest basement",
  "client_mac": "00:18:11:22:33:44",
  "data": {
    "first_name": "Jane",
    "last_name": "Doe",
    "phone": "+14159001010",
    "birthday": "1975-05-26",
    "gender": "F",
    "email": "jane.doe@gmail.com",
    "opted_in": 1
  }
}

```

Each authentication method requires specific properties. If required properties
are not included, a 400 error will be given. If a property is not listed below
that property is not accepted for this authentication route. 

### HTTPS Request

`POST https://wifi.getturnstyle.com/auth/email/third-party`

Property     | Description                                     | Required
------------ | ------------------------------------------------| ------------
access_token | The token generated in oauth                    | Yes
ap_mac       | MAC address of the AP the user is connecting to | No, if ap_alias is provided
ap_alias     | Other identifier for the AP                     | No, if ap_mac provided 
client_mac   | User's device MAC adddress                      | Yes
first_name   | User's first name                               | No (note, if not provided emails will not have a personalized greeting)
last_name    | User's last name                                | No 
birthday     | User's birthday, yyyy-mm-dd                     | No
gender       | User's gender                                   | No 
email        | User's email                                    | Yes 
phone        | User's phone number                             | No 
opted_in     | Is the user opted-in for marketing, boolean     | Yes

## User Update 

> POST URL

```raw

https://api-general.getturnstyle.com/api/user-update/account_name

```

> Header

```raw

Content-Type: application/json

```

> Body

```json
{
  "access_token": "abc123",
  "user_id": "12345",
  "data": {
    "first_name": "Jane",
    "last_name": "Doe",
    "email": "jane.doe@gmail.com",
    "phone": "+14161234567",
    "opted_in": 0
  }
}

```

You may have a use case in which a user updates their information on your 
application's side, and you would like to sync this data back to Turnstyle. For 
example, if on your POS a user changes their email or phone number, you can use 
the following API to update the user profile on the Turnstyle platform instead of 
waiting for the user to sign back into the Wi-Fi portal to provide their updated 
information. Note All of the fields under 'data' are optional (but you must 
include at least one). Also, under the 'data' field, you are able to update all of 
the same fields as the different data types in the above user registration methods. 

The account_name in the URL will be provided by Turnstyle to you.

### HTTPS Request

`POST https://api-general.getturnstyle.com/api/user-update/account_name`

Property     | Description                                     | Required
------------ | ------------------------------------------------| ------------
access_token | The token generated in oauth                    | Yes
user_id      | The visitors Turnstyle ID (or wifi_uid)         | Yes
first_name   | User's first name                               | No (
last_name    | User's last name                                | No 
email        | User's email                                    | Yes 
phone        | User's phone number                             | No 
opted_in     | Is the user opted-in for marketing, boolean     | Yes

# Advanced Social WiFi Settings 

## Include User Data Check Box


This section contains documentation for some of the advanced features available 
when customizing a venue's social wifi settings in the Turnstyle dashboard. 
These are NOT Turnstyle endpoints.

When enabled, all available user data will be appended to the redirect url as 
query string parameters. The data available is dependent on the user's 
authentication method and permissions granted.

Fields with null values will be stripped and not included in the redirect query 
string.

### Redirect URL Example

`http://www.redirecturl.com/?id=1&email=noreply%40getturnstyle.com&first_name=John&last_name=Smith&gender=M&birthday_approximate=0&opted_in=1&email_valid=1`

Property             | Description                                
-------------------- | -------------------------------------------
id                   | User's Turnstyle ID (or wifi_uid)
birthday             | User's birthday 
birthday_approximate | Is the user's birthday guessed, boolean
company              | Where the user works, as per LinkedIn
email                | User's email address 
email_valid          | Is the user's email validated, boolean
facebook_id          | User's Facebook profile ID
first_name           | User's first name 
last_name            | User's last name
gender               | User's gender 
google_id            | User's Google profile ID 
job                  | User's job, as per LinkedIn 
linkedin_id          | User's LinkedIn profile ID
linkedin_url         | User's LinkedIn profile URL
locale               | User's language 
opted_in_time        | Date the user opted in to messaging 
phone                | User's phone number 
twitter_name         | User's Twitter handle 
zip_code             | User's zip code/postal code
