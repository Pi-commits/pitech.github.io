---
layout: post
title: "Uber"
description: "Includes HLD + LLD + DB Schema + Requests"
comments: true
keywords: "uber, system design"
date: 2023-09-19 23:41:00 +05:30
tags: SystemDesign 
---

### Requirements

#### Functional Requirements

We will design our system for two types of users: Customers and Drivers.

##### Customers

1. Customers should be able to see all the cabs in the vicinity with an ETA and pricing information.
2. Customers should be able to book a cab to a destination.
3. Customers should be able to see the location of the driver.
4. Customers should be able to see the ride history.
5. Customers should be able to add stops 

##### Drivers

1. Drivers should be able to accept or deny the customer-requested ride.
2. Once a driver accepts the ride, they should see the pickup location of the customer.
3. Drivers should be able to mark the trip as complete on reaching the destination.
4. Drivers should be able to see their ride history without showing the customers personal information. 


#### Non-Functional requirements
1. High reliability.
2. High availability with minimal latency.
3. The system should be scalable and efficient.

#### Extended requirements

1. Drivers are to be assigned based on location and availability
2. Customers can rate the trip after it's completed.
3. Payment processing.
4. Metrics and analytics.

<div class="divider"></div>

### Estimation and Constraints (Based on assumptions)

#### Traffic

Daily Active Users (DAU): **100 million**  
Drivers Count: **1 million**  
Daily Rides: **10 million**  
On average each user performs 10 actions: **100 million X 10 = 1 billion requests/day** =~ **12k Requests/second**  

#### Storage

Each message takes **400 Bytes**  
Per Day: **1 billion×400 bytes=∼400 GB/day**  
10 Years: **400 GB×10 years×365 days=∼1.4 PB**  

#### Bandwidth

As our system is handling 400 GB of ingress every day, we will require a minimum bandwidth of around 4 MB per second.  

400/(24\*60\*60) =∼5 MB/second  

#### High-level estimate

| Type                       | Estimate        | 
| -------------------------- |:---------------:|
|Daily active users (DAU)    |	100 million    |
|Requests per second (RPS)	 |  12K/s          |
|Storage (per day)           |	~400 GB        |
|Storage (10 years)			 |  ~1.4 PB        |
|Bandwidth					 | ~5 MB/s         |

<div class="divider"></div>

### Data model design

<img src="./assets/images/uber-database.jpg" alt="" />

<div class="divider"></div>

### API Design

Basic API design for our services:<br/>

#### Request a Ride
Through this API, customers will be able to request a ride.<br/>
Request<br/>
```requestRide(customerID: UUID, source: Tuple<float>, destination: Tuple<float>, cabType: Enum<string>, paymentMethod: Enum<string>) ```

Response<br/>
```

{
	RideDetails: {},
	status: <enum> ('timeout', '')
	message: <string>
}

```


#### Cancel the Ride
This API will allow customers to cancel the ride.<br/>
Request<br/>
```cancelRide(customerID: UUID, reason?: string): boolean```

Response<br/>
```Result (boolean): Represents whether the operation was successful or not.```

#### Accept or Deny the Ride
This API will allow the driver to accept or deny the trip.<br/>
Request<br/>
```
acceptRide(driverID: UUID, rideID: UUID): boolean
denyRide(driverID: UUID, rideID: UUID): boolean`
```

Response<br/>
```Result (boolean): Represents whether the operation was successful or not.```

#### Start or End the Trip
Using this API, a driver will be able to start and end the trip.<br/>
Request<br/>
```
startTrip(driverID: UUID, tripID: UUID): boolean
endTrip(driverID: UUID, tripID: UUID): boolean
```

Response<br/>
```Result (boolean): Represents whether the operation was successful or not.```

#### Rate the Trip
This API will enable customers to rate the trip.<br/>

Request<br/>
```rateTrip(customerID: UUID, tripID: UUID, rating: int, feedback?: string): boolean```

Response<br/>
```Result (boolean): Represents whether the operation was successful or not.```



 




