# Preparing

Here is an overview about the aspcets of an enterprise app written in SAPUI5.

## Approach
SAPUI5 is areal big library and there are different ways to reach your goal. We show you one way, feel free to choose another.

## Definition of an App
### Indipendent
You should use a **Component.js** and a minimal **index.html** file for your application. With this approach you can use the app stand-alone or in a SAP Fiori launchpad.

The Component.js is used for setting up the routing, the models and starting the app.
The index.html _(you could also name it localIndex.html or any other name)_ contains the **bootstraping** and starts the Component in a so-called ```sap.m.ComponentContainer```.

The bootstraping is responsible for starting up SAPUI5: where is the sapui5 script located, which theme and libraries you'd like to use and where the framework can find your files with the ```data-sap-ui-resourceroots``` parameter.

#### Bootstraping example:
```
<script id="sap-ui-bootstrap"
	src="resources/sap-ui-core.js"
	data-sap-ui-libs="sap.m"
	data-sap-ui-theme="sap_bluecrystal"
	data-sap-ui-xx-bindingSyntax="complex"
	data-sap-ui-resourceroots='{"where_are_my_files": "./"}'>
</script>
```
### Adressable
It should be possible to bookmark or forward a link to a certain point in the application, for example to a specific product. We are linking resources (f.e. product) and not application states. This behaviour is called **deep linking**.

Here you see a deep linked example to the supplier of the first product: ```index.html#/product/1/supplier```

### UI-Focused
An app consists of backend and frontend logic. Both can be developed seperately - with mocking and testdata it is possible to continue with the frontend development even if the backend is not ready. SAPUI5 uses the MVC concept so that you can seperate your UI from the frontend logic.

### Responsive
The ```sap.m``` library is designed from the ground up to run on different devices like desktop, tablets and mobile. For layouting the ```sap.ui.layout``` library is used and also the core MVC library with ```sap.ui.core.mvc```.

To handle information about the device and it's different capabilities (touch and navigation buttons) we will create a **device model**. The information will be gathered upfront and then can be consumed in the declarative XML views. There it will be used for ```sap.m.ListMode```and ```sap.m.ListType```.

### Accessible
SAPUI5 ```sap.m Controls``` have build in **keyboard support**. When you are using native HTML to enhance your app, you have to take care about accessiblity (keyboard, high contrast theme) on your own.

### Translateable
To handle translations in your application, we will use a **resource model** (called i18n which is short for internationalization). The files are stored as _.properties files_. SAPUI5 has also support for right-to-left (RTL) languages. The language of the user is gathered via the users implicit locale settings or via an URL parameter.

### Maintainable
Applications can get big and complex very quickly. To stay on top of things we have the MVC concept and the Component concept. The Component is a concept to use and reuse the application as whole or in parts.

## Design Patterns
The different patterns used in SAP Fiori are:

* Master-Detail (MD)
* Master-Master-Detail (MMD)
* Full Screen (FS)
* Multi Flow (MF)

This guide uses the Master-Detail pattern, whis is created with the ```sap.m.SplitApp``` control. You have your **Master** on the left side and the **Detail** on the right sight of your application.

With the Master-Master-Detail you navigate from Master1 to Master2 and then to the Detail.
In the Full Screen app you see everything on one screen.
With the Multi Flow you yould switch from a Full Screen to the next Full Screen and then maybe to a Master Detail.

## Business Scenario
The well known Northwind OData service will be used for this guide. We will be using the **products** entityset. Each product has a relation (association) to 0..1 **supplier** and 0..1 **category**.

We will use a Read-Write V2 version of the Northwind service, our session id is **sapuidemotdg** - feel free to use your own: ```http://services.odata.org/V2/(S(sapuidemotdg))/OData/OData.svc/``` 

### Functionality
The app will present a list of existing products. Once a product is selected detailed information about the product, supplier and category will be shown. Navigation to the details of a product will also be possible via URL.

You will also have the possiblity to add a new product which is saved in the backend. You can also provide category and supplier. Only very little to no input validion will be used.