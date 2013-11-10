# Placeholder Selectors

## 14th of February, 2013

Introduced with Sass 3.2 placeholder selectors enable us to write better modular <abbr>CSS</abbr> by extending classes, which won’t be included in the compiled file. The main advantage of using placeholder selectors is the reduction of classes in your <abbr>HTML</abbr> __and__ <abbr>CSS</abbr>.

### Plain CSS

Let’s assume we want to implement a website, which has tiles with different colors. Each tile has the same width, height and margin.

<pre class="language-scss"><code>.tile {
	width: 200px;
	height: 200px;
	margin-right: 20px;
}</code></pre>

For the ability to add different colors to the tiles we included two theme classes in our <abbr>CSS</abbr>.

<pre class="language-scss"><code>.tile-blue {
	background-color: blue;
}
.tile-red {
	background-color: red;
}</code></pre>

The corresponding markup could look like this:

<pre class="language-markup"><code>&lt;div class=&quot;tile tile-blue&quot;&gt;&lt;/div&gt;
&lt;div class=&quot;tile tile-red&quot;&gt;&lt;/div&gt;</code></pre>

### Without Placeholder Selectors

We’ve added two classes to the tile element: one for basic tile styles and one for the color. To reduce the number of classes we could simply extend `.tile` and remove it from our <abbr>HTML</abbr>.

<pre class="language-scss"><code>.tile {
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

Although we wouldn’t have to use the `.tile` class in our markup anymore, it would still be in our compiled <abbr>CSS</abbr>:

<pre class="language-scss"><code>.tile, .tile-blue, .tile-red {
	width: 200px;
	height: 200px;
	margin-right: 20px;
}</code></pre>

To save some bytes or to prevent other developers from using the basic tile class without a color, we could also remove it from the compiled <abbr>CSS</abbr>.

### Using Placeholder Selectors

Changing the dot before a class to a percent sign tells Sass to use it as a placeholder class.

<pre class="language-scss"><code>%tile {
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

Now we just need to use our theme classes.

<pre class="language-markup"><code>&lt;div class=&quot;tile-red&quot;&gt;&lt;/div&gt;
&lt;div class=&quot;tile-blue&quot;&gt;&lt;/div&gt;</code></pre>

And our compiled <abbr>CSS</abbr> doesn’t contain the basic tile class anymore.

<pre class="language-scss"><code>.tile-blue, .tile-red {
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

To sum up placeholder classes are not included in your compiled <abbr>CSS</abbr> so that you can prevent developers from using those classes in their <abbr>HTML</abbr>. It is also possible to build a framework solely out of placeholder classes, which will only be added to the compiled <abbr>CSS</abbr> if developers extend them.

### Further Reading

[Sass Reference: Placeholder Selectors](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#placeholder_selectors_)
