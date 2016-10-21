# AC3.2-APIs: Intro
---

### Readings

1.
2.

---
### Objectives

1. Introduce the concept of web based APIs
2. Give examples of popular webservices as being APIs to reinforce their ubiquity
3. Frame using APIs as being able to develop amazing apps that would not be possible on your own or without large development teams
4. Explain JSON a bit and show how to view some simple JSON using the Maps Geocode API
5. Bring in API documentation as what defines which requests are possible, and what their responses will be
6. Introduce Postman as a utility for quickly testing APIs
7. Search Geocode API in Postman

---
 
### API's, What Are They? 

> **How many weather apps do you think there are in the app store?**

I’d wager there must be in the *thousands*, at least. Some of those apps have entire teams dedicated to building the app, while some of them are a single person; a person who might have just done it as a weekend project. And despite the great variety of apps made, all of their data is (relatively) consistent.
 
But where are those developer teams, large and small, getting their weather data? I mean here you have 1000’s of different apps and they all have the same data set. How are they able to all present the same information?
 
The answer: from an __API__ (Application Programming Interface)

An API is a digital middleman - delivering data from some service as long as you ask for it in the right way. In this case, all of these weather apps are asking a weather-related API for data on the weather. In a broad sense **an API is a standard set of requests and responses that allows software to communicate.** And it is not just iOS apps that use API's: websites use them, Android devices use them, and computers use them. 
 
When iOS developers talk about API's we usually mean one of two things: 

1. Any library used to do a specific function in an app (for example UIKit could be considered a native iOS API for UI elements)
2. A REST API that is used to communicate with some service on the web, (like a weather API!)
 
----
### Why do APIs matter
 
__They allow you to develop software faster!__ The existance of APIs let you perform a variety of tasks that just take way too long to write out yourself. Can you imagine having to write out your own custom `JSONSerialization` function for every app you create?
 
In the context of web-based `REST API`s, they are how your app is going to talk to the world. There are hundreds of services out there that you might want to develop an app around

