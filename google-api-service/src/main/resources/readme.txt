
READ ME

This interface consumes the messages from the RabbitMq queue, and gets the values from db table to construct the url.
And converts this long url into the short url using the GoogleAPI URL shortener.

Technologies used : MULE3.8APIKIT, Maven, Munit, GoogleAPI, MySQL, RabbitMQ, Ehcaching

Rabbit mq details

http://localhost:15672/#/queues/%2F/toll_q

Input json

{
  "UUID": "1",
  "VRN": "EX54NSN",
  "CrossingDate":"2017-06-23T12:00"
}

Output Json

{
  "UUID": "1",
  "TollID": "b31a4e98-a373-43d1-b32f-7b6a03238adb",
  "VRN": "EX54NSN",
  "CrossingDate": "2017-06-23T12:00",
  "InboundQ": "toll_q",
  "JourneyDetails": {
    "longitude": "-0.139435",
    "latitude": "51.526972",
    "url": "https://goo.gl/XeJN1x"
  }
}


DB table 

DROP TABLE IF EXISTS `qe2`.`locations`;
CREATE TABLE  `qe2`.`locations` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `latitude` varchar(45) NOT NULL DEFAULT '',
  `longitude` varchar(45) NOT NULL DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=latin1;

==============
1. case 1


*******************************************************************************************************
*            - - + APPLICATION + - -            *       - - + DOMAIN + - -       * - - + STATUS + - - *
*******************************************************************************************************
* qe2                                           * default                        * DEPLOYED           *
* api-google-url                                * default                        * DEPLOYED           *
*******************************************************************************************************

INFO  2017-07-13 21:05:42,872 [[qe2].toll-dispatcherFlow.stage1.02] org.mule.api.processor.LoggerMessageProcessor: Message received from toll_q: {
  "UUID": "1",
  "VRN": "EX54NSN",
  "CrossingDate":"2017-06-23T12:00"
}
INFO  2017-07-13 21:05:45,394 [[qe2].QE2Service_HTTP_Listener.worker.01] com.mulesoft.weave.mule.utils.MuleWeaveFactory$: MimeType was not resolved '*/*' delegating to Java.
INFO  2017-07-13 21:05:46,468 [[api-google-url].api-httpListenerConfig.worker.01] org.mule.api.processor.LoggerMessageProcessor: outsideCache
WARN  2017-07-13 21:05:46,468 [[api-google-url].api-httpListenerConfig.worker.01] com.mulesoft.mule.cache.ObjectStoreCachingStrategy: Message will be processed without cache: payload is consumable
INFO  2017-07-13 21:05:46,468 [[api-google-url].api-httpListenerConfig.worker.01] org.mule.api.processor.LoggerMessageProcessor: insideCache
INFO  2017-07-13 21:05:47,089 [[api-google-url].api-httpListenerConfig.worker.01] org.mule.api.processor.LoggerMessageProcessor: {
 "kind": "urlshortener#url",
 "id": "https://goo.gl/XeJN1x",
 "longUrl": "https://maps.googleapis.com/maps/api/staticmap?zoom=16&size=600x300&maptype=roadmap&markers=color:purple|label:Car|51.526972,-0.139435"
}

INFO  2017-07-13 21:05:47,986 [[qe2].QE2Service_HTTP_Listener.worker.01] org.mule.api.processor.LoggerMessageProcessor: {
  "UUID": "1",
  "TollID": "b31a4e98-a373-43d1-b32f-7b6a03238adb",
  "VRN": "EX54NSN",
  "CrossingDate": "2017-06-23T12:00",
  "InboundQ": "toll_q",
  "JourneyDetails": {
    "longitude": "-0.139435",
    "latitude": "51.526972",
    "url": "https://goo.gl/XeJN1x"
  }
}
INFO  2017-07-13 21:05:47,986 [[qe2].QE2Service_HTTP_Listener.worker.01] org.mule.api.processor.LoggerMessageProcessor: <?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://www.w3.org/2003/05/soap-envelope"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	<SOAP-ENV:Body>
		<qe:TollResponse xmlns:qe="urn:qe.2.com">
			<TollResult>ACK</TollResult>
		</qe:TollResponse>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>

