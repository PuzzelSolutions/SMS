#Value-added services for MO messages
[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/Overview.md) - [Previous section](/sections/Interfaces/Management-api.md) 

It is possible to enable automatic retrieval of customer data and attach it to the incoming SMS messages. Currently the services offers directory inquiries and network lookup.

This integration extends the set of input parameters available in the MO SMS request given above with the following:

<table>
<tr><th>VAS Type</th><th>Parameter name</th><th>Description</th></tr>
<tr><td>Directory Inquiry</td><td>di_recordtype</td><td>Record type. See the table below for mapping the code to types.<table><tr><th>Code</th><th>Type</th><th>Description</th></tr><tr><td>0</td><td>Unset</td><td>No result received from the directory inquiry service provider</td></tr><tr><td>1</td><td>Person</td><td>Personal Record</td></tr><tr><td>2</td><td>Business</td><td>Business / company / organizational record</td></tr><td>3</td><td>Hybrid</td><td>Mixed Result Data</td></tr><tr><td>4</td><td>Unknown</td><td>Type is unknown</td></tr></table></td></tr>
<tr><td></td><td>di_firstname</td><td>First name, if person</td></tr>
<tr><td></td><td>di_middlename</td><td>Middle name</td></tr>
<tr><td></td><td>di_lastname</td><td>Last name, or company name if record type is Business</td></tr>
<tr><td></td><td>di_gender</td><td>Gender type. See the table below for mapping the code to types.<table><tr><th>Code</th><th>Type</th><th>Description</th></tr><tr><td>0</td><td>Unset</td><td>No result received from the directory inquiry service provider</td></tr><tr><td>1</td><td>Male</td><td></td></tr><tr><td>2</td><td>Female</td><td></td></tr><td>3</td><td>Hybrid</td><td></td></tr><tr><td>4</td><td>Unknown</td><td></td></tr></table></td></tr>
<tr><td></td><td>di_birthdate</td><td>Person - Birth date in format YYYYMMDD</td></tr>
<tr><td></td><td>di_streetname</td><td>Address - Street name</td></tr>
<tr><td></td><td>di_house_number</td><td>Address - House number</td></tr>
<tr><td></td><td>di_entrance</td><td>Address - House entrance</td></tr>
<tr><td></td><td>di_zip</td><td>Address - Post zip number</td></tr>
<tr><td></td><td>di_zip_location</td><td>Address - Post zip location</td></tr>
<tr><td></td><td>di_municipiality</td><td>Address - Municipality</td></tr>
<tr><td></td><td>di_country</td><td>Address - Country</td></tr>
<tr><td></td><td>di_orgnr</td><td>Business – Organization number</td></tr>
<tr><td></td><td>di_boxtext</td><td>Postbox – Name on postbox</td></tr>
<tr><td></td><td>di_boxnumber</td><td>Postbox – Number</td></tr>
<tr><td></td><td>di_boxoffice</td><td>Postbox - Office</td></tr>
<tr><td></td><td>di_boxzip</td><td>Postbox – Post zip code</td></tr>
<tr><td></td><td>di_boxcity</td><td>Postbox – Post zip location / city</td></tr>
<tr><td></td><td>di_boxcountry</td><td>Postbox - Country</td></tr>
<tr><td></td><td>di_coord_matchtype</td><td>Coordinate – match type</td></tr>
<tr><td></td><td>di_coord_xpos</td><td>Coordinate – X Position</td></tr>
<tr><td></td><td>di_coord_ypos</td><td>Coordinate – Y Position</td></tr>
<tr><td>MSISDN Network lookup</td><td>msisdn_errorcode</td><td>Error code</td></tr>
<tr><td></td><td>msisdn_errortext</td><td>Error description</td></tr>
<tr><td></td><td>msisdn_mnc</td><td>Mobile network code</td></tr>
<tr><td></td><td>msisdn_mcc</td><td>Mobile country code</td></tr>
<tr><td></td><td>msisdn_spid</td><td>Service provider ID</td></tr>
<tr><td></td><td>msisdn_spname</td><td>Service provider Name</td></tr>
<tr><td></td><td>msisdn_cc</td><td>Country Code</td></tr>
</table>

### HTTP GET example of a valid MO URL with VAS parameters

	http://mogw.example.com/incomingaction?messageid=[messageid] &originator=[originator]&streetname=[di_streetname]&date_of_birth=[di_birthdate]&mnc=[msisdn_mnc]&mcc=[msisdn_mcc]

The attributes in the SMS-MO message will substitute the corresponding part of the template.
