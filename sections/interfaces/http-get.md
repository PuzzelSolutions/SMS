# HTTP GET API

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/overview.md) - [Previous section](/sections/interfaces/soap.md) -  [Next section](/sections/interfaces/smtp.md)

This section describes how to integrate towards the Puzzel SMS Gateway HTTP(S) GET API. 

The content provider may invoke the SMS Gateway (SMSGW) using HTTP GET queries. Though not as flexible as its SOAP / REST counterparts, it is a very easy protocol to integrate with, and to send simple test messages from your browser for example. If you need to integrate a third party product to SMS, this protocol is often the only option. However, as mentioned earlier, we recommend that you integrate using the [REST API](/sections/interfaces/rest.md) if you have the possibility to do so. 

Also note that due to URL length limitations, this interface is not optimal for batch sending (many recipients in one request).

The HTTP(S) GET APIs support both sending SMS (MT), receiving SMS (MO) and delivery reports (DR). Please see [here](/sections/common.md) for information about the available message parameters.

## Encoding

The request URI must be percent encoded, following RFC2396 (“Uniform Resource Identifiers (URI): Generic Syntax”), and use UTF-8.
For example, a message with the content “Dette er en melding med ÆØÅ i seg” should be encoded as:

	Dette%20er%20en%20melding%20med%20%C3%A6%C3%B8%C3%A5%20i%20seg.

## Sending messages (MT)

### How to connect

The HTTP(S) GET Gateway is accepting GET requests on the URL:

	https://<server-url>/gw/rs/sendMessages?

### Parameters

Parameter names are case sensitive. For example for the Serviceid parameter, the correct spelling is “serviceId“. Incorrect examples are “serviceid”, “serviceID”, “SERVICEID”, “serViceID”, etc.

[Common parameters](/sections/common.md#common-parameters) do not need any prefix, e.g., “username” and “serviceId”.

A dot (“.”) notation is used to specify nested properties, such as message[0].settings.priority.

Similar to the other interfaces the HTTP(S) GET interface supports sending multiple messages. Message parameters must therefore be prefixed with message[n] (where n is a zero-based index for the message). The first message is therefore message[0]. For example to set the message content for the first message the query parameter key name would be message[0].content. Similarly, setting the recipient becomes message[0].recipient.


### Request examples

#### Simple message:

	https://<server-url>/gw/rs/sendMessages?serviceId=99999&message[0].recipient=%2B4799999999&message[0].content=Dette+er+en+ny+test.&username=test&password=test

*Note that +47 becomes %2B47 when URL encoded*

#### Message with originator settings:

	https://<server-url>/gw/rs/sendMessages?serviceId=999899&username=test&password=test&message[0].recipient=+4799999999&message[0].content=Test&message[0].settings.originatorSettings.originatorType=ALPHANUMERIC&message[0].settings.originatorSettings.originator=Puzzel
 
#### Message with PID parameter setting:

	https://<server-url>/gw/rs/sendMessages?serviceId=99999& username=test&password=test&message[0].recipient=%2B4799999999&message[0].content=Dette+er+en+ny+test.&message[0].settings.parameter[0].key=pid&message[0].settings.parameter[0].value=68

### Response example

The response format is of content-type "text/xml" and is the same as for the REST interface described [here](/sections/interfaces/rest.md#xml-response-example). 

## Receiving messages (MO)

If you want to enable end users to send SMS messages to your solution using HTTP(S) GET, you will need to set up a service able of receiving HTTP(S) GET requests. This API will send only one request for each message.

The SMSGW will invoke your HTTP service when MO messages are slated for delivery to your server. The URL of your service must be provided to Puzzel Service Desk ([help.puzzel.com](https://help.puzzel.com "Puzzel Help")) for proper configuration of the service. You also need to provide information that you want to use the HTTP(S) GET API method.

If you need to add a firewall rule, you can find the originating IP addresses on [this](https://help.puzzel.com/product-documents/technical-specs/basic-requirements) page. 

[ngrok](/references/ngrok.md) is a great tool to use when testing MO / DR messages locally. 

For description of incoming SMS (MO) parameters see [this section](/sections/common.md#parameters-for-incoming-mo-messages).

### MO SMS Example using HTTP(S) GET

	http://mogw.example.com/incomingaction?messageid=[messageid]&sno=[sno]&commandtype=[commandtype]&command=[command]&content=[content]&timestamp=[timestamp]&sctimestamp=[sctimestamp]&serviceid=[serviceid]&originator=[originator]&mcc=[mcc]&mnc=[mnc]&sessionid=[sessionId]&type=[type]&servicename=[servicename]

The attributes in the SMS-MO message will substitute the corresponding parts of the template.


## Receiving Delivery Report (DR) messages

If you need to know whether a specific message is received by the end user's handset or not, you will need to implement a server side service able of receiving HTTP(S) GET requests. 

This is an asynchronous operation and you will need to implement a mechanism for storing messageid and/ or batchReference and/ or clientReference from sent messages (MT) in order to associate an incoming delivery report (DR) to the correct MT message.

[ngrok](/references/ngrok.md) is a great tool to use when testing MO / DR messages locally. 

For description of delivery report parameters see [this section](/sections/common.md#parameters-for-delivery-reports-dr).

### DR SMS Example using HTTP(S) GET

	http://drgw.xx.no/reportaction?messageid=[messageid]&statuscode=[statuscode]&statusdescription=[statusdescription]&extstatuscode=[extstatuscode]&extstatusdescription=[extstatusdescription]&customerMessageReference=[customermessagereference]&customerBatchReference=[customerbatchreference]&serviceid=[serviceid]&servicename=[servicename]&mcc=[mcc]&mnc=[mnc]&type=[type]

The attributes in the SMS-DR message will substitute the corresponding parts of the template.

## HTTP response for incoming SMS (MO) and Delivery Report (DR) messages

The CP must respond to the HTTP request with a HTTP 200 header response. Any other header responses cause a retry of delivery.

This is the same as for the REST API, please see [this section](/sections/interfaces/rest.md#http-response-for-incoming-sms-mo-and-delivery-report-dr-messages) for more information.

