seamless.js (v1.0.0)
==================================

About
----------------------------------
seamless.js is the mobile web/app display advertising script of seamless. The script currently supports interstitial (320x480), banner (320x50), medium rectangle (300x250) and custom size display advertising formats.


## Table Of Contents
* [Integration Steps](#integration)
    * [1. Insert ad places into your HTML document](#ad-places)
    * [2. Define ad properties and options](#ad-definitions)
    * [3. Copy and paste seamless.js initializer](#initialize)
* [Configuration](#configuration)
* [Custom Initialization](#custom-initialization)


## Integration Steps

### 1. Insert ad places into your HTML document

Ad places are empty div nodes with unique id's. seamless.js will inject ads into these places whenever an ad is available for the place. Insert these div nodes in suiting parts of your HTML document.
Say you want to have a banner ad at footer section of your page, place a div node into your footer node and set a unique id for the div. Or you want to have an interstitial ad on your page, simply add another div node right after opening of the body tag (`<body>`), again with a unique id.

```
    <div id="seamless-banner"></div>
    <div id="seamless-mre"></div>
```

### 2. Define ad properties and options

Now that you have empty ad places in your documents, seamless.js needs to know what to inject into those places.
Ad properties and options are defined in the window.seamlessAds global variable. The value for this variable is an array of objects and each object in the array has the definition for a single ad place.
If you have two ad places on your page, one with unique id seamless-banner to display standard banners ads (size 320x50) and the other with unique id seamless-mre to display medium rectangle banner ads (size 300x250), here is how you set the window.seamlessAds variable.
Set this variable in a script tag right before the closing of the body tag (`</body>`).

```
<script type="text/javascript">
    window.seamlessAds = [{
        adUnitId: 'AD_UNIT_ID',
        nodeId: 'seamless-banner',
        adWidth: 320,
        adHeight: 50,
        keywords: '',
        reload: true
    },
    {
        adUnitId: 'AD_UNIT_ID',
        nodeId: 'seamless-mre',
        adWidth: 300,
        adHeight: 250,
        keywords: '',
        reload: true
    }];
</script>
```

As you see there are predefined properties for each ad definition. 

- **adUnitId** => a unique hash specific both to your web site/app and ad place. This id will be delivered to you by seamless ad operations team.
- **nodeId** => the unique id of your ad place `<div>` object which this ad definition belongs. seamless.js will inject the ad into this div node.
- **adWidth** => width of the ad you want to display.
- **adHeight** => width of the ad you want to display.
- **keywords** => keywords are used for targeted ad delivery. it's optional and can be set to an empty string.
- **reload** => information about whether this ad place should refresh itself in predefined periods. default value is true.


### 3. Copy and paste seamless.js initializer

You have now ad places and ad definitions set in your document. Last step is to place the script tag to initialise seamless.js.
You can simply copy and paste the following tag into your document, again right before the closing of body tag (`</body>`). 

```
<script type="text/javascript">
    (function() {
        [
            'http://ad.mobilike.com/seamless/script/seamless.js'
        ].forEach(function(src) {
            var script = document.createElement('script');
            script.src = src;
            script.type = "text/javascript";
            script.async = false;
            var nodeBody = document.getElementsByTagName("body")[0];
            nodeBody.appendChild(script);
        });
    })();
</script>
```

That's it. Here is how the end part of your HTML document should look after following integration steps, first the ad definitions and then the initializer tag.

```
<script type="text/javascript">
    window.seamlessAds = [{
        adUnitId: 'AD_UNIT_ID',
        nodeId: 'seamless-banner',
        adWidth: 320,
        adHeight: 50,
        keywords: '',
        reload: true
    },
    {
        adUnitId: 'AD_UNIT_ID',
        nodeId: 'seamless-mre',
        adWidth: 300,
        adHeight: 250,
        keywords: '',
        reload: true
    }];
</script>
<script type="text/javascript">
    (function() {
        [
            'http://ad.mobilike.com/seamless/script/seamless.js'
        ].forEach(function(src) {
            var script = document.createElement('script');
            script.src = src;
            script.type = "text/javascript";
            script.async = false;
            var nodeBody = document.getElementsByTagName("body")[0];
            nodeBody.appendChild(script);
        });
    })();
</script>
```

## Configuration of seamless.js

There's another global variable which you can set to configure seamless.js. You may to configure seamless.js explicitly, in this case place the following script tag before the initializr tag.

seamlessJS automatically initializes the defined advertisements into `<div>` nodes that you want to insert in. However you can also define a config object to disable automatic initialization:

```
<script type="text/javascript">
    window.seamlessConfig = {
        debug: true,
        debugLevel: 'trace',
        autoInit: false
    };
</script>
```

- **debug** => default value is false. If set to true, seamless.js will output debug information to the standard console.
- **debugLevel** => may have two values, 'trace' or 'info'. default value is 'info'. 'info' level gives you standard information about the script operation, 'trace' on the other hand gives a much more detailed insight.
- **autoInit** => default value is true. seamless.js initializr tag automatically looks for windows.seamlessAds variable in the document and initializes ad display for all ad definitions in the variable. Don't set to this value to false, unless you're pursuiung a custom initialization.

## Custom initialization

In some cases you may not want to initialize every ad place at once on page load. One sample case for this would be when you have a single page web application, where your load/display cycles is custom to your design. In such a case you can init single ads explicitly whenever you want.
To accomplish this, set autoInit property of window.seamlessConfig global variable to false. This will hold seamless.js back from looking for a window.seamlessAds variable on the page and also from initializing ads automatically on page load. That means you also won't need to set window.seamlessAds global variable on your page. Instead you can use the following method to initialize an ad.
seamlessMW.initAd method needs a single argument, an object for ad definition which is the same object type described above. 

```
<script type="text/javascript">
    window.seamlessMW.initAd({
        adUnitId: 'AD_UNIT_ID',
        nodeId: 'seamless-banner',
        adWidth: 320,
        adHeight: 50,
        keywords: '',
        reload: true
    });
</script>
```

## Exchange integrations

### Google DFP

To enable DFP support on your mobile web site/app, you also need to place the following script tag before closing of the head tag (`</head>`) in your document.
seamless ad operations team will inform you if and when you need to have the following tag in your page.

```
<script type='text/javascript'>
    var googletag = googletag || {};
    googletag.cmd = googletag.cmd || [];
    (function() {
        var gads = document.createElement('script');
        gads.async = true;
        gads.type = 'text/javascript';
        var useSSL = 'https:' == document.location.protocol;
        gads.src = (useSSL ? 'https:' : 'http:') +
        '//www.googletagservices.com/tag/js/gpt.js';
        var node = document.getElementsByTagName('script')[0];
        node.parentNode.insertBefore(gads, node);
    })();
</script>
```


### Google Adsense & AdX

To enable Adsense and AdX support on your mobile web site/app, you need to use the following initializr tag in your document instead of the one given in above section "Copy and paste seamless.js initializer".
seamless ad operations team will inform you if and when you need to have the following tag in your page.

```
<script type='text/javascript'>
    (function() {
        [
            'http://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js',
            'http://ad.mobilike.com/seamless/script/seamless.js'
        ].forEach(function(src) {
            var script = document.createElement('script');
            script.src = src;
            script.type = "text/javascript";
            script.async = false;
            var nodeBody = document.getElementsByTagName("body")[0];
            nodeBody.appendChild(script);
        });
    })();
</script>
```

### Criteo Retargeting

To enable Criteo Retargeting Ads support on your mobile web site/app, first you need to provide ad definition objects with keywords set to Criteo variable. Suppose you want to enable Criteo ads for both your banner and medium rectangle ad places (following the example in integration steps section), you should have the following `window.seamlessAds` variable in your document. Notice that the only difference is the value of keywords property.

```
<script type="text/javascript">
    window.seamlessAds = [{
        adUnitId: 'AD_UNIT_ID',
        nodeId: 'seamless-banner',
        adWidth: 320,
        adHeight: 50,
        keywords: (typeof crtg_content != "undefined" && crtg_content ? crtg_content : ""),
        reload: true
    },
    {
        adUnitId: 'AD_UNIT_ID',
        nodeId: 'seamless-mre',
        adWidth: 300,
        adHeight: 250,
        keywords: (typeof crtg_content != "undefined" && crtg_content ? crtg_content : ""),
        reload: true
    }];
</script>
```

As a second step you need the have Criteo tag inserted into the `head` tag of your document. seamless ad operations team will inform you if and when you need to have Criteo implementation in your page and provide the Criteo tag.
