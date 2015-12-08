# Common SMS Gateway documentation 

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/Overview.md) - [Previous section](/sections/About.md) - [Next section](/sections/Interfaces-general.md)

This section describes all relevant parameters used in the Intelecom SMS Gateway and which is common for all different interfaces. 

## Parameters for MT (outgoing) SMS messages

The following lists of parameters are used when sending messages in either of our available protocols. In its simplest form an outgoing message can consist of the common parameters, and at least one message object (basic message parameters) without any settings. 

### Common parameters

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th><th>Mandatory</th></tr>	
<tr><td>serviceid</td><td>Integer</td><td>Identifies the service. Provided by Intelecom.</td><td>Yes</td></tr>	
<tr><td>username</td><td>String</td><td>For authentication. Provided by Intelecom.</td><td>Yes</td></tr>		
<tr><td>password</td><td>String</td><td>For authentication. Provided by Intelecom.</td><td>Yes</td></tr>
<tr><td>batchReference</td><td>String</td><td>Reference ID that will be returned in the response.</td><td>No</td></tr>	
<tr><td>message</td><td>List of composite objects</td><td>At least one message.</td><td>Yes</td></tr>	
</table>

### Basic message parameters

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th><th>Mandatory</th></tr>	
<tr><td>recipient</td><td>String</td><td>The MSISDN of the recipient. The format should follow the ITU-T E.164 standard with a + prefix. Example: +4792000001.<br/>
<b>Note:</b> This must be a valid MSISDN, meaning <u>mobile phone number</u>. E.g. for Norway these numbers start with 4, 9, 58 or 59.</td><td>Yes</td></tr>	
<tr><td>content</td><td>String</td><td>The message payload to send, typically the message text. Read <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#message-content">here</a> for more details.</td><td>Yes</td></tr>		
<tr><td>price</td><td>Integer</td><td>The cost for the recipient to receive the message. In lowest monetary unit. See <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#pricing---non-premium-and-premium-messages-cpa--gas">here</a> for more details.<br/>
Example value: 200 = 2,- NOK
</td><td>No</td></tr>
<tr><td>clientReference</td><td>String</td><td>Arbitrary client reference ID that will be returned in the message response.</td><td>No</td></tr>	
<tr><td>settings</td><td>Composite object</td><td>For message settings, see below</td><td>No</td></tr>	
</table>

