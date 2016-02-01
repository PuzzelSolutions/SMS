#SMPP API

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/Overview.md) - [Previous section](/sections/Interfaces/TCP_XML.md) -  [Next section](/sections/Interfaces/Management-api.md)

It is possible to integrate towards the Intelecom SMS gateway using the SMPP protocol.

The SMPP Gateway supports version 3.4 of the SMPP interface. The SMPP protocol specification can found onine, for example [here](https://www.openmarket.com/customer-center/documentation/SMSSMPP-Specification/SMPP-v3-4-Issue1-2.pdf)

### Supported PDUs
- bind_receiver
- bind\_receiver_resp
- bind_transmitter
- bind\_transmitter_resp
- bind_transceiver
- bind\_transceiver_resp
- unbind
- unbind_resp
- submit_sm
- submit\_sm_resp
- deliver_sm
- deliver\_sm_resp
- enquire_link
- enquire\_link_resp

###	Data coding scheme
- The default encoding scheme is GSM encoding.
- Supported encoding schemes:
	- GSM (SMSC Default Alphabet)
	- IA5/ASCII
	- Latin 1 (ISO-8859-1)
- No bit packing.

### Validity period
- The minimum validity period is 5 minutes, which is also the default.
- The maximum validity period is one week.

### Current limitations
- "SUBMIT SHORT MESSAGE" operation
- Only alphanumeric text messages are supported.
- "esm_class" is ignored, all bits are set to 0.
- "protocol_id" is ignored.
- "priority_flag" is ignored.
- "schedule\_delivery_time" is ignored, messages will be delivered immediately.
- "registered_delivery" is ignored, the SMPP gateway will use the SMS Gateway service settings.
- "replace\_if\_present_flag" is ignored.
- "sm\_default\_msg_id" is ignored.
- All optional parameters are ignored except "message_payload"
