Progressive enhancement is fortunately a highly discussed topic in the web community again, thanks to talented people like [Jeremy Keith](http://adactio.com/journal/6246/), [Jake Archibald](http://jakearchibald.com/2013/progressive-enhancement-still-important/http://www.youtube.com/watch?v=li4Y0E_x8zE) and [Nicholas Zakas](http://www.youtube.com/watch?v=li4Y0E_x8zE). Enhancing the user’s experience progressively means essential interactions work without JavaScript, for example if it is loading or doesn’t work, due to bugs or other causes.

Today I wanted to test how some of the biggest social networks progressively enhance their interactions. The most common functionalities of social networks are simple <abbr>CRUD</abbr> operations and authentication: consuming content, posting content, logging in, logging out and navigating to different pages. This is basic stuff and can be easily done with `forms`, <abbr>GET</abbr>/<abbr>POST</abbr> requests and links. As it turns out the most essential functionality is broken if you turn off JavaScript.

### Results

<a href="/images/JavaScriptNetworks.png" class="image-inline"><img src="/images/JavaScriptNetworks.png" title="Social Networks without JavaScript statistic"></a>

This graphic shows which interactions work without JavaScript and if a warning is displayed by the network when the user has turned it off. Yellow ticks in the "consume" column mean that you only have access to the first page of content because infinite scroll is broken. The yellow tick in Youtube’s row means that you can only navigate your feed if you are already logged in.

The most surprising fact to me is that you can’t post something on any of these social networks without JavaScript. There always is a textbox, but you either don’t have any button or the button doesn’t work.

<a href="/images/facebook-no-button.png" class="image-inline"><img src="/images/facebook-no-button.png" title="facebook’s input field without a button"></a>

Some interesting quirks I’ve found are that Youtube’s preview images need JavaScript otherwise you just get grey boxes and that twitter’s wrong password page requires JavaScript too. If you misstype your password you’ll get redirected to another page, which again has a login form, but in contrast to the first one, does not work without <abbr>JS</abbr>.

<a href="/images/gray-youtube.png" class="image-inline"><img src="/images/gray-youtube.png" title="Youtube without preview images"></a>

I also had some problems after testing twitter. Apparently twitter thinks bots run without <abbr>JS</abbr>, so I had to login again with a captcha. Unfortunately the captcha service seems to be broken, as I couldn’t solve it—or maybe I’m not human enough. After several desperate attempts I tried the audio version. Seriously, have you ever tried the audio version of a captcha? Listen for yourself:

<p class="text-centered"><audio src="/files/captcha.mp3" controls></audio><a href="/files/captcha.mp3">captcha.mp3</a></p>

I guess that’s why ReCaptcha’s slogan is: "stop spam. read books.", which translates to: "Hey you, spammer! Stop posting content on the internet and read a book!". The following image is one of the captchas I had to solve. As you can see the image on the left clearly shows a number.

<a href="/images/captcha.png" class="image-inline"><img src="/images/captcha.png" title="captcha that can not be solved"></a>

Back to topic: The bottom line is that everything that breaks on these socials networks does not require JavaScript. Using links with `href` pointing to a valid <abbr>URL</abbr> will enable users to browse your website. Using `form` elements and a server will allow users to post content. Using pagination users may browse a stream of content. Building a web applications doesn’t always mean building a JavaScript applications. I want to end this post with a tweet by Mat Marquis.

> "Webapp (n.): Website where the developers responsible wanted to require JavaScript."<br>
> — [@wilto](https://twitter.com/wilto/statuses/372080088898367488)