### Message settings parameters

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th><th>Mandatory</th></tr>	
<tr><td>priority</td><td>Integer</td><td>Used to prioritize between messages sent from the same service.<br/>
<ol>
<li>low (slower)</li>
<li>medium</li>
<li>high (faster)</li>
</ol>
Example: 2<br/><br/>Uses value from service configuration unless specified. 
</td><td>No</td></tr>	
<tr><td>validity</td><td>Integer</td><td>Specifies the TTL (time to live) for the message, i.e. how long before the message times out in cases where it cannot be delivered to a handset. See table <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#validity-period">here</a> for valid values.<br/><br/>
Example: 173
</td><td>No</td></tr>		
<tr><td>differentiator</td><td>String</td><td>Arbitrary string defined by the client to enable grouping messages in certain statistic reports.<br/><br/>
Example: OTP message
</td><td>No</td></tr>
<tr><td>invoiceNode</td><td>String</td><td>Arbitrary string defined by the client to enable grouping messages on the service invoice from Intelecom to the client.<br/><br/>
Example: marketing_dept
</td><td>No</td></tr>	
<tr><td>age</td><td>Integer</td><td>Only relevant for premium rate messages.<br/>
Defines an age limit for message content. The mobile network operators enforces this.<br/><br/>
IMPORTANT: If the service is a subscription service all premium rate messages must have age set to 18. <br/><br/>Valid values are:<br/>
<ul>
<li>0</li>
<li>16</li>
<li>18</li>
</ul>
Example: 18
</td><td>No</td></tr>	
<tr><td>newSession</td><td>Boolean</td><td>Used to start a new session. Read <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#sessions">here</a> for more information.<br/><br/>
Example: true
</td><td>No</td></tr>
<tr><td>sessionId</td><td>String</td><td>Used to continue an existing session. Read <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#sessions">here</a> for more information.<br/><br/>
Example: 01bxmt7f8b8h3zkwe2vg
</td><td>No</td></tr>
<tr><td>autoDetectEncoding</td><td>Boolean</td><td>Currently not in use. Default value is false.<br/><br/>
Example: true
</td><td>No</td></tr>
<tr><td>safeRemoveNonGsmCharacters</td><td>Boolean</td><td>If set to true the SMSGW will remove or safely substitute invalid characters in the message content instead of rejecting the message. See <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#message-content">here</a> for more information. Default value is false.<br/><br/>
Example: true
</td><td>No</td></tr>
<tr><td>originatorSettings</td><td>Composite object</td><td>Used to specify the originator. See description below.<br/><br/>
Uses values from service configuration unless specified.
</td><td>No</td></tr>
<tr><td>originatorSettings</td><td>Composite object</td><td>Used to specify the originator. See description below.<br/><br/>
Uses values from service configuration unless specified.
</td><td>No</td></tr>
<tr><td>gasSettings</td><td>Composite object</td><td>Used if the message is a premium SMS transaction. See description below<br/><br/>
Uses values from service configuration unless specified.
</td><td>No</td></tr>
<tr><td>sendWindow</td><td>Composite object</td><td>Used if the message should be queued and sent in the future instead of immediately. See description below<br/><br/>
Sends immediately unless specified.
</td><td>No</td></tr>
<tr><td>parameter</td><td>Composite object</td><td>Used to specify special settings including settings for binary message.
</td><td>No</td></tr>
</table>

### Originator settings

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th><th>Mandatory</th></tr>	
<tr><td>originatorType</td><td>String</td><td>Specifies the type of originator. See <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#message-originator">this section</a> for more information. <br/><br/>
Valid values are:
<ul>
<li>INTERNATIONAL</li>
<li>ALPHANUMERIC</li>
<li>NETWORK</li></td><td>Yes</td></tr>	
<tr><td>originator</td><td>String</td><td>Value depends on the originatorType. <br/><br/>
Example: +4799999999, Intelecom, 1960
</td><td>Yes</td></tr>		
</table> 

### GAS settings
<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th><th>Mandatory</th></tr>	
<tr><td>serviceCode</td><td>String</td><td>Identifier for the category of Goods and services. See <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#pricing---non-premium-and-premium-messages-cpa--gas">this section</a> for more information.<br/><br/> See list of valid servicecodes for valid parameter values for service codes.<br/><br/>
Example: 05008</td><td>Yes</td></tr>	
<tr><td>description</td><td>String</td><td>Further details of the Goods and services. The description may occur on the end-user invoice (together with category) for certain Mobile Network Operators.
 <br/><br/>
Example: Aftenposten
</td><td>No</td></tr>		
</table> 

### Send Window

See <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#send-window">this section</a> for more information about send window.<br/>

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th><th>Mandatory</th></tr>	
<tr><td>startDate</td><td>Date, CCYY-MM-DD[Z|(+|-)hh:mm]</td><td>
The date to send the message. <br/><br/>
Example: 2013-12-24</td><td>Yes</td></tr>	
<tr><td>stopDate</td><td>Date, CCYY-MM-DD[Z|(+|-)hh:mm]</td><td>The date to stop sending messages, if messages still are enqueued. <br/><br/>
Example: 2013-12-25
</td><td>No</td></tr>		
<tr><td>startTime</td><td>Time, hh:mm:ss[Z|(+|-)hh:mm]</td><td>
The time of day to start sending the messages.<br/><br/>
Example: 12:00:00, 12:00:00Z, 12:00:00+02:00</td><td>Yes</td></tr>	
<tr><td>stopTime</td><td>Time, hh:mm:ss[Z|(+|-)hh:mm]</td><td>The time to stop sending messages, if messages still are enqueued.<br/><br/>
Example: 12:00:00, 12:00:00Z, 12:00:00+02:00
</td><td>No</td></tr>	
</table> 

