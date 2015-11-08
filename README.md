# Intelecom SMS Gateway
## Offical documentation

Welcome to the developer pages for the Intelecom SMS Gateway API. Here you will find all you need to SMS-enable your applications. This respository will cover the general API documentation and code samples. In addition we provide several other repositories containing finished libraries for many different progamming languages.

### Where to start?

Well - that depends on you, may we suggest:

- Browsing our [list of libraries](#list-of-official-libraries) you can import into your existing code - A good choice if you want to just dive right into coding.
- Learn how our documentation is [structured](#how-the-documentation-is-structured)
- Read our [introduction to A2P SMS and SMS Gateways](/sections/About.md) - a good starting point if you have not used a SMS Gateway before.
- Read the [API documentation](/sections/Interfaces-general.md) for one of our specific interfaces
- [Learn about Intelecom](#about-intelecom), our history in providing SMS services and other related products.
- Find out [how to register an account](#registering-an-account) with Intelecom to start using the SMS Gateway services.

### List of official libraries

We provide you with many "off-the-shelf" libraries that you may use directly in you existing or new applications. Feel free to expand, modify and improve these libraries and we would be thrilled if you send us a pull request or two.

These links will navigate to the respective repository for the chosen library. Basic information about how to get started using these libraries are provided, but please refer to these pages for more in-detail information about the APIs.

**List of current libraries:**

- [PHP](https://github.com/Intelecom/smsgw-client-php)  
- Java  
- [.NET](https://github.com/Intelecom/smsgw-client-dotnet)  
- [Go](https://github.com/Intelecom/smsgw-client-go)  
- [Python](https://github.com/Intelecom/smsgw-client-python)  
- [Node.js](https://github.com/Intelecom/smsgw-client-nodejs)   

Please do get in touch and let us know if you are missing any libraries from this list.

### How the documentation is structured

The documentation consists of different sections, starting an overview / table of contents page. From each section you may navigate to the next section, or jump directly into a specific section.

**Section list:**

- [Overview](/sections/Overview.md) (Introduction and ToC)
- [About A2P SMS and SMS Gateways](/sections/About.md)
- [Common SMS Gateway documentation](/sections/Common.md) - information relevant to most of the interfaces.
- [Interface specifications](Interfaces-general.md)
	- [REST API](sections\Interfaces\Rest.md)
	- [SOAP API](sections\Interfaces\Soap.md)
	- [HTTP GET API](sections\Interfaces\HTTP_Get.md)
	- [SMTP SMS GW](sections\Interfaces\SMTP.md)
	- [TCP sockets / XML](sections\Interfaces\TCP_XML.md)
	- [SMPP](sections\Interfaces\SMPP.md)
- Library documentation - [Each library](#list-of-official-libraries) provides basic "getting started" in each repo (readme.md).
- How to [get in touch with us](/sections/Contact.md)?

We also provide reference documentation such as the SMPP specification and GSM specifications. 

### Registering an account

To use the SMS Gateway you will need the URLs to our staging / production sites as well as some credentials:
- Username / password
- Serviceid

If you do not already have an account, and want to try out or order access, please do contact us for more information. We provide demo accounts for both live and emulated MNOs - no strings attached. 

For live accounts pricing is based on establishment, monthly subscription and traffic (per message) fees. Contact us for more information.


### About Intelecom 

Intelecom is a leading provider of cloud-based and on-premise communication solutions. We have over 30 years of experience and with our experience and competence we aim to give our customers stable, flexible, user-friendly and scalable solutions. 

We provide innovative solutions for SMS, mobile applications, system integration, call-centers, wireless networks, unified communications and more. Our customer base counts over 2000 customers across many verticals from offshore to transport, primarially in Scandinavia and UK. What most of our customers have in common is that they have a need to be able to communicate better with their users and employees. Our contribution is often that we offer means to integrate exisiting solutions with new ones or new interfaces. This results in continous utilization of current investments and at the same time providing a value-add for the customer. Our mission is to make sure that good communication is rewarding. 

SMS solutions have been a part of Intelecom starting with the platform originally set up by Carrot Communications  back in 2000. Since then not a lot have changed in the basic SMS GSM specifications, but a lot have changed concerning our customers demands for stability, scalablity, redundancy and speed. SMS now is a business critical application for many companies, both private and public. In addition a lot have happened with SMS as a payment channel over the years. In later years many telcos have been opening up for selling physical goods and services, using SMS or carrier billing as payment. We at Intelecom have been working hard to keep up, both with customer demands and new possibilities over the years. As a result, we have a SMS platform, now in it's fifth major version, that is both techically advanced, high-capacity and stable. 

#### Intelecom Group
[Intelecom Group AS](http://www.intelecom.no) was started in Norway in 1998 and has its roots in older companies such as Alcatel and Nexans. In 2010 Intelecom merged with Carrot Communications and was aquired by Herkules Capital. The main office is located in Oslo, with branch offices in many other Norwegian cities, Sweden, Denmark, Bulgaria and UK. 

#### Herkules Capital
Since 2010, Intelecom Group and its subsidiaries have been fully owned by [Herkules Capital](http://www.herkulescapital.no/), the leading Norwegian private equity firm which supports established companies located in the Nordic region with strong growth potential.

### Authors
- Sven Ståle Osa
- Andreas Häber
- Morten Trydal
- Gunnar Grenlee

> **Note:** These documents replaces the PDF only documentation which final version was _2.3.0_.

