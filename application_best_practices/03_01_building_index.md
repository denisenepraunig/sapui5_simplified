# Step 1: index.html

The first step is to create the **index.html** file with the minimal bootstraping.

TDG stands for **The Definitve Guide**.

### index.html
```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta charset="UTF-8">
        
        <title>TDG Demo App</title>
        
        <script id="sap-ui-bootstrap"
        src="/path/to/resources/sap-ui-core.js"
        data-sap-ui-libs="sap.m"
        data-sap-ui-theme="sap_bluecrystal"
        data-sap-ui-preload="async"
        data-sap-ui-xx-bindingSyntax="complex"
        data-sap-ui-resourceroots='{ "sap.ui.demo.tdg": "./" }'>
        </script>
        
        <script>
            sap.ui.getCore().attachInit(function() {
                new sap.m.Shell({
                    app: new sap.ui.core.ComponentContainer({
                        height : "100%",
                        name : "sap.ui.demo.tdg"
                    })
                }).placeAt("content");
            });
        </script>
    </head>
    <body class="sapUiBody" id="content" />
</html>
```

## Header
We tell the Internet Explorer to its newes rendering mode - and not compatible mode with ```<meta http-equiv="X-UA-Compatible" content="IE=edge" />```. And we are using **UTF-8** with ```<meta charset="UTF-8">```.

## Bootstrap
We see that we use the **sap.m** libray, the **sap_bluecrystal** theme. The id **sap-ui-bootstrap** is important sothat the whole script is qualified as a **bootstraping**. We are using a **complex** data-binding syntax, which means we can mix databinding and additional text like: ```<Label text="{binding} additional text">```.

We are using the **async** parameter to load all our resources asynchronously, therefore at the bottom we have to use the **attachInit** event to make sure to start with our code after the loading has finished.

We are creating a ```sap.m.Shell``` which has an app-property, where we put our ```sap.ui.core.ComponentContainer``` , which then tries to instantiate our Component via its name property **sap.ui.demo.tdg**.

Our Component file is called **Component.js** but we are refernecing the name **sap.ui.demo.tdg**. This works because we defined the ```data-sap-ui-resourceroots='{ "sap.ui.demo.tdg": "./" }'```. This means that **sap.ui.demo.tdg** is based in the same folder **/.** and the ComponentContainer is looking automatically for the Component.js file.

The **Compoment.js** file looks like this and there you see it's namespace **sap.ui.demo.tdg.Component**:
```
jQuery.sap.declare("sap.ui.demo.tdg.Component");
sap.ui.core.UIComponent.extend("sap.ui.demo.tdg.Component", {
...
``` 


> Async-Parameter from https://sapui5.netweaver.ondemand.com/sdk/docs/guide/91f1e3626f4d1014b6dd926db0e91070.html, this is for the attachInti function