- A messaging app might use [Firebase](https://firebase.google.com/) for realtime communication
- A social media app that aggregates your top tweets will make use of the Twitter API ([Fabric](https://get.fabric.io/))
- A cloud-based, file storage app may decide to use the [Dropbox API](https://www.dropbox.com/developers) for storing, retrieving and editing files
- Perhaps you have a new take on location-based B2B services, and will make use of the [Foursquare API](https://developer.foursquare.com/) to load local business data
- Have a way to track pokemon in PokemonGo? Seems like a good place to use the [Google Maps API](https://developers.google.com/maps/) to display live GPS data
 
Apps can use multiple `REST` API's to perform complex tasks and create novel experiences for their users. With enough practice and skill, you can even develop your own APIs that other developers will use
 
---
### JSON (A deeper dive)

Since there is a wide possibility of devices that use API's and many differnt APIs providing unique services, there needs to be a standard for how they can all communicate effectively. The most common format in use is `JSON` (Javascript Object Notation). `JSON` defines how the data returned from an API will be formatted, and at its core is really just a dictionary. You may even often hear json referred to as a "json dictionary." Though, the structure and content that json dictionary's key/value pairs is up to the API. This is what we mean when we say that __"an API defines it's data response"__.
 
To get a sense of what JSON looks like, and how its used, let's go ahead and navigate to: http://maps.googleapis.com/maps/api/geocode/json
 
![Response JSON for maps API](./Images/googleMapsAPI.png)

Not an exciting result, but there's way more here than you might initially expect. For one, we see that the page is essentially a dictionary with three keys, `error_message, results, and status`. But why those three keys, and how can we know to expect them? And moreover, how did we know to go to that URL to even try this out?
 
----
### API Documentation

As mentioned before, API's define a standard for how software can communicate. Meaning that they define the kinds of *requests* that can be made to them, along with the *response* they will return. `JSON` defines the structure and syntax of the request/response, but its up to the API as to what should be included in a request and what could be included in the response. 
 
 All APIs will provide documentation on exactly what they expect in a request, and what they will return in a response. 
 
 ![Error message documentation](./Images/error_message.png)
 ![Status Codes documentation](./Images/status_codes.png)
  
<details> 
  <summary> Try it out: </summary>
    Switch out to Chrome and plug in the (URL)[https://developers.google.com/places/web-service/search] and scroll down the "Search" section
 
  The above is just an example to give background to the JSON response we got earlier. If we check out https://developers.google.com/places/web-service/search we'll be able to see every possible request and response that can be made by the API.
</details>

----
### Trying out an API

So looking at our previous request:

`http://maps.googleapis.com/maps/api/geocode/json`

... we see we're getting back an error. And judging by the APIs documentation, this is expected. Fortunately in the event of a bad request to an API, it is possible that the API returns a response with helpful error messages regarding what was bad about the request. In this case, we made an "invalid request" because we didn't include some additional information it was expecting to get along with the request. This additional information passed along with a request is called **parameters**. Parameters specify additional constraints on the requests we make. They may limit the data requested by filtering it by some criteria. 
 
<details>
  <summary> Example 1: Adding An Address to the API call </summary>
  Go back to your prior request and add the "address" key along with a "value" of the address of C4Q
  For example: http://maps.googleapis.com/maps/api/geocode/json?address=%2243-06%2045th%20Street%22
  Note: Parameters appear following a single ? and spaces are replaced by %20 for the actual request, but the google api will understand the request the exact same way as if you put in "43-06 45th Street"
</details>

<details>
  <summary> Example 2: Compare valid request with invalid one </summary>
  1. Notice how we get new data passed along with a valid request? 
  2. Bring up the API documentation page again and compare the keys with what the API states will be returned
  3. All of these results are listed in the API's documentation for this kind of response, so we will always know what to expect
</details>

Plugging away in a webbrowser is a lightweight way to test out an API, but we can get some real power by using some utilities specifically meant for making API requests.
 
 -----
 ### [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en)

Try this out: 

1. Open Postman and enter the prior googleAPI request (http://maps.googleapis.com/maps/api/geocode/json)
2. Add in "address" as a parameter along with some value
3. If this worked, try some other addresses

![Google Maps request in Postman](./Images/postman_request_googlempas.png)

```json
{
  "results": [
    {
      "address_components": [
        {
          "long_name": "The Falchi Building",
          "short_name": "The Falchi Building",
          "types": [
            "premise"
          ]
        },
        {
          "long_name": "31-00",
          "short_name": "31-00",
          "types": [
            "street_number"
          ]
        },
        
        // ... much more json...
        
       ]
     }
   ]  
 }
```


---
# Testing API Requests and [myJson](http://myjson.com/)

Think back to the `URLSession` demo: I was calling our hosted `json` an "API endpoint". And in some ways it does meet the requirement: we could send a request to the `URL` and we would receive a formatted `json` response. And at its core, an API is just a way to request and receive  info based on a set of parameters. Though, in practice API's are a bit more detailed than simply plugging in a `URL` endpoint and parsing out any data that gets returned. And it's likely that you'll be working with API's with incredible frequency in your development careers. 

Making test requests is a big part of software, and iOS, development. So much so that a fellow developer created the myJson site after he became annoyed that there were no simple ways of hosting json with the intention of testing network requests and json parsing. Making web requests, specifically to service APIs, and parsing the returned response is going to be a part of a vast majority of iOS apps. Think about all the apps you use that you can log in with Facebook! That's it's own API that needs integration in an iOS app.

Fortunately, since working with API's is such a ubiquoitous thing for all developers (especially ios, android and web) there are quite a few resources and tools available to make development as smooth as possible. Some of the most important tools are those that let us test out API requests to verify that our inputs and outputs are correct and what we expect. 

---
# The [Random User API](https://randomuser.me/)
One of my favorite APIs to use for quick testing of creating user accounts is the [Random User API](https://randomuser.me/). 
Many of the APIs discussed prior require some sort of authentication method, but fortunately the Random User API doesn't require it making it quite easy to hit the ground rounning with testing with it. 

> Side note, I found an easter egg in the source code of the site's documentation page and tweeted at the developer with my own take on it 😀 (it was a function named like konamiCode()). Could be a nice little anecdote on the development community culture in general. - Louis

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">nice easter egg <a href="https://twitter.com/solewolf1993">@solewolf1993</a> .. needs more iddqd though. is it open for api requests? <a href="http://t.co/7djehsLWx4">http://t.co/7djehsLWx4</a></p>&mdash; Louis Tur (@louistur) <a href="https://twitter.com/louistur/status/587827969529348096">April 14, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
![Tweet Image](http://i.imgur.com/Jeqcrdk.png)

---
# To Do: Exercises
1. I think this would be a good API for the students to test out requests and parameters due to the single endpoint, limited parameters, and easy to understand/straightforward documentation.
      - Thoughts: We could do an entire practice lesson on API usage with this API... making the requests, model, etc.. Doing this before moving onto the more complicated Aeris API may serve to ease the learning curve invovled.
    2. Part of this interaction should include clicking on the RandomUser image URLs to further reinforce the universality of the the URL and the need for the developer to handle not only the "plain text" dictionary portion of the json responses, but also their content can vary considerably and will impact how their app should function.
 
