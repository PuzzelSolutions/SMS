#SMTP API

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/Overview.md) - [Previous section](/sections/Interfaces/SMTP.md) -  [Next section](/sections/Interfaces/TCP_XML.md)

The SMS gateway also provides email as an alternative channel for sending / receiving sms messages. This channel is limited in what kind of messages it can send and what parameters are accepted. 

### Sending email to SMS (MT SMS)

The recipients in the mail message are the receivers of the message in the format: 

	<recipient>-<serviceid>@smsmail.intele.com

The subject field is ignored (however, it may be configured to be appended to the message). The body of the email is used as the SMS content.

There is a maximum limit of 918 characters of the sms, and sms’ that extend one sms (160 characters) are concatenated and sent as single message to the phone (with many fragments).


### Receving email from SMS (MO SMS)

It is also possible to configure the SMSGW to format and send an incoming SMS message as an email message.

The email address to send incoming SMS messages to will need to be provided to Intelecom service desk. The end user's mobile number as well as Intelecom's serviceid is by default set as the originator of the message (this is highly configurable though), so it is fully supported to reply to an email to respond immediately.

The SMS message content will come in the email body, but is also highly configurable.

By saying highly configurable, we mean that any field from [this section](/sections/Common.md#parameters-for-incoming-mo-messages) can be substituted in any of the fields in the email. 

Example: 

	Sender: 	[originator]-[serviceid]@sms.carrot.no
	Subject: 	SMS message from Intelecom: [originator]
	Message:	This is a message from Intelecom SMS platform. User sent: [content]

### Limitations

- It is only possible to send ordinary text messages
- Messageid, status etc. (ack) is not returned when sending a message
- Valid parameters when sending SMS are
	- recipient
	- serviceid
	- newSession
	- content

### Security

You will need to provide us with the IP adresses / IP ranges of the machines that should be able to send email towards the SMS Gateway. Support staff will then add these IP adresses as valid senders, all other IP adresses will be rejected. 