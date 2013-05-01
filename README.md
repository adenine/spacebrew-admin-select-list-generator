Spacebrew Admin Select List Generator  
=====================================  
  
This script enables you to easily add admin select lists for subscribers and publishers to your admin-enabled client spacebrew apps. You just have to follow these 5 easy steps (more details are included below):  
  
  1. import the select list generator script  
  2. instantiate the select list generator  
  3. initialize the drop down lists   
  4. register the spacebrew client object with the list generator  
  5. add html select tag for each admin select lists  
  
Please note that this library only works will the Spacebrew.js library sb-admin-0.1.0 and above.  
  
@author: 	Julio Terra  
@filename:	sb-admin-dropdown-gen-0.2.0.js  
@version:	0.2.0  
@date: April 30, 2013  

Detailed Instructions
---------------------  

###1. Import the Select List Generator Script  
At the top of your web app page import the select list generator script using a standard HTML script tag.

```
<script type="text/javascript" src="js/sb-admin-dropdown-gen-0.2.0.js"></script>
```

###2. Initialize the Select List Generator
In your javascript code, you first need to initialize the select list generator by calling the `adminSelectListGenerator` method. This method will return an object with two methods, `initDropdown` and `registerSB`, both of which we will review below.

```
var selects = adminSelectListGenerator( { "debug": false } );
```

###3. Initialize the Drop Down Lists
Next, you need to call the `initDropdown` method. This method will read, and then customize, the appropriate HTML select nodes on your web app. This method will also identify the data types to which it needs listen for when parsing admin messages from Spacebrew. 

```
select.initDropdown()
```

###4. Register Spacebrew Client Object
The `registerSB` method is used to add the following admin event listeners to the Spacebrew Client object: `onNewClient`, `onUpdateClient`, `onRemoveClient`, and `onUpdateRoute`. 

```
select.registerSB( sb )
```

###5. Add HTML Select Tags to Your Code
Finally you need to add an HTML select tag for each of the admin select lists that you want to generate. The select tag needs to include the following attributes:
* `class="spacebrew-select"`: the script will attempt to process all select nodes that feature that class spacebrew-select.  
* `data-local-route-name`: name of the publisher or subscriber. This name needs to match exactly the name of the publisher or subscriber to which this select list is associated.  
* `data-pub-or-sub`: flag that identifies if this is a `publisher` or `subscriber`. Note that if this is a publisher, then the list will be populated with subscribers, and vice versa.  
* `data-sb-type`: data type of the publisher or subscriber. The data type can be a custom or standard data type.  
  
```
<select data-local-route-name="text" data-sb-type="string" data-pub-or-sub="subscriber" class="spacebrew-select"></select>
```
  
Feel free to stylize these tags.  By default, this script was designed to work nicely with jQuery mobile. It also works with just plain HTML. It has not been tested with other frameworks, such as bootstrap.

###6. Remember that You Need the Spacebrew Admin Library
In order for the admin select script to work you have to import the Spacebrew Admin library, and extend the Spacebrew Client library with admin functionality. Here's how:

To import the Spacebrew Admin library just use a standard HTML script tag pointing to the appropriate file
```
<script type="text/javascript" src="js/sb-admin-0.1.0.js"></script>
```

To extend the Client Spacbrew library with the admin functionality just use the Spacebrew Client library `extend` method. Make sure to extend the Spacbrew Client library before registering it to admin select script.
```
sb = new Spacebrew.Client();
sb.extend(Spacebrew.Admin);
```
