# TCP Socket / XML API

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/overview.md) - [Previous section](/sections/interfaces/smtp.md) -  [Next section](/sections/interfaces/smpp.md)

TCP provides a reliable point-to-point communication channel that client-server applications on the Internet can use to communicate with each other. To communicate over TCP, a client program and a server program establish a connection. Each program binds a socket to its end of the connection. To communicate, the client and the server each reads from and writes to the socket bound to the connection.

### How to connect

A socket is one end-point of a two-way communication link between two programs running on the network. In order to integrate towards this service you will need to implement a socket client that connects to one of our SMS socket servers at the following addresses and ports:

	Primary: [server adress] - port [server port]
	Backup:  [server adress] - port [server port]


If there is no activity on an established connection for a certain time interval (default = 1 minute) it will close automatically. The client will then need to establish a new connection.

###	Sending and receiving messages

When a connection is established between the client and the server, the server will wait for the client to send a request. The request must be XML and formatted according to the correct schema, and the encoding used must be UTF-8. The server will parse the request and send a response to the client. The client should always wait for a response before sending another request.

Delivery Reports are not returned over TCP in this mode, but may be configured to be sent asynchronously to a your endpoint over a HTTP(S) connection using GET or POST.

It is recommended that each request should contain no more than 1000 messages. If you need to send a larger batch, it should be split into several XML requests.

###	XML Request Example

	<?xml version="1.0"?>
	<req:request xmlns:req="http://chimera.intele.com/gw/xsd/SMSGateway/Request/2013/02">
	  <serviceId>29</serviceId>
	  <username>gre</username>
	  <password>erg</password>
	  <message>
	    <recipient>+4741414141</recipient>
	    <content>test</content>
	    <price>0</price>
	    <settings>
	      <sendWindow>
	        <startDate>2015-06-15+01:00</startDate>
	        <startTime>16:15:00</startTime>
	      </sendWindow>
	     </settings>
	   </message>
	</req:request>

###	XML Response Example

	<?xml version="1.0"?>
	<rsl:result 	xmlns:rsl=http://chimera.intele.com/gw/xsd/TCPGateway/Result/2015/10
		   	xmlns:sms=http://chimera.intele.com/gw/xsd/SMSGateway/Response/2013/02
			xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
		<status>
			<code>1</code>
			<description>OK</description>
		</status>
		<sms:response>
			<batchReference>0c2c002f-ccc6-4c7b-86e1-c7871b1c98b3</batchReference>
			<messageStatus>
				<statusCode>1</statusCode>
				<statusMessage>Message enqueued for sending</statusMessage>
				<clientReference>SMS-AFFS-000000100</clientReference>
				<recipient>+4741915590</recipient>
				<messageId>6y06b02hdo00</messageId>
				<sequenceIndex>1</sequenceIndex>
			</messageStatus>
		</sms:response>
	</rsl:result>

For a list of possible status codes, see [here](/sections/common.md#response-parameters).

