# About A2P SMS and SMS Gateways

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/overview.md) - [Previous section](/sections/overview.md) -  [Next section](/sections/common.md)

SMS is best known for P2P messaging where SMS messages are exchanged between two mobile phones. Chances are that you in the last couple of months also have recevied an SMS that was sent from a machine. This may be a confirmation of a taxi booking, a one-time password for access, or a notification of your next dentist appointment. If so, you have received an A2P SMS message. 

A2P SMS is when SMS messages are sent from an application, such as a CRM system, VPN pincode solution (OTP) or custom webpages _to_ a mobile phone. This is also often named MT (_Mobile_ _Terminated_) SMS messages. Messages may also be sent _from_ the mobile phone to an application, something that is called P2A messages, and also often named MO (_Mobile_ _originated_) messages.

Puzzel is an enabler of both A2P / P2A messaging - meaning that you can use our SMS Gateway API to "SMS enable" your applications and systems. 

The chapters below will introduce you to common terms and possibilites for an A2P / P2A solution. 

### SMS integration overview abc

To send SMS messages you will need to integrate with one of the APIs described below and in more detail in later sections. 

The parameters are common for the SOAP, HTTP GET and REST APIs and divided into three groups: common parameters, basic message parameters and message settings parameters. The message settings parameters are optional, if you do not have any special need for custom settings you can ignore these. In the current version of SMSGW, not all parameters are available for SMTP (email) and SMPP methods.

The available APIs for sending SMS messages are:

- SOAP Webservices
- REST services – XML or JSON using HTTP POST
- HTTP GET (with limited functionality)
- SMTP (email – with limited functionality)
- SMPP

By using the SOAP and REST interfaces, it is possible to send several messages in one batch. This can be messages to different recipients and with different price and content. All interfaces except SMTP will synchronously return a status code and message identifier, which is a unique identifier for each message in the Puzzel platform. The status code will give information about whether the messages were added to the internal queue in the Puzzel system or not. The status code will not give information about whether the message was received on the end user's handset or not. In order to check for this, you need to utilize the delivery report mechanism as described in a later section. 

### Pricing - Non-premium and premium messages (CPA / GAS)

When sending messages there are some alternatives concerning pricing of the messages. The messages may be sent to the end users free of charge, meaning that the end user will not have to pay to receive your message. Your company typically pays for this message. 

The other alternative is that the end user pays a price for receiving the message; paid for on the end user’s phone bill. Often called premium messages, you may use these for billing purposes such as paying for digital content or services. Premium messages are not available in all countries; please contact your customer representative for more information. 

In Norway, the supported premium rates are from 1,- to 1000,- in steps of 1 NOK. The price parameter uses the lowest monetary unit available, for example in order to send to Norwegian recipients, Norwegian “øre” is used. 

Example: To send a billing message with a price of 2 NOK to a Norwegian recipient, set the price parameter to the value of 200. 

In some countries, there are also different business models depending on what product you are charging for.These business models decide the divident of the payout, i.e. the operator's cut. For example the business model "physical goods" have different payout than the business model "donation". Each service that is to use premium SMS also needs to be approved to use a given business model by the Mobile Network Operators. The business model is set by specifying a service code and category as defined by the mobile network operators for each message.  You can find the listing of the Mobile Network Operator service codes [here](/references/servicecodes.md). 

### Message Originator

When sending SMS messages, it is possible to specify the originator of the messages that is shown on the end users' handsets when receiving the message. Three different types of originator settings exist:

- International Number – if the originator is to be an international phone number, in E164 format e.g. +4799999999
- Alphanumeric Text – if the originator is to be alphanumeric text, for example “Puzzel”. The max length of an alphanumeric originator is 11 characters and only a-z, 0-9 and the chars ‘ ‘ (space), '%', '&', '-', '+', '.' , ',' may be used as content.
- Network specific – if the originator is to be short number, e.g. 1960.

You must set the correct originator and originatortype parameter values if you want to override the default originator for your service. For example, if you want the originator to be ‘Puzzel’, you need to set the originator parameter to “Puzzel” and the originatortype parameter to “ALPHANUMERIC”.

Note that is not possible for an end user to reply to a message sent with alphanumeric originator. Some phones may be able to reply to alphanumeric originators if you set alphanumeric originator with only numbers in the content parameter. As not all phones will accept this, we recommend that you use the types for international or national numbers if you are to send a numeric string as originator.

Also note that it is only possible to specify originator for messages that are received by the end user free of charge (price = 0). The reason for this, is that it needs to be easy to identify who sent specific billing messages to an end user. 

Our experience is that some operators outside of Scandinavia have problems delivering messages with alphanumeric originator. If you are developing a global service you should consider using an international number as originator instead of alphanumeric. 

### Validity Period

It is possible to define the validity period of each message when sending SMS messages. The validity period is the period of time that delivery attempts occur for a SMS message. Meaning that if you specify a validity time of 5 minutes, the Puzzel platform and the Mobile Network Operators will try to deliver the message for 5 minutes using the respective retry schemes. If the message cannot be delivered to the handset in this timeframe (handset turned off etc.), the message is discarded, resulting in a delivery report with a timeout status. This feature is handy if you have messages that only are valid for a certain period of time, such as one-time passwords or special offers with a time limitation. When specifying the validity parameter, please refer to the table below:


<table>
<tr><th>Value</th><th>Validity period</th></tr>	
<tr><td>0 to 143</td><td>(Value + 1) x 5 minutes</td></tr>	
<tr><td>144 to 167</td><td>12h + (Value-143) x 30 minutes</td></tr>	
<tr><td>168 to 173</td><td>(Value-166) x 1 day</td></tr>	
</table>

### Message Content

You can specify the content of the SMS message by using the “content” parameter. The Data Coding Scheme (DCS) specifies how the content is encoded. Three encodings are supported:
<ul>
  <li>GSM 7-bit</li>
  <li>Data (8-bit) (rarely used)</li>
  <li>UCS-2 (UTF-16)</li>
</li>

#### GSM 7-bit
The max length of a single message is 160 characters. If you provide text that is longer than 160 characters, the SMSGW will automatically split the message into concatenated text messages. When SMS messages are concatenated, some of the SMS payload is needed for the UDH, resulting in the max message length for each concatenated message being 153 characters. The Puzzel platform allows a maximum of six concatenated messages, meaning that the maximum character length of the content field is 918 characters (153 x 6). The GSM specification allows for a much higher number of concatenated messages, but because of restrictions in some of the MNO SMSC's, the max limit of six concatenated messages had to be included.

##### Valid characters
SMS default encoding uses 7 bits to handle a character. The GSM 03.38 specification defines the valid character sets, this being the “Basic Character Set” and the corresponding extension table as depicted below:

<p align="center">
<img src="http://i.imgur.com/Otl1whV.png">
</p>

If you use characters from the extension table, for example the EUR character (€), an escape character is needed in addition to the character from the extension table. This means that the EUR character counts as two characters and you will have less space available in the message.

#### Data (8-bit)
Data encoding is used for binary messages and is used in some Machine-2-Machine (M2M) communication use cases. You must set an appropriate Data Coding Scheme (DCS) parameter to use this encoding.

