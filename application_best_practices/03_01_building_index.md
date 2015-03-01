# Step 1: index.html

The first step is to create the **index.html** file with the minimal bootstraping.

TDG stands for **The Definitve Guide**.

We see that we use the **sap.m** libray, the **sap_bluecrystal** theme, the id **sap-ui-bootstrap** is important that the whole script is qualified as a **bootstraping**. We are using the **async** parameter to load all our resources asynchronously, therefore at the bottom we have to use the **attachInit** event to make sure to start with our code after the loading has finished.

We are creating a ```sap.m.Shell``` which has an app-property, where we put our ```sap.ui.core.ComponentContainer``` in.

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

> Async-Parameter from https://sapui5.netweaver.ondemand.com/sdk/docs/guide/91f1e3626f4d1014b6dd926db0e91070.html, this is for the attachInti function