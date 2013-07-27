
Introduced with Sass 3.2 placeholder selectors enable us to write better modular CSS, by extending classes which won’t be included in the compiled file. The main advantage of using placeholder selectors is the reduction of classes in your HTML __and__ CSS.

### Plain CSS

Let’s assume we want to implement a website which has tiles with different colors. Each tile has the same width, height and margin.

<pre class="language-css"><code>.tile {
	width: 200px;
	height: 200px;
	margin-right: 20px;
}</code></pre>

For having the ability of adding different colors to those tiles we add two theme classes to our tile module.

<pre class="language-css"><code>.tile-blue {
	background-color: blue;
}
.tile-red {
	background-color: red;
}</code></pre>

Using our tile classes in HTML could look like this:

<pre class="language-markup"><code>&lt;div class=&quot;tile tile-blue&quot;&gt;&lt;/div&gt;
&lt;div class=&quot;tile tile-red&quot;&gt;&lt;/div&gt;</code></pre>

### Without Placeholder Selectors

We now have two classes in our HTML one for basic tile styles and one for color. To reduce the number of classes we could simply extend `.tile` and remove it from our HTML.

<pre class="language-css"><code>.tile {
	width: 200px;
	height: 200px;
	margin-right: 20px;
}
.tile-blue {
	@extend .tile;
	background-color: blue;
}
.tile-red {
	@extend .tile;
	background-color: red;
}</code></pre>

Although we wouldn’t have to use `.tile` in our HTML anymore it would still be in our compiled CSS:

<pre class="language-css"><code>.tile, .tile-blue, .tile-red {
	width: 200px;
	height: 200px;
	margin-right: 20px;
}</code></pre>

Additionally it could be the case that we don’t want those basic tile styles used independently without a color.

### Using Placeholder Selectors

Changing the dot before a class to a percent sign tells Sass to use it as a placeholder class.

<pre class="language-css"><code>%tile {
	width: 200px;
	height: 200px;
	margin-right: 20px;
}
.tile-blue {
	@extend %tile;
	background-color: blue;
}
.tile-red {
	@extend %tile;
	background-color: red;
}</code></pre>

Finally we are able use just the theme classes in our HTML.

<pre class="language-markup"><code>&lt;div class=&quot;tile-red&quot;&gt;&lt;/div&gt;
&lt;div class=&quot;tile-blue&quot;&gt;&lt;/div&gt;</code></pre>

And our compiled CSS doesn’t contain our tile module anymore.

<pre class="language-css"><code>.tile-blue, .tile-red {
	width: 200px;
	height: 200px;
	margin-right: 20px;
}
.tile-blue {
	background-color: blue;
}
.tile-red {
	background-color: red;
}</code></pre>

To sum up placeholder classes are not included in your compiled CSS so that you can prevent developers to use those classes in their HTML or building a framework of placeholder classes which will only be included if extended by another class.

### Further Reading

[Sass Reference: Placeholder Selectors](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#placeholder_selectors_)
