#Available Interfaces

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/overview.md) - [Previous section](/sections/common.md) -  [Next section](/sections/interfaces/rest.md)

The SMS Gateway API have several different interfaces that you can choose to integrate towards. We generally suggest the REST API for both MT, MO and DR if you have no preference.

- [REST API](/sections/interfaces/rest.md)
- [SOAP API](/sections/interfaces/soap.md)
- [HTTP GET API](/sections/interfaces/http-get.md)
- [SMTP SMS GW](/sections/interfaces/smtp.md)
- [SMPP](/sections/interfaces/smpp.md)
- [TCP sockets / XML](/sections/interfaces/tcp-xml.md)

The different interfaces have some differences regarding what functionality is available, see table below:


<table>
<tr><th>Interface Name</th><th>Outgoing (MT SMS)</th><th>Incoming (MO SMS)</th><th>Delivery Reports (DR)</th><th>Comments</th></tr>	
<tr><td>REST API</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Recommended</tr>
<tr><td>SOAP API</td><td>Yes</td><td>No</td><td>No</td><td></tr>
<tr><td>HTTP(S) GET</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Number of messages in each batch limited by max URL length</tr>
<tr><td>SMTP (email)</td><td>Yes</td><td>Yes</td><td>No</td><td>Not all parameters are available</tr>
<tr><td>SMPP</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Only recommended if you have a pre-built SMPP client </tr>
<tr><td>TCP Socket</td><td>Yes</td><td>No</td><td>No</td><td></tr>
</table>

It is possible to combine the different interfaces, for example it is possible to send MT messages using SOAP webservices, receive MO SMS using Rest API (HTTP POST with JSON or XML) and recieve delivery reports using HTTP(S) GET.

When integrating towards SMS Gateway, make sure that your client support the latest TLS standars (e.g. TLSv1.2) and support cipher suites that are considered secure.
