# SOAP API

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/Overview.md) - [Previous section](/sections/Interfaces/Rest.md) -  [Next section](/sections/Interfaces/HTTP_Get.md)

This section describes how to integrate towards the Intelecom SMS Gateway SOAP (web services) API. The SOAP API only support sending SMS (MT), meaning that receiving SMS (MO) and delivery reports (DR) will have to be implemented using protocols that support these message types such as HTTP GET or HTTP POST with JSON or XML. An overview over each protocols capabilities are shown [here](/sections/Interfaces-general.md) 

Please see [here](/sections/Common.md) for information about the available message parameters.

### How to connect

The web service interface is defined by the WSDL and can be retrieved from: 

	https://<server-url>/gw/ws/SMSGatewayV10?wsdl

### SOAP Request Example

	<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sms="http://chimera.intele.com/gw/wsdl/SMSGateway-v1.0" xmlns:ns="http://chimera.intele.com/gw/xsd/SMSGateway/Request/2013/02">
		<soapenv:Header/>
		<soapenv:Body>
			<sms:sendMessages>
				<ns:request>
					<serviceId>1000</serviceId>
					<username>intelecom</username>
					<password>xdyf3bf2</password>
					<message>
						<recipient>+4741000000</recipient>
						<content>This is a message from Intelecom.</content>
						<price>0</price>
						<settings>
						<originatorSettings>
								<originator>Intelecom</originator>
								<originatorType>Alphanumeric</originatorType>
							</originatorSettings>
						</settings>
					</message>
				</ns:request>
			</sms:sendMessages>
		</soapenv:Body>
	</soapenv:Envelope>
	
### SOAP Response Example

	<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
		<soap:Body>
			<ns3:sendMessagesResponse xmlns:ns2="http://chimera.intele.com/gw/xsd/SMSGateway/Request/2013/02" xmlns:ns3="http://chimera.intele.com/gw/wsdl/SMSGateway-v1.0" xmlns:ns4="http://chimera.intele.com/gw/xsd/SMSGateway/Response/2013/02">
				<ns4:response>
					<messageStatus>
						<statusCode>1</statusCode>
						<statusMessage>Message enqueued for sending</statusMessage>
						<recipient>+4741000000</recipient>
						<messageId>7a0081hfe800</messageId>
						<sequenceIndex>1</sequenceIndex>
					</messageStatus>
				</ns4:response>
			</ns3:sendMessagesResponse>
		</soap:Body>
	</soap:Envelope>
