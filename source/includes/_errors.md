# Errors

Yelp WiFi's Turnstyle APIs use the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request could not be understood by the server because of malformed syntax.
401 | Unauthorized -- Your API key is incorrect
403 | Forbidden -- The data requested is for administrators only
404 | Not Found -- The specified request could not be found
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The data requested has been removed from our servers
429 | Too Many Requests -- You're requesting too many kittens! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