### Parameters

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th><th>Mandatory</th></tr>	
<tr><td>key</td><td>String</td><td>
Parameter key, see valid values below.<br/><br/>
Example: dcs</td><td>Yes</td></tr>	
<tr><td>value</td><td>String</td><td>The actual value to use with the chosen key. See description for each key below.<br/><br/>
Example: F5
</td><td>Yes</td></tr>		
</table> 

#### List of valid parameters (key / value)

<table>
<tr><th>Key</th><th>Data Type</th><th>Description</th></tr>	
<tr><td>businessModel</td><td>String</td><td>
May be used to specify operator specific business models..<br/><br/>
Example: productA</td></tr>	
<tr><td>dcs</td><td>One octet (2 hex digits)</td><td>Data Coding Scheme for message<br/><br/>

Specifies what data coding scheme is used for this message. This feature is defined in 3GPP TS 23.038 ch. 4.<br/><br/>

Should be one octet (2 hex digits). For example '15' or 'F5'.<br/><br/>
Example: F5
</td></tr>
<tr><td>udh</td><td>String (hex octets)</td><td>User Data Header<br/><br>

If non-empty will set the TP-User Data Header Indicator (UDHI) for the message.<br/><br/>

Defined in 3GPP TS 23.040 ch. 9.2.3.24 TP-User Data (TP-UD).<br/><br/>

Example: 0B0504158200000023AB0201
</td></tr>	
<tr><td>pid</td><td>Integer</td><td>Protocol Identifier – replace short message feature<br/><br>

A message containing a PID will replace an existing message having the same PID. Valid values are 65 – 71.<br/><br/>
<b>Note:</b> It will only be replaced if the service center address and originating address match the previous message. <br/><br/>

Also note that this functionality is only guaranteed to work for messages that are free of charge to receive for the end user. Many MNOs does not allow this setting for premium SMS. 
</td></tr>	
<tr><td>flash</td><td>Integer</td><td>Valid values: True (case-insensitive) - All other values, or if omitted means false.<br/><br>

A flash SMS is a type of text message that - without user action - appears directly and fullscreen on the the mobile phone. Some terminals will allow you to store this message, other will not. <br/><br/>
This functionality may be useful in case of emergencies or if you want to send confidential information, such as a One Time Password. Note that these messages often are not displayed on lock screens if the phone OS do not already display messages on lockscreen as default (such as iOS).<br/><br/>

Also note that this functionality is only guaranteed to work for messages that are free of charge to receive for the end user. Many MNOs does not allow this setting for premium SMS. 
</td></tr>		
</table> 

## Response parameters

All interfaces except SMTP will return a synchronous response with at least the fields for status code, status message and message identifier populated per message. All available fields in the response are described in the tables below.

### Message Response
<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th></tr>	
<tr><td>batchReference</td><td>String</td><td>
Reference ID for the request. Either the value provided by the client in the request or an automatically generated ID if no such value is set.</td></tr>	
<tr><td>messageStatus</td><td>List of composite objects</td><td>At least one element of messageStatus objects. See below.
</td></tr>		
</table>

### Message Status
<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th></tr>	
<tr><td>statuscode</td><td>Integer</td><td>
<table>
<tr><th>Statuscode</th><th>Value</th><th>Description</th></tr>	
<tr><td>MESSAGE_DELIVERED_OK</td><td>1</td><td>OK</td></tr>	
<tr><td>ACCESS_ERROR</td><td>2</td><td>No access. Authentication failed.</td></tr>	
<tr><td>ILLEGAL_ACTION</td><td>3</td><td>An illegal operation was tried.</td></tr>	
<tr><td>ILLEGAL_SERVICE</td><td>4</td><td>An illegal service was tried.</td></tr>	
<tr><td>SYNTAX_ERROR</td><td>5</td><td>The request contained syntax errors.</td></tr>
<tr><td>INTERNAL_ERROR</td><td>6</td><td>The request contained syntax errors.</td></tr>
</table></td></tr>
<tr><td>statusmessage</td><td>String</td><td>Textual information about status, e.g. which parameter failed
</td></tr>		
<tr><td>clientReference</td><td>String</td><td>The client reference ID if specified in the request
</td></tr>	
<tr><td>recipient</td><td>String</td><td>The recipient of the SMS message (MSISDN).<br/><br/> 
<b>Note:</b> The SMS gateway runs all numbers through a number parser and so the recipient in the response may be in same format than in the request, i.e. “+47 41 00 00 00” will be “+4741000000” in the response. Use the clientReference if you need to match messages in the request and response.
</td></tr>
<tr><td>messageId</td><td>String</td><td>Message ID (used as reference for delivery reports).
</td></tr>	
<tr><td>sessionId</td><td>String</td><td>Sessionid for a session, see <a href="https://github.com/Intelecom/sms/blob/master/sections/About.md#sessions">here</a> for more information. Only returned if newSession parameter is set to true, or if a sessionid was specified.
<tr><td>sequenceIndex</td><td>Integer</td><td>The messages in the response will always be in the same order as in the request. The sequence index is a convenience counter starting at 1.</td></tr>	
</table>  
<br/>

## Receiving messages using the SMS Gateway (MO SMS)

If you want to enable end users to send SMS messages to your solution you will need to set up a service able of receiving HTTP GET requests or HTTP POST requests through a REST API with either JSON or XML formatting. Whilst the HTTP GET API will one request for each message, the REST API will accumulate batches of messages and only send 1 request per second.

The SMSGW will invoke your HTTP service when MO- and DR-messages are slated for delivery to your server. The URL of your service must be provided to Intelecom Interactive Service Desk ([support.interactive@intele.com](mailto:support.interactive@intele.com)) for proper configuration of the service. You also need to provide information about which API you prefer for incoming (MO) messages. (HTTP GET, HTTP POST with JSON or HTTP POST with XML).

### Parameters for incoming (MO) messages

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th></tr>	
<tr><td>messageid</td><td>String</td><td>Unique messageid generated by the SMS platform for this message.</td></tr>
<tr><td>sno</td><td>String</td><td>The shortnumber associated with this message (e.g. 1960).
</td></tr>		
<tr><td>command</td><td>String</td><td>Also known as keyword. The pattern that causing the routing to the service. Usually a keyword e.g. “TLF”
</td></tr>	
<tr><td>content</td><td>String</td><td>The content of the SMS message. For regular text SMS messages this is a plain text, for binary messages this will be hex content. 
</td></tr>
<tr><td>strippedcontent</td><td>String</td><td>Same as content, but <b>keyword</b> is stripped from beginning of content.
</td></tr>	
<tr><td>timestamp</td><td>Date - Format: yyyyMMdd HH:mm:ss</td><td>The time when the message entered the Intelecom SMS platform. 
<tr><td>sctimestamp</td><td>Date - Format: yyyyMMdd HH:mm:ss</td><td>Service Center time stamp represents the time the operator SMSC received the message.</td></tr>	
<tr><td>serviceid</td><td>Integer</td><td>The id of the Intelecom service that has been identified for this message.</td></tr>	
<tr><td>servicename</td><td>String</td><td>The name of the service as provisioned in Intelecom systems</td></tr>
<tr><td>originator</td><td>String</td><td>The originator / sender of the SMS message. MSISDN with country code (international formatting) - e.g. +4799999999 </td></tr>
<tr><td>mcc / mnc</td><td>Integer</td><td>Mobile Country Code / Mobile Network Code for this message:
<table>
<tr><th>MNO (Operator)</th><th>MCC</th><th>MNC</th></tr>	
<tr><td>Telenor</td><td>242</td><td>1</td></tr>
<tr><td>NetCom</td><td>242</td><td>2</td></tr>
<tr><td>Teletopia</td><td>242</td><td>3</td></tr>
<tr><td>Network Norway</td><td>242</td><td>5</td></tr>
<tr><td>Phonero (Previous Ventelo Customers)</td><td>242</td><td>7</td></tr>
<tr><td>TDC Norway</td><td>242</td><td>8</td></tr>
<tr><td>Tele2 Norway</td><td>240</td><td>7</td></tr>
</table>  </td></tr>
<tr><td>sessionid</td><td>String</td><td>This contains the session identifier that this message is a reply to, this parameter allows you to bind an outgoing and incoming message together. This field will be empty if the message does not belong to a session</td></tr>	
<tr><td>type</td><td>Integer</td><td>Always=1 (parameter used to distinguish between MO and DR). Note that this parameter is only available on the HTTP GET interface.</td></tr>
</table>  

