


# PLUGIN: 

phonegap-plugin-wizViewManager



# DESCRIPTION :

PhoneGap plugin for;

creating
removing
showing
hiding
messaging (cross communication with JSON objects to each and every view)
animating views





# INSTALL (iOS): #

Project tree<br />

<pre><code>
project
	/ www
		-index.html
		-newview.html
		-json.js
		/ phonegap
			/ plugin
				/ wizViewManager
					/ wizViewManager.js	
	/ Classes
		AppDelegate.m
	/ Plugins
		/ wizViewManager
			/ wizViewManager.h
			/ wizViewManager.m
	-project.xcodeproj
</code></pre>



1 ) Arrange files to structure seen above.

2 ) Add to phonegap.plist in the plugins array;<br />
Key : wizViewManager<br />
Type : String<br />
Value : wizViewManager<br />


3 ) Configure your AppDelegate.m

See the example AppDelegate.m
(just add/copy \#import and shouldStartLoadWithRequest function)


4 ) Add \<script\> tag to your index.html<br />
\<script type="text/javascript" charset="utf-8" src="phonegap/plugin/wizViewManager/wizViewManager.js"\>\</script\><br />
(assuming your index.html is setup like tree above)
You will also need the json.js (for getting JSON objects)


5 ) Follow example code below.






# INSTALL (Android coming soon...): #



<br />
<br />
<br />
# EXAMPLE CODE : #

<br />
<br />
Creating a view<br />
<pre><code>
wizViewManager.create(String viewName, JSONObject options, Function success, Function fail);

    * Example options object; 

{

    "height": "300", [pixels - default : fills height] 
    "width": "300", [pixels - default : fills width] 
    "x": "0", [pixels - default : 0] 
    "y": "0", [pixels - default : 0] 
    "src": "http://google.com" [URL/URI to load] 

}; 
</code></pre>


Update a view<br />
<pre><code>
wizViewManager.update(String viewName, JSONObject options, Function success, Function fail);

    * Example options object; 

{

    "src": "http://google.com" [URL/URI to load] 

}; 
</code></pre>


Remove a view<br />
```
wizViewManager.remove(String viewName, Function success, Function fail); 
```


Show a view<br />
<pre><code>
wizViewManager.show(String viewName, JSONObject animOptions, Function success, Function fail);

    * Animation Types; 

slideInFromLeft - iOS
slideInFromRight - iOS
slideInFromTop - iOS
slideInFromBottom - iOS
fadeIn - iOS/Android
zoomIn - iOS/Android

    * Example animOptions object; 

animation : {

    "type": "fadeIn", [string - default : fadeIn] 
    "duration": "300", [int - default : 500] 

}; 
</code></pre>



Hide a view<br />
<pre><code>
wizViewManager.hide(String viewName, JSONObject animOptions, Function success, Function fail);

    * Animation Types; 

slideOutFromLeft - iOS
slideOutFromRight - iOS
slideOutFromTop - iOS
slideOutFromBottom - iOS
fadeOut - iOS/Android
zoomOut - iOS/Android

    * Example animOptions object; 

animation : {

    "type": "fadeOut", [string - default : fadeOut] 
    "duration": "300", [int - default : 500] 

}; 
</code></pre>

Message a view<br />
add a receiver to your html that gets the message...
<pre><code>
function wizMessageReceiver(data) 
{
                        
    // your data comes in here
    console.log('i got :' + data);
                        
}
</code></pre>

to send a messsage, add this to the html you wish to send from use...
<pre><code>
function sendExample()
{
    
    var targetView = 'newView';
    var action = 'message';
    var params = { 'x' : 500 };
    
    
    postEvent(targetView, action, params );
    
}

function postEvent(targetView, action, params) 
{
    var msg = { 'event' : action , 'params' : params };
    
    var iframe = document.createElement('IFRAME');
    iframe.setAttribute('src', 'wizMessageView://'+ window.encodeURIComponent(targetView)+ '?'+ window.encodeURIComponent(JSON.stringify(msg)) );
    document.documentElement.appendChild(iframe);
    iframe.parentNode.removeChild(iframe);
    iframe = null;
}
</code></pre>