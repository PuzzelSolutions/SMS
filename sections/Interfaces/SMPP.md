#SMPP API

It is possible to integrate towards the Intelecom SMS gateway using the SMPP protocol. Please see chapter 8 - Appendix B for further details.

The SMPP Gateway supports version 3.4 of the SMPP interface. The SMPP protocol specification can be provided upon request.

### Supported PDUs
- bind_receiver
- bind_receiver_resp
- bind_transmitter
- bind_transmitter_resp
- bind_transceiver
- bind_transceiver_resp
- unbind
- unbind_resp
- submit_sm
- submit_sm_resp
- deliver_sm
- deliver_sm_resp
- enquire_link
- enquire_link_resp

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
- "schedule_delivery_time" is ignored, messages will be delivered immediately.
- "registered_delivery" is ignored, the SMPP gateway will use the SMS Gateway service setting.
- "replace_if_present_flag" is ignored.
- "sm_default_msg_id" is ignored.
- All optional parameters are ignored except "message
