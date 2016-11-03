# wiremock

WireMock is a flexible library for stubbing and mocking web services. Unlike general purpose mocking tools it works by creating an actual HTTP server that your code under test can connect to as it would a real web service.
It supports HTTP response stubbing, request verification, proxy/intercept, record/playback of stubs and fault injection, and can be used from within a unit test or deployed into a test environment.
It integrates seamlessly with Java, but can also be configured via JSON API.

How to Start WireMock Server ?

$ java -jar wiremock-standalone-2.2.2.jar

Defaul port is 8080 , but you can change the port using --port flag .

$ java -jar wiremock-standalone-2.2.2.jar --port 8000

To Create stub mapping do this :-

$ curl -X POST \
--data '{ "request": { "url": "/get/this", "method": "GET" }, "response": { "status": 200, "body": "Here it is!\n" }}' \
http://localhost:8080/__admin/mappings/new


And then fetch it back:

$ curl http://localhost:8080/get/this
Here it is!


SON file configuration
You can also use the JSON API via files. When the WireMock server starts it creates two directories under the current one: mappings and __files.

To create a stub like the one above by this method, drop a file with a .json extension under mappings with the following content:

{
    "request": {
        "method": "GET",
        "url": "/api/mytest"
    },
    "response": {
        "status": 200,
        "body": "More content\n"
    }
}
After restarting the server you should be able to do this:

$ curl http://localhost:8080/api/mytest
More content



Other way is here :--


Keep the json file in __file directory and in the same directory where you are running the wiremock server .


In json file write this code :-

{
    "request": {
        "method": "GET",
        "url": "/api/mytest"
    },
    "response": {
        "status": 200,
        "headers":
        {
          "Content-Type" : "application/json"
        },
      --"bodyFileName" :"memberCard.json"
// Keep this memberCard.json file in __file directory .
    }

}






