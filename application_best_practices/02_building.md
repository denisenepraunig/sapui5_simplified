# Building

We start to build the application from scratch with a serices of small progressions. In "preparing" the characteristics of a SAPUI5 application have been covered.

The final Master-Detail application will look like this:

TODO IMAGE Master Detail

The app is build with the following blocks:

TODO IMAGE app components

## Building blocks
* **index.html** creates a ```sap.m.Shell``` and a ```sap.m.ComponentContainer``` which initializes the Component
* **Component.js** is a ```sap.ui.core.UIComponent```, it creates the models for the _data, device and translation_, it starts the _App.view.xml_ and configures the routing
* **App.view.xml** creates the Split app
* **MyRouter.js** handles the routing
* **...view.xml** are the different views like Master and Detail
* **...controller.js** are the corresponding controllers for the views
* **...fragment.xml** are small view parts without own controllers, used for creating new product
* **Formatter.js** contains formating utilites used in the Master and Detail view

### Index, Component and Message Bundle

#### Index
In the index file there is only minimal configuration done in the **bootstrap**, like the theme, databinding-syntax and the resource-roots. A **Shell** is created, which is responsible that the app has a nice background and that there is space to the left and right of the screen. The **ComponentContainer** is needed to instanciate the Component.

### Component
The **Component** is the file **Component.js** located next to the index.html. Technically speaking it is a **UIComponent** but we will refer to it as Component. In the Component there is some metadata defined like app information and routing.

The **Routing** is the most crucial part for non-trivial apps and it superseeds the previous ```sap.ui.core.EventBus``` based naviagtion. The ```sap.ui.core.routing.Router``` is also initialized here.

All the **models** for data (domain), the device and the translation/internationalization/i18n (**Message Bundle**) are also created in the Component.

The root view of the application **App.view.xml** is also instantiated in the Component.

### Views and Fragemts
The root view is the **App.view.xml** which contains the ```sap.m.SplitApp``` contorl, which is needed for creating a Master-Detail application. The master-detail aggreations of the SplittApp are filled at runtime via the Router, so therefore the view itself is pretty small. The App View does not need a controller.

The main views of the app are the **Master** and **Detail** view. Each of these views contain a ```sap.m.Page```. A Page can have a title, content and a footer. 

There is also a **NotFound** view when no view can be matched to a requested resource. The **AddProduct** view is used to add a new product. All views are independet to each other.

**Fragments** are lightweight, re-usable UI definitions which have no own controller. Their files are named **fragmentname.fragment.xml**. The fragments in this example contain a ```sap.ui.layout.form.SimpleForm``` for displaying the supplier address and the category details.