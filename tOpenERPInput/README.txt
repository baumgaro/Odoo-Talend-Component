-----------------------------
datenpol gmbh
Regensburger Straße 9
4020 Linz
Austria
-----------------------------
Web:   http://www.datenpol.at
Email: office@datenpol.at
Phone: +43-732-997035-0
-----------------------------
Created 2013
-----------------------------

This components reads OpenERP entities via XML-RPC.

Usage:
- OpenERP Version: Only v7 is supporteed

- Enter connection data (server, port, database, user, password)

- Model
  Either select a preconfigured model with some scheme data  or 'Custom Model'. 
  In the latter case enter the 'Custom Model Name'.

- Filter: Specify filter for your query

- Scheme:

1) Fields: specify attributes according to the OpenERP object

2) Many2One-Relations
Depending on the type of the attribute (String or Integer) you either receive the 'id' or the 'name' value.
res_partner.title <String>  = name of title
res_partner.title <Integer> = id of title

However, to ensure that attributes can be written to OpenERP you should ALWAYS use 
- the original name and
- the original type

Best practise would be to use:
res_partner.title <Integer> = id of title
res_partner.title___name <String> = name of title

You can extend the fieldname with '___' and some explanatory description:

3) One2Many-Relations

Usually these attributes have the ending '_ids': i.e. res_partner.bank_ids
If the attibute ends with '_ids' you can do as following:

1) Only for One2Many-attributes ending with '_ids'
res_partner.bank_ids <String> = concatenated string of ids separated by commas ('12,23,67,128')

You can easily normalize the result with a tNormalize for further joins with tMap

2) For any One2Many-Attribute

res_partner.bank_ids <List> = ArrayList of Objects containing the ids {'12','23','67','128'}

The resulting list can be interated.
