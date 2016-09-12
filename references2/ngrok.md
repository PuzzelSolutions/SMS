# Using ngrok to test MO and DR messages locally

[ngrok](https://ngrok.com/) is a great tool for establishing secure tunnels to localhost and is such ideal to use when developing for MO (incoming SMS) and DR (Delivery Reports).

Install ngrok, implement your server-side code for receiving messages and deploy it to a server running on localhost. Typically the server is running in your IDE to allow for debugging etc. 

Next, say the development server is running http on localhost port 8080, then run ngrok:

	ngrok http 8080

If everything is fine, you should see something like this:

![](http://i.imgur.com/vVbye9k.png)

The forwarding URL generated can then be provisioned in the Intelecom extranet or by our support staff so that you receive actual MO SMS and DR from our SMS platform to your localhost. [Contact us](/sections/contact.md) for more information regarding URL provisioning when integrating.

See also [ngrok documentation](https://ngrok.com/docs) for much more details.