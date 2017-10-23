creating valid application's keys:
https://api.ovh.com/g934.first_step_with_api
https://github.com/ovh/python-ovh

create file ovh.conf
    [default]
    ; general configuration: default endpoint
    endpoint=ovh-eu

    ;ovh-eu for OVH Europe API
    ;ovh-ca for OVH North-America API
    ;soyoustart-eu for So you Start Europe API
    ;soyoustart-ca for So you Start North America API
    ;kimsufi-eu for Kimsufi Europe API
    ;kimsufi-ca for Kimsufi North America API

    [ovh-eu]
    ;configuration specific to 'ovh-eu' endpoint
    application_key=my_app_key
    application_secret=my_application_secret
    ; uncomment following line when writing a script application
    ; with a single consumer key.
    ;consumer_key=my_consumer_key

# Then run python-script (for all methods: GET, POST, DELETE, PUT - FULL ACCESS) and follow steps:

    # -*- encoding: utf-8 -*-

    import ovh

    # create a client using configuration
    client = ovh.Client()

    # Request RO, /me API access
    ck = client.new_consumer_key_request()
    ck.add_rules(ovh.API_READ_ONLY, "/me")

    # Request token
    validation = ck.request()

    print "Please visit %s to authenticate" % validation['validationUrl']
    raw_input("and press Enter to continue...")

    # Print nice welcome message
    print "Welcome", client.get('/me')['firstname']
    print "Btw, your 'consumerKey' is '%s'" % validation['consumerKey']



or like so:

    curl -s -H "Content-type: application/json" --header "X-Ovh-Application:YOURAPPLICATIONKEY" --data '{"accessRules":[{"method":"GET","path":"/*"},{"method":"POST","path":"/*"},{"method":"PUT","path":"/*"},{"method":"DELETE","path":"/*"}]}' https://api.ovh.com/1.0/auth/credential | python -m json.tool

response:
    {
        "consumerKey": "YOURCOMSUMERKEYWILLBEHERE",
        "state": "pendingValidation",
        "validationUrl": "https://eu.api.ovh.com/auth/?credentialToken=YOURCREDENTIALTOKENHERE"
    }


After that you can do evething you want via OVH OVH.