#### UCS-2 (UTF-16)
The GSM 7-bit character set is fairly limited. UCS-2 makes it possible to send emojis and other symbols. However, a single message encoded with UCS-2 can maximum fit 70 characters (notice that some UCS-2 symbols, especially emojis, use multiple code points. A 🍉 (watermelon) consumes 2 characters (2*16 bit = 32 bit). In addition such a character cannot be split between multiple messages which further reduces the maximum amount of characters per message.

UCS-2 is used preferably by setting the parsing type to 'AUTO_DETECT'. Optionally it can also be enabled by setting the DCS parameter.

#### Invalid characters
If the content payload contains characters that are not valid the default behaviour of the gateway is to return an error code and not send the message. This means that the customer should verify the message content before it is sent.
This behaviour can be customized for each service. Currently we offer these parsing types:
<table>
<tr><th>Type</th><th>Description</th></tr>	
<tr><td>None</td><td>This is the default behaviour. Any invalid characters will lead to an error and the message will not be sent.</td></tr>	
<tr><td>Remove characters</td><td>Any invalid characters will be removed and the message will be sent. E.g. "Testing: Клавдии áàóòúù" will result in "Testing àòù"</td></tr>	
<tr><td>Replace characters</td><td>Any invalid characters will be replaced or removed and the message will be sent. Characters that will be replaced are "accented" characters, e.g. "Testing Клавдии áàóòúù " will result in "Testing aàoòuù".</td></tr>
</table>
You can contact Puzzel to select a specific parsing type for your service. Parsing type can also be set for each message with the <a href="https://github.com/Intelecom/sms/blob/master/sections/common.md#parameters">parsing-type parameter.</a>

### Sessions

The Puzzel SMS platform has introduced a session mechanism that allows for two-way dialog between a system and end-user without the need for keywords. Keywords in SMS are short text identifiers for services on a shared short number. 

Example using sessions: To order weather information on the short code 1881 you can send “WEATHER OSLO”. In this example “WEATHER” is the keyword identifying the service, whilst “OSLO” is a parameter. Using keywords to have a SMS dialog with an end user is not a very user-friendly solution as the end user will will have to provide the keyword before entering the text for each message. 

Example not using sessions: Your service desk needs to update email information for your customers. You want to send them a SMS message requiring them to reply to the SMS with their correct email address. 
The following is an illustration of the interaction without and with the use of session.

<p align="center">
<img src="http://i.imgur.com/w8M0rRh.png">
</p>


Using session, you can also continue a conversation by providing the unique sessionid as a parameter when sending a message, for example like this:
<p align="center">
<img src="http://i.imgur.com/ScggctX.png">
</p>

Currently the use of sessions is only available for Norwegian subscribers, meaning that you can only send messages with session to end users with Norwegian subscriptions. 

For the implementation of the session logic in Norway, we have utilized a feature from the Mobile Network Operators called subnumbering, also sometimes named recipient range routing. With this feature, a string of numbers uniquely identifying the session is added to the last part of the short number resulting in a fourteen-digit originator. 
As the identifier will be generated when sending the message, it is only possible to start a session with a message sent to the end user. 

There are two ways to access the session for MT messages: Request a new session, or reuse a previously used session. 

When using a session, the originatortype must be set to the value 3 (Network specific / short number). It is not possible to use alphanumeric or international number types as originator when using sessions. 
The synchronous response from the gateway will contain a session identifier, which must be stored in your system if you want to be able to identify the response from the end user when replying to the message. 

<p align="center">
<img src="http://i.imgur.com/rTyKf14.jpg">
</p>

#### Start a new session

Add the parameter newSession=true. This flag will tell the Gateway to start a session and you will receive a session identifier in the response. 

#### Continue a session

To continue an existing session, use the sessionid parameter in the request, by sending the session identifier returned in the response when you started a new session. A session expires by default after 14 days if no messages have been sent using the sessionid. But this period is prolonged as long as you keep sending messages with the same sessionid. If you want the expiration period shorter or longer than 14 days for your service, please do contact us, and we will set this up for you.

Note: If you want to continue the session do not set the new session flag. If you set both the new session flag and the sessionid, a new session will be generated.

### Send Window

You can schedule a message to be sent at some point in the future with the send window parameters.

The send window composite object consists of four parameters where the start date is the only mandatory field. The common use case is to set a start date and start time to indicate when the platform should send the message.

In the WSDL definition and in the XML Schemas, the dates and times are XSD Date and XSD Time data types. If you integrate without using a framework that formats these types automatically, or when using JSON or HTTP GET with query parameters, make sure to format these parameters correctly. The XSD Date and XSD Time types are based on a subset of the ISO 8601 standard. If no time zone is set it defaults to Central European Time (CET).

If a send window has a stop date set to a later date than the start date, the start time and stop time will be used for each of these dates. 

E.g., the following send window indicates that the messages can be sent on August 5 and August 6 between 9 and 10:
- StartDate: 2015-08-05
- StartTime: 09:00:00
- StopDate: 2015-08-06
- StopTime: 10:00:00

If it is not possible to send the message within this timeframe, it will be discarded.

Specifying a time window as in the previous example would only be useful for very large batches of messages that that would take a long time to process. If you need control over how long a specific message is valid, then take a look at the message validity parameter

### Spam filter

To avoid situations where a recipient receives a large number of messages by mistake, the SMS Gateway implements a filter that keeps track of the number of messages per service sent and received for all MSISDN. 
If a message sent to the SMS Gateway violates the rules implemented in the spam filter it will result in an [error accompanied by a status code](/sections/common.md#message-status), and no message will be sent.

Some services needs to be able to send many messages to the same MSISDN within a short timeframe, and to accommodate for such cases it is possible to disable the spam filter. To disable the spam filter for a service you need to contact Puzzel.

### Message identifiers
All messages sent through the SMS Gateway is assigned a unique identifier named [messageId](/sections/common.md#response-parameters). Each request made to the SMS Gateway will also be assigned a unique identifier named [batchReference](/sections/common.md#response-parameters).
These identifiers follow the messages through the platform and makes it possible to track each individual message. These identifiers is also used in [the delivery reports](/sections/common.md#receiving-sms-delivery-reports-dr).
#### Customer generated identifiers
It is also possible to create identifiers on the customer side. Each message can be given a unique identifier named [clientReference](/sections/common.md#basic-message-parameters). And each request can be given a unique identifier named [batchReference](/sections/common.md#common-parameters) (this will overwrite the default batchReference value from the SMS Gateway).
#### Validations of customer generated identifiers
The message identifiers set by the customer in the request are not validated by default so there is no requirement for them to be unique. It is possible to have the gateway validate that the identifiers are unique for each service. The SMS Gateway will check that an identifier is unique and give an [error message](/sections/common.md#message-status) if it is not.
To avoid keeping track of too many customer generated message identifiers the SMS Gateway will only keep track of message identifiers generated within the last hour.
This functionality must be turned on for the service. Please contact Puzzel support in order to activate this.

### Retry logic and fault situations
When a client connects to the SMS Gateway certain faults can lead to situations where the client does not know if the request was processed or not. This means that the client cannot know if the messages have been sent, and that retrying the operation could lead to duplicate messages being sent. Such situation will typically be network related, e.g. timeouts or a broken connection.
If the client [generates its own identifiers](#customer-generated-identifiers) and [validation is enabled](#validations-of-customer-generated-identifiers), it is possible to retry the operation and be certain that no duplicates will be sent.
