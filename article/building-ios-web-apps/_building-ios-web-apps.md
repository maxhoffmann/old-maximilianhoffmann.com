# Building iOS Web Apps

#### 22nd of February

## Web Inspector
Remote debugging web applications is available since iOS6. With remote debugging it is easy to check and alter the rendered CSS and test the functionality of your app on the device itself. Instead of Safari I recommend you to use the latest [Nightly WebKit](http://nightly.webkit.org/), which has more features and a better interface. Changes to WebKit’s developer tools since Safari 6 can be found [here](https://gist.github.com/paulmillr/4056234).

To enable developer tools on your computer go to __Preferences > Advanced__ in Webkit/Safari and check the box next to “Show Develop menu in menu bar”.

<a href="/images/AdvancedSettings.png" class="image-inline"><img src="/images/AdvancedSettings.png"></a>
On your mobile device go to __Settings > Safari > Advanced__ and toggle the Web Inspector there.

<a href="/images/ios_web_inspector.png" class="image-inline"><img src="/images/ios_web_inspector.png"></a>
Afterwards you can connect the device with your computer using a __cable__. If you have opened a website on mobile Safari, its desktop counterpart should now list your device in its develop menu including your open tabs. Clicking on one of these should open the developer tools for the selected website.

## Local Web Server

While developing your application it is useful to see changes instantly and without the need of a server. That’s why I recommend you to install and start [MAMP](http://www.mamp.info/). This application allows you to choose a folder, which will be displayed at `http://localhost` and at your IP address on mobile devices if they are in the same wireless network as your computer. To find your computer’s IP go to __System Preferences > Network__. It will probably look like 192.168.0.X therefore you should be able to open the web app from your device at `http://192.168.0.X`. For instant updates when saving a file you can use tools like [LiveReload](http://livereload.com/).

## Hiding Safari’s chrome

Users have always the ability to add websites to their homescreen, but If you want to hide Safari’s chrome after they have added yours, you need to include this meta tag:

<pre class="language-markup"><code>&lt;meta name=&quot;apple-mobile-web-app-capable&quot; content=&quot;yes&quot;&gt;</code></pre>

## Zooming and Viewports

On websites users may pinch to zoom at anytime anywhere, but this shouldn’t be possible for web apps in most cases. This meta tag disables zooming with gestures and sets the viewport to its ”default” value:

<pre class="language-markup"><code>&lt;meta name=&quot;viewport&quot; content=&quot;user-scalable=no, initial-scale=1&quot;&gt;</code></pre>

I have to admit that “default value” is not quite right as viewport is a larger topic, but you can read more about it on [Apple’s Safari Web Content Guide](http://developer.apple.com/library/ios/#documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html#//apple_ref/doc/uid/TP40006509-SW1).

##  Status bar options

The status bar above your web app is black by default on iOS6. You may change this to black translucent, but keep in mind that this will add 20px and 40px on retina screens respectively to your app’s height.

<pre class="language-markup"><code>&lt;meta name=&quot;apple-mobile-web-app-status-bar-style&quot; content=&quot;black-translucent&quot;&gt;</code></pre>

## Your app’s name

If a user wants to add your site to his homescreen, Safari uses the webpage's title as a suggestion for the name of your web app. Since iOS6 you can suggest another name:

<pre class="language-markup"><code>&lt;meta name=&quot;apple-mobile-web-app-title&quot; content=&quot;My Web App&quot;&gt;</code></pre>

In both cases it is just a proposal and users will always be able to define another name.

## Icon sizes

By default iOS uses a screenshot of your website as icon for the web app. You can set your own by appending a `link` tag to your website with the `rel` attribute of “apple-touch-icon”.  As there are different screen resolutions across Apple’s devices you can define an icon for each of them, but iOS is also able to scale icons down (or even up). This means you can define an icon for the retina iPad, which has the size of 144 by 144 pixels and it will work on every other device for example an iPhone 3G. I prefer defining one icon for each retina device and leave standard displays behind as retina will be everywhere. So if your web app will work on both iPhone and iPad, make and include both in retina sizes. If it’s intended to work on iPhone only like [doubbble](http://doubbble.com), include just the retina iPhone icon. To tell iOS which icon it should use if both options are available, give it a hint with the `sizes` attribute. Example:

<pre class="language-markup"><code>&lt;!-- iPhone Retina --&gt;
&lt;link rel=&quot;apple-touch-icon-precomposed&quot; sizes=&quot;114x114&quot; href=&quot;apple-touch-icon-114x114-precomposed.png&quot;&gt;

&lt;!-- iPad Retina --&gt;
&lt;link rel=&quot;apple-touch-icon-precomposed&quot; sizes=&quot;144x144&quot; href=&quot;apple-touch-icon-144x144-precomposed.png&quot;&gt;</code></pre>

You may leave out the `link` tags if your icons are stored in your website’s root directory and start with ”apple-touch-icon-...”, but as there are some Android devices using theses tags too, it is possible that it won’t work for them. In the example I’ve also added __precomposed__ to the icon’s name and the `rel` attribute of the `link` tag. This tells iOS not to overlay its default glossy gradient over your icons. For further information about naming conventions have a look at [Apple’s Guide](http://developer.apple.com/library/ios/#documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html#//apple_ref/doc/uid/TP40002051-CH3-SW4).

## Startup image

As for native apps you have the ability to display an image when the user starts your web app. [doubbble](http://doubbble.com) for example displays an image of its initial screen so that the first start of the app feels much faster. A startup image is always the size of the device’s resolution minus the status bar. iPads can have one startup image for portrait mode and one for landscape mode whereas iPhone web apps will always start in portrait mode. Furthermore iOS doesn’t scale startup images. You have to include images for every device you support with the correct dimensions to work. Additionally startup images in landscape mode have to be saved in portrait mode rotated 90 degrees clockwise. According to the `media` attribute of the `link` tags iOS applies the matching image. A full list with every possible startup image definition can be found on this [gist](https://gist.github.com/tfausak/2222823). The code is pretty heavy if you support a broad range of devices, but it’s easy and short if you just support iPhone 5 and iPhone 4 for example:

<pre class="language-markup"><code>&lt;!-- iPhone 4 --&gt;
&lt;link rel=&quot;apple-touch-startup-image&quot; href=&quot;images/iphone4.png&quot; media=&quot;(device-height:480px)&quot;&gt;

&lt;!-- iPhone 5 --&gt;
&lt;link rel=&quot;apple-touch-startup-image&quot; href=&quot;images/iphone5.png&quot; media=&quot;(device-height:568px)&quot;&gt;</code></pre>

Image dimension of startup images for iPhone 4/4S is 640x920 and for iPhone 5 it’s 640x1096.

## Writing the first lines

Taking everything into account I have written an `index.html` for the dribbble feed viewer:

<pre class="language-markup"><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
	&lt;meta charset=&quot;utf-8&quot;&gt;
	&lt;meta name=&quot;viewport&quot; content=&quot;user-scalable=no,initial-scale=1&quot;&gt;
	&lt;meta name=&quot;apple-mobile-web-app-capable&quot; content=&quot;yes&quot;&gt;
	&lt;meta name=&quot;apple-mobile-web-app-title&quot; content=&quot;my web app&quot;&gt;
	&lt;link rel=&quot;apple-touch-icon-precomposed&quot; href=&quot;apple-touch-icon-114x114-precomposed.png&quot;&gt;
	&lt;link rel=&quot;apple-touch-startup-image&quot; href=&quot;images/iphone4.png&quot; media=&quot;(device-height:480px)&quot;&gt;
	&lt;link rel=&quot;apple-touch-startup-image&quot; href=&quot;images/iphone5.png&quot; media=&quot;(device-height:568px)&quot;&gt;
	&lt;title&gt;Install dribbble feed viewer&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;h1&gt;Welcome buddy!&lt;/h1&gt;
	&lt;p&gt;Add this site to your homescreen to install the dribbble feed viewer.&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

I have uploaded the complete code with images to [github](https://github.com/maxhoffmann/ios-web-apps). After adding this site to your homescreen it should look like this:

<a href="/images/icon.jpg" class="image-inline"><img src="/images/icon.jpg"></a>

## Questions?

Is anything unclear to you or have you found grammatical errors due to the fact that I am not a native speaker? I’d value your feedback on this article on [Branch](http://branch.com/b/building-ios-web-apps-part-1-maximilian-hoffmann/invite_link/m7YHa4NJhx7Mzw).