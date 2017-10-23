creating valid application's keys:
https://api.ovh.com/g934.first_step_with_api

curl -s -H "Content-type: application/json" --header "X-Ovh-Application:YOURAPPLICATIONKEY" --data '{"accessRules":[{"method":"GET","path":"/*"},{"method":"POST","path":"/*"},{"method":"PUT","path":"/*"},{"method":"DELETE","path":"/*"}]}' https://api.ovh.com/1.0/auth/credential | python -m json.tool


answer:
{
    "consumerKey": "YOURCOMSUMERKEYWILLBEHERE",
    "state": "pendingValidation",
    "validationUrl": "https://eu.api.ovh.com/auth/?credentialToken=YOURCREDENTIALTOKENHERE"
}