### Response when receiving MO SMS messages from Intelecom

Your server must respond to the HTTP request with a HTTP 200 header response, any other response code will by default cause a retry of delivery.

If the gateway does not receive a HTTP 200 acknowledge it will try resending the message to the CP. The MessageId will be the same as the previous attempt. Normally the mo-request will wait 60 seconds for the HTTP 200 response. If your server does not respond within the time limit the message is marked as undelivered and the gateway will try to resend the message later. 

<b>IMPORTANT:</b> Respond as fast as possible on the request before you start doing heavy business logic. It is strongly recommended to use an asynchronous model where you acknowledge the message and add it to an internal queue for example database. Do not use a synchronous model where you do all the business logic and then send a response message. Our experience is that customers that fail to respond within the time limit of the request often experience that their messages are queued. This is because the system will use some of its resources to resubmit messages that your server has received earlier but failed to acknowledge. The higher the traffic peaks, the more significant this problem will be.

## Receiving SMS Delivery Reports

If you need to know whether a specific message is received by the end users handset or not you will need to implement a server side service able of receiving HTTP GET requests or HTTP POST requests through a REST API with either JSON or XML formatted content.
 
This is an asynchronous operation and you will need to implement a mechanism for storing messageid and/ or batchReference and / or clientReference from sent (MT) messages in order to associate an incoming delivery report to the correct MT message.

### Parameters for delivery reports (DR) 

