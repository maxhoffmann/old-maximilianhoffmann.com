
The two main factors which define how fonts will look on displays are their hinting and the operating system’s rendering algorithm. That’s the reason why trying different fonts is important as well as testing them on different devices, operating systems, browsers and browser versions.

Photoshop doesn’t use the system’s font rendering and therefore text looks very differently. One could use [Sketch](http://www.bohemiancoding.com/sketch/) as an alternative, but it’s best to design in the medium itself—the browser. Style guides or new tools like [Typecast](http://typecast.com/) and [Macaw](http://macaw.co/) are great for a responsive workflow.

### Font rendering on OS X

Due to its sub-pixel antialiasing algorithm OS X tends to render light text on dark backgrounds too bold. Using icon fonts sometimes leads to more [blurry](http://people.mozilla.org/~jdaggett/tests/social-waterfall.html) rendering.

Fortunately developers can influence how browsers render text on OS X. Webkit/Chromium-based browsers offer `-webkit-font-smoothing` and  Firefox [recently added](https://bugzilla.mozilla.org/show_bug.cgi?id=857142) `-moz-osx-font-smoothing` to version 25 (currently Nightly build).

These properties switch the rendering algorithm to grayscaling, which will result in a thinner and sharper appearance of fonts. As both are non-standard I’ve created a simple mixin to normalize the syntax differences.

#### Mixin

<pre class="language-scss"><code>=font-smoothing($value: on)
    @if $value == on
        -webkit-font-smoothing: antialiased
        -moz-osx-font-smoothing: grayscale
    @else
        -webkit-font-smoothing: subpixel-antialiased
        -moz-osx-font-smoothing: auto</code></pre>

#### Usage

<pre class="language-scss"><code>.dark-on-light
    +font-smoothing(off)

.light-on-dark
    +font-smoothing(on)</code></pre>

My website also uses these properties for better rendering. If you are browsing with Firefox (version < 25) try the Nightly build or Chrome to see the difference. Keep in mind that these properties should be used as a solution and [not in general](http://www.usabilitypost.com/2012/11/05/stop-fixing-font-smoothing) as it may lead to worse results.
