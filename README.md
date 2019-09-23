# Puzzel SMS Gateway
## Official documentation

Welcome to the developer pages for the Puzzel SMS Gateway API. Here you will find all you need to SMS-enable your applications. This repository will cover the general API documentation and code samples. In addition we provide several other repositories containing finished libraries for many different programming languages.

### Where to start?

Well - that depends on you, may we suggest:

- Browsing our [list of libraries](#list-of-official-libraries) you can import into your existing code - A good choice if you want to just dive right into coding.
- Learn how our documentation is [structured](#how-the-documentation-is-structured)
- Read our [introduction to A2P SMS and SMS Gateways](sections/about.md) - a good starting point if you have not used a SMS Gateway before.
- Read the [API documentation](/sections/interfaces-general.md) for one of our specific interfaces
- [Learn about Puzzel](#about-Puzzel), our history in providing SMS services and other related products.
- Find out [how to register an account](#registering-an-account) with Puzzel to start using the SMS Gateway services.

### List of official libraries

We provide you with many "off-the-shelf" libraries that you may use directly in your existing or new applications. Feel free to expand, modify and improve these libraries and we would be thrilled if you send us a pull request or two.

These links will navigate to the respective repository for the chosen library. Basic information about how to get started using these libraries are provided, but please refer to these pages for more in-detail information about the APIs.

**List of current libraries:**

- [PHP](https://github.com/Intelecom/smsgw-client-php)  
- [Java](https://github.com/Intelecom/smsgw-client-java) 
- [.NET](https://github.com/Intelecom/smsgw-client-dotnet)  
- [Go](https://github.com/Intelecom/smsgw-client-go)  
- [Python](https://github.com/Intelecom/smsgw-client-python)  
- [Node.js](https://github.com/Intelecom/smsgw-client-nodejs)   

Please do get in touch and let us know if you are missing any libraries from this list.

### How the documentation is structured

The documentation consists of different sections, starting with an overview / table of contents page. From each section you may navigate to the next section, or jump directly into a specific section.

**Section list:**

- [Overview](sections/overview.md) (Introduction and ToC)
- [About A2P SMS and SMS Gateways](sections/about.md)
- [Common SMS Gateway documentation](sections/common.md) - information relevant to most of the interfaces.
- [Interface specifications](sections/interfaces-general.md)
	- [REST API](sections/interfaces/rest.md)
	- [SOAP API](sections/interfaces/soap.md)
	- [HTTP GET API](sections/interfaces/http-get.md)
	- [SMTP SMS GW](sections/interfaces/smtp.md)
	- [TCP sockets / XML API](sections/interfaces/tcp-xml.md)
	- [SMPP](sections/interfaces/smpp.md)
	- [Management API](sections/interfaces/management-api.md)
	- [Value-added services for MO messages](sections/interfaces/vas.md)
- Library documentation - [Each library](#list-of-official-libraries) provides a basic "getting started" in each repo (readme.md).
- How to [get in touch with us](sections/contact.md)?

We also provide reference documentation such as the SMPP specification and GSM specifications. 

### Registering an account

To use the SMS Gateway you will need the URLs to our staging / production sites as well as some credentials:

- Username 
- Password
- Serviceid


If you do not already have an account and want to try out or order access, please do [contact us](sections/contact.md) for more information. We provide demo accounts for both live and emulated MNOs - no strings attached. 

For live accounts pricing is based on establishment, monthly subscription and traffic (per message) fees. 


### About Puzzel 

Puzzel (formerly Intelecom’s contact centre entity) builds on 20 years’ heritage of crafting inventive and dependable solutions for customer interactions. It was one of the first pioneers to develop a cloud-based contact centre and has now extended this to encompass a complete new customer interaction platform with unique integration capabilities and payment solutions. Puzzel can be adapted to accommodate from one to several thousand users using any device, in any location and integrates with multiple applications seamlessly, allowing customers to meet the needs of today’s omni-channel and mobile environments.

Puzzel is one of the few contact centre solutions that is completely multi-channel and brings together all the pieces to respond to phone, email, Web Chat, Social Media, SMS and payment enquiries all within one application. Click here to learn more about our multi-channel contact centre with our new extensible user interface and secure payment solutions.

Puzzel employs over 130 people who are all passionate about delivering innovative customer interaction solutions for contact centres and mobile environments.

##### Puzzel’s Heritage

Puzzel is an enigma – it is a new and vibrant company with over 20 years’ heritage of delivering communication solutions that take customer interaction to another level.

Puzzel was created out of Intelecom Group to further focus on developing it’s contact centre and payment solutions where the company has taken a substantial position in the fast-growing market for cloud-based Customer Engagement Solutions. These solutions are used by a range of customers in different geographies, verticals and usage areas.

Puzzel’s focus is to develop and deliver inventive technology that is empowering our customers by being feature rich and easy to use, being able to adapt to any environment through strong integration capabilities, and always being dependable by offering consistently high levels of stability and security.


### Authors
- Sven Ståle Osa
- Andreas Häber
- Morten Trydal
- Gunnar Grenlee
- Kjetil Johannesen

> **Note:** These documents replace the PDF only documentation which final version was _2.3.0_.

