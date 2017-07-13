# GoogleAPIIntegrationUsingMule
This interface consumes the messages from the RabbitMq queue, and gets the values from db table to construct the url. And converts this long url into the short url using the GoogleAPI URL shortener.  Technologies used : MULE3.8APIKIT, Maven, Munit, GoogleAPI, MySQL, RabbitMQ, Ehcaching


--------------
Demo for integrating the Google API


This project 
---------
consumes the messages from the RabbitMq queue, and gets the values from db table to construct the url.
And converts this long url into the short url using the GoogleAPI URL shortener.


Mule components
---------
1.	Dataweave
2.  	APIKIT router
3.	Context property place folders
4.	AMQP {Rabbit MQ}
5.	Ehcache
6.	DB connector
7.	Object-to-string-transformer
8.	Http post
9.	Parse template
10.  	Exception Strategies



To Trigger the execution
-------
Publish the message in the RabbitMQ 
{
  "UUID": "1",
  "VRN": "EX54NSN",
  "CrossingDate":"2017-06-23T12:00"
}

Technologies
---------
- J2E
- MySQL
- MULE ESB 3.8{APIKIT}
- Munit
- Maven
- Google API
- RabbitMQ

