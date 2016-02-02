#Overview
[Back to main page](https://github.com/Intelecom/sms/) - [Next section](/sections/About.md)

## Table of Contents

- [Overview](/sections/Overview.md) (This section)
- [About A2P SMS and SMS Gateways](/sections/About.md)
- [Common SMS Gateway documentation](/sections/Common.md) - information relevant to most of the interfaces.
- [Interface specifications](Interfaces-general.md)
	- [REST API](/sections/Interfaces/Rest.md)
	- [SOAP API](/sections/Interfaces/Soap.md)
	- [HTTP GET API](/sections/Interfaces/HTTP_Get.md)
	- [SMTP SMS GW](/sections/Interfaces/SMTP.md)
	- [TCP sockets / XML](/sections/Interfaces/TCP_XML.md)
	- [SMPP](/sections/Interfaces/SMPP.md)
	- [Management API](/sections/Interfaces/Management-api.md)
	- [Value-added services for MO messages](/sections/Interfaces/VAS.md)
- Library documentation - [Each library](#list-of-official-libraries) provides basic "getting started" in each repo (readme.md).
- How to [get in touch with us](/sections/Contact.md)?

##Introduction
This documentation describes the functionality of, and explains how to integrate with, the Intelecom SMS Gateway (SMSGW). 

The SMSGW is an API that enables your solution(s) to send and receive SMS messages, both single messages and bigger batches of messages using the same API. 

To be able to connect to the SMSGW you will need a service configured by Intelecom with sensible defaults and settings for your use case.  The service identifiers are serviceid, as well as a username and password. Please contact Intelecom Support (support.interactive@intele.com) if you want to create an agreement, get a demo account or if you have an active agreement but have not received these credentials.

The SMSGW has three main functionalities with corresponding APIs:

- Sending one or many SMS messages from your system to end-users (MT)
- Receiving SMS messages from end-users to your system (MO)
- Receiving delivery reports to your system for SMS messages sent to end-users (DR)

To send SMS messages to end-users, you need to integrate with one of the APIs via REST (XML, JSON or web form over HTTP POST), Web Service (with corresponding WSDL), email (SMTP), SMPP, TCP Sockets or via HTTP GET (with query parameters). 

Due to the flexibility of the REST / SOAP interfaces, we generally recommend that you choose to integrate with one of these endpoints if possible.

To receive SMS messages (MO) or delivery reports (DR) you need to provide a service endpoint that can receive HTTP GET or POST requests. As an alternative, you can also receive MO messages as email messages (SMTP) or using the SMPP protocol.

#####High level sequence diagram for basic SMS Gateway operations
![Figure 1: High-level sequence diagram for basic SMSGW operations](http://i.imgur.com/3CXClMd.jpg)

Additionally, the Gateway provides a Management API to manage messages. A description of this API is given [here](/sections/Management.api.md).

##Abbreviations

<table>
<tr><th>Abbreviation</th><th>Description</th></tr>	
<tr><td>MCC</td><td>Mobile Country Code</td></tr>	
<tr><td>MNC</td><td>Mobile Network Code</td></tr>	
<tr><td>SNO</td><td>Short Number (e.g. 1960)</td></tr>	
<tr><td>TTL</td><td>Time To Live</td></tr>	
<tr><td>UDH</td><td>User Data Header</td></tr>	
<tr><td>DCS</td><td>Data Coding Scheme</td></tr>	
<tr><td>MO</td><td>Mobile Originated (incoming messages sent from end users)</td></tr>	
<tr><td>MT</td><td>Mobile Terminated (outgoing messages sent to end users).</td></tr>	
<tr><td>CP</td><td>Content Providers (Customers of Intelecom and Intelecom itself)</td></tr>	
<tr><td>DR</td><td>Delivery Reports (Confirmations from operators that messages have been / not have been received by end-user)</td></tr>	
<tr><td>MSISDN</td><td> Mobile Station International ISDN Number</td></tr>	
<tr><td>SMSGW</td><td>Intelecom SMS Gateway</td></tr>	
<tr><td>REST</td><td>Representational State Transfer (https://en.wikipedia.org/wiki/Representational_state_transfer)</td></tr>	
<tr><td>MNO</td><td>Mobile Network Operator (e.g. Telenor, Telia)</td></tr>	
<tr><td>CPA</td><td>Content Provider Access – An agreement with MNOs to be able to use four digit short numbers with billing possibilities.</td></tr>	
<tr><td>GAS</td><td> Goods And Services – Like CPA only with the possibility to sell physical goods and services.</td></tr>	
</table>