<table>
<tr><th>Parameter Name</th><th>Data Type</th><th>Description</th></tr>	
<tr><td>customerbatchreference</td><td>String</td><td>The batchReference of the MT message. A system batch reference is generated if you do not specify one when sending the MT message.</td></tr>
<tr><td>customermessagereference</td><td>String</td><td>The clientReference you specified in the MT message. 
</td></tr>	
<tr><td>serviceid</td><td>Integer</td><td>The id of the Intelecom service that has been identified for this message.</td></tr>	
<tr><td>servicename</td><td>String</td><td>The name of the service as provisioned in Intelecom systems</td></tr>
<tr><td>mcc / mnc</td><td>Integer</td><td>Mobile Country Code / Mobile Network Code for this message:
<table>
<tr><th>MNO (Operator)</th><th>MCC</th><th>MNC</th></tr>	
<tr><td>Telenor</td><td>242</td><td>1</td></tr>
<tr><td>NetCom</td><td>242</td><td>2</td></tr>
<tr><td>Teletopia</td><td>242</td><td>3</td></tr>
<tr><td>Network Norway</td><td>242</td><td>5</td></tr>
<tr><td>Phonero (Previous Ventelo Customers)</td><td>242</td><td>7</td></tr>
<tr><td>TDC Norway</td><td>242</td><td>8</td></tr>
<tr><td>Tele2 Norway</td><td>240</td><td>7</td></tr>
</table></td></tr>	
<tr><td>statuscode</td><td>Integer</td><td><table>
<tr><th>Code</th><th>Description</th></tr>	
<tr><td>0</td><td>Operation successful.</td></tr>
<tr><td>350</td><td>Non-existing or invalid network provider</td></tr>
<tr><td>354</td><td>The account cannot send bulk messages</td></tr>
<tr><td>355</td><td>Missing or illegal tariff for account</td></tr>
<tr><td>360</td><td>Syntax error - as reported by MNO (operator)</td></tr>
<tr><td>361</td><td>Validity period expired (without recipient receiving the message)</td></tr>
<tr><td>362</td><td>The message timed out in SMSC (before recipient received message)</td></tr>
<tr><td>363</td><td>SMSC operation failed - Internal SMSC error or the message contains errors and the SMSC is unable to process the message.</td></tr>
<tr><td>370</td><td>Unspecified error</td></tr>
<tr><td>371</td><td>Transmit error - The message was cancelled due to transmit errors towards the SMSC.</td></tr>
<tr><td>380</td><td>Illegal login towards MNO (operator)</td></tr>
<tr><td>368</td><td>Not connected/not logged in to SMSC.</td></tr>
<tr><td>369</td><td>SMSC Specific error - An error condition occurred on the SMSC.</td></tr>
<tr><td>351</td><td>Unknown recipient number - Recipient unknown (do not belong to current network operator) or illegal recipient.</td></tr>
<tr><td>356</td><td>Customer temporary barred - Customer is barred for an unspecified for an unspecified amount of time</td></tr>
<tr><td>357</td><td>Customer permanently barred - Remove MSISDN from all subscription services</td></tr>
<tr><td>358</td><td>Subscription barred for overcharged messages - The subscriber has explicit chosen to be permanently barred from receiving premium rate messages. The recipient is only allowed to receive messages that are free of charge</td></tr>
<tr><td>359</td><td>Age limit exceeded - The subscriber is not old enough to receive a premium rate message. Should only occur when an ageLimit is set for a message</td></tr>
<tr><td>364</td><td>Subscription temporary not reachable - For some reason, the subscription number cannot be reached for the moment</td></tr>
<tr><td>390</td><td>The message was sent successfully, but not billed (either it was not supposed to, or billing failed)</td></tr>
<tr><td>385</td><td>Illegal function - The message is stopped because of trying to use a function that requires a special agreement</td></tr>
<tr><td>386</td><td>Message billed but not sent - The recipient did not receive the message, but was billed for the message</td></tr>
<tr><td>650</td><td>Database problems, error connecting to Database or other database related problems</td></tr>
<tr><td>652</td><td>Missing system data - Crucial system data not found cannot perform task without this data.</td></tr>
<tr><td>651</td><td>No route to subscriber found</td></tr>
<tr><td>653</td><td>Unknown unexpected data. Please see error message in the message object</td></tr>
<tr><td>654</td><td>Invalid MSISDN - MSISDN is not recognized as a valid number</td></tr>
<tr><td>655</td><td>Inactive service -  Service is no longer active, message discarded</td></tr>
</table> 
</td></tr>	
<tr><td>statusdescription</td><td>String</td><td>Brief description of the internal statuscode (primarily used for logging). 
</td></tr>
<tr><td>extstatuscode</td><td>String</td><td>External statuscode (from mobile network operator)
</td></tr>	
<tr><td>extstatusdescription</td><td>String</td><td>Brief description of the external statuscode (primarily used for logging).</td></tr>	
<tr><td>type</td><td>Integer</td><td>Always=6 (parameter used to distinguish between MO and DR). Note that this parameter is only available on the HTTP GET interface.</td></tr>	
</table> 

### Reponse when receiving DR - Delivery Reports from Intelecom

You must respond to the HTTP request with a HTTP 200 header response, otherwise any other header responses will cause a retry of delivery.
 