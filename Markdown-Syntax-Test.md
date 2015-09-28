---
title: API Reference

language_tabs:
  - json

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>
  - <a href='http://www.jsoneditoronline.org/'>Validate JSON online with syntax highlighting</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the FLYTZE API! 

You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](http://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Making a Request

```http
POST /thewall HTTP/1.1
Host: flytzedev-flytzedev1deployment.azurewebsites.net
Content-Type: application/json
Cache-Control: no-cache
Postman-Token: 79584588-31d2-e75d-e5aa-6ab2c3abf2d4

{
  "username": "brycesublette@gmail.com",
  "sentTime": "2015-8-4T17:40:00",
  "function": "search",
  "params": {
    "arrivalLocation": "Boulder Municipal Airport (WBU)",
    "departureLocation": [
      "Indianapolis International Airport (IND)",
      "China Airport (CA)"
    ],
    "departureTime": "2015-10-02T01:00:18",
    "departureFlexibility": 3,
    "index": 0
  },
  "hash": "728da4b84c35206e3941a101933cdd28bf68a192ce598524a034e814"
}
```

```json
{
  "username": "brycesublette@gmail.com",
  "sentTime": "2015-8-4T17:40:00",
  "function": "search",
  "params": {
    "arrivalLocation": "Boulder Municipal Airport (WBU)",
    "departureLocation": [
      "Indianapolis International Airport (IND)",
      "China Airport (CA)"
    ],
    "departureTime": "2015-10-02T01:00:18",
    "departureFlexibility": 3,
    "index": 0
  },
  "hash": "728da4b84c35206e3941a101933cdd28bf68a192ce598524a034e814"
}
```



The FLYTZE API was developed to allow for easy intagration into a variety of systems. To simplify the process all requests should be directed to one end point [Wall](http://flytzedev-flytzedev1deployment.azurewebsites.net/thewall). This endpoint is referred to as the wall and serves the purpose of validating all traffic. To improve readability all requests and responses are in the JSON format.


<aside class="notice">
You should never send the <code>token</code>.
</aside>

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
username | true | The email of the user
sentTime | true | Time front-end created the request
function | true | Action being performed
params | true | Parameters that are passed to the function
hash | true | The hash of the request. .
token | true | A token is associated with each account. It is similar to a password as it verfies the request was sent by the specified user. Each time a user is logs in a token will be passed back. The token should be stored for the enirity of the session. Logging in generates a new token causing the previous token to expire.

# Search

## Trips
```json
{
  "username": "brycesublette@gmail.com",
  "token": "TokenHere",
  "sentTime": "2015-8-1T17:40:00",
  "function": "search.trips",
  "params": {
    "arrivalLocation": "Boulder Municipal Airport (WBU)",
    "departureLocation": "Indianapolis International Airport (IND)",
    "departureTime": "2015-10-02T01:00:18.965Z",
    "departureFlexibility": 3,
    "index": 0
  },
  "hash": "6dsf0c836790bfb48e3dc8614cc8c2542973c5f7649845f77df65070"
}
```

> The above command returns JSON structured like this:

```json
{
  " success": true,
  "error": "",
  "departures": [
    {
      "id": "ObjectId(55a736cee4b07e03cc6ac5fa)",
      "departureLocation": "IndianapolisInternationalAirport(IND)",
      "departureTime": "2015-10-02T01: 00: 18.965Z",
      "arrivalLocation": "BoulderMunicipalAirport(WBU)",
      "arrivalTime": "2015-10-02T03: 30: 18.965Z",
      "flightDurationTime": "02:30",
      "openSeats": 8,
      "operatedBy": "WinnerAviation",
      "isFlytze": true,
      "planeId": "55a74198e4b07e03cc6ac65a",
      "cost": 3600,
      "costPerSeat": [
        {
          "seat": 1,
          "cost": 350.5
        }
      ]
    }
  ]
}
```

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
arrivalLocation | true | the arrival location
departureLocation | true | the departure location
departureTime | true | the departure date time (UTC)
*departureFlexibility | false | the plus/minus days the user is flexible for departure
index | true | the current index to load


# FBO

## Read All FBOs

```json
{
  "function": "fbo.readAll",
  "params": {}
}
```

> The above command returns JSON structured like this:

```json
{
  "fbo": {
    "id": "55be6c2eb8cff92350e3a114",
    "name": "WinnerAviation",
    "phoneNumber": "",
    "agreement": "/winterAviationTos.html",
    "email": ""
  },
  "success": true,
  "error": ""
}
```

Read all FBOs

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

## Read By ID

```json
{
  "function": "fbo.readById",
  "params": {
    "id": "55be6c2eb8cff92350e3a114"
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "fbo": {
    "id": "55be6c2eb8cff92350e3a114",
    "name": "WinnerAviation",
    "phoneNumber": "",
    "agreement": "/winterAviationTos.html",
    "email": ""
  },
  "success": true,
  "error": ""
}
```

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | true | the fbo id

## Create

```json
{
  "function": "fbo.createFbo",
  "params": {
    "agreement": "/winterAviationTosv2.html",
    "phoneNumber": "555-555-5555",
    "email": "winner@awesome.com",
    "name": "Winner Aviation V2"
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "id": "55c3f54eb8cff9160863a109",
  "success": true,
  "error": ""
}
```
Create a new FBO

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
name | true | the fbo's name
agreement | true | the url to the fbo's agreement
*phoneNumber | false | the fbo's phone number	
*email | false | the fbo's email

## Update

```json
{
  "function": "fbo.update",
  "params": {
    "id": "55c3f54eb8cff9160863a109",
    "lastUpdatedTime": "ISODate(2015-08-07T00:01:17.868Z)",
    "email": "",
    "phoneNumber": "777-777-7777",
    "name": "Winner Aviation V3",
    "agreement": "/winterAviationTos.html",
    "createdTime": "ISODate(2015-08-07T00:01:17.868Z)"
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "error": ""
}
```
Update an existing FBO

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | true | the fbo's id
name | true | the fbo's name
agreement | true | the url to the fbo's agreement
phoneNumber | true | the fbo's phone number
email | true | the fbo's email

## Delete

```json
{
  "function": "fbo.delete",
  "params": {
    "id": "55be6c2eb8cff92350e3a114"
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "error": ""
}
```
Delete an FBO by ID

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | true | the fbo id

# Plane

## Read All

```json
{
  "function": "plane.readAll",
  "params": {}
}
```

> The above command returns JSON structured like this:

```json
{
  "plane": {
    "id": "55a74198e4b07e03cc6ac65a",
    "cruiseSpeed": 325,
    "engine": "SingleTurboprop",
    "fboId": "55a74297e4b07e03cc6ac65e",
    "fboOwner": "WinnerAviation",
    "Images": [
      "http: //seattleclouds.com/myapplications/daly365/AircraftGuide/EpicLT.jpg",
      "http: //www.flightglobal.com/assets/getasset.aspx?itemid=40851"
    ],
    "Type": "EpicLT",
    "maxRange": 1625,
    "seatCount": 6,
    "features": [
      "champagne",
      "fullystockedbar",
      "surroundsound",
      "wifi"
    ],
    "maxCruiseAltitude": 28000
  },
  "success": true,
  "error": ""
}
```
Read all planes

## Read by ID

```json
{
  "function": "plane.readById",
  "params": {
    "id": "55a74198e4b07e03cc6ac65a"
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "plane": {
    "id": "55a74198e4b07e03cc6ac65a",
    "cruiseSpeed": 325,
    "engine": "SingleTurboprop",
    "fboId": "55a74297e4b07e03cc6ac65e",
    "fboOwner": "WinnerAviation",
    "Images": [
      "http: //seattleclouds.com/myapplications/daly365/AircraftGuide/EpicLT.jpg",
      "http: //www.flightglobal.com/assets/getasset.aspx?itemid=40851"
    ],
    "Type": "EpicLT",
    "maxRange": 1625,
    "seatCount": 6,
    "features": [
      "champagne",
      "fullystockedbar",
      "surroundsound",
      "wifi"
    ],
    "maxCruiseAltitude": 28000
  },
  "success": true,
  "error": ""
}
```
Read a planes information by ID

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | true | the plane id

## Create

```json
{
  "function": "plane.create",
  "params": {
    "type": "Epic LT",
    "fboOwner": "Winner Aviation V2",
    "fboId": "55c3f54eb8cff9160863a109",
    "Images": [
      "http://seattleclouds.com/myapplications/daly365/AircraftGuide/EpicLT.jpg",
      "http://www.flightglobal.com/assets/getasset.aspx?itemid=40851"
    ],
    "seatCount": 10,
    "engine": "Single Turboprop",
    "cruiseSpeed": 305,
    "maxRange": 1725,
    "maxCruiseAltitude": 29000,
    "features": []
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "error": "",
  "id": "55c3fa78b8cff91d4c590760",
  "success": true
}
```
Create a new plane

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
type | true | the plane type
fboId | true | the plane's fbo owner id
seatCount | true | the seat count
engine | true | the engine type
cruiseSpeed | true | the cruise speed
maxRange | true | the plane's max range
maxCruiseAltitude | true | the plane's max cruise altitude
*images | false | the plane's images url
*features | false | the plane's features
				   
## Update

```json
{
  "function": "plane.update",
  "params": {
    "id": "55c3fa78b8cff91d4c590760",
    "type": "Epic LT 2",
    "fboOwner": "Winner Aviation V3",
    "fboId": "55c3f54eb8cff9160863a109",
    "Images": [
      "http://seattleclouds.com/myapplications/daly365/AircraftGuide/EpicLT.jpg",
      "http://www.flightglobal.com/assets/getasset.aspx?itemid=40851"
    ],
    "seatCount": 12,
    "engine": "Double Turboprop",
    "cruiseSpeed": 315,
    "maxRange": 1725,
    "maxCruiseAltitude": 29000,
    "features": []
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "error": "",
  "id": "55c3fa78b8cff91d4c590760",
  "success": true
}
```
Update a plane

### Query Parameters
	
Parameter | Default | Description
--------- | ------- | -----------
id | true | the plane's id to update
type | true | the plane type
fboId | true | the plane's fbo owner id
seatCount | true | the seat count
engine | true | the engine type
cruiseSpeed | true | the cruise speed
maxRange | true | the plane's max range
maxCruiseAltitude | true | the plane's max cruise altitude
*images | false | the plane's images url
*features | false | the plane's features
				   	
## Delete

```json
{
  "function": "plane.delete",
  "params": {
    "id": "55c3fa78b8cff91d4c590760"
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "error": ""
}
```
Delete a plane by ID
	
### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | true | the plane id	
