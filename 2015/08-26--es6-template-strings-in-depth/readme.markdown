<sub>&#x1F6A8; <strong>Autogenerated!</strong> See <a href="https://github.com/ponyfoo/articles/tree/noindex/contributing.markdown"><code>contributing.markdown</code></a> for details. See also: <a href="https://ponyfoo.com/articles/es6-template-strings-in-depth">web version</a>.</sub>

<a href="https://ponyfoo.com/articles/es6-template-strings-in-depth"><div></div></a>

<h1>ES6 Template Literals in Depth</h1>

<p><kbd>es6</kbd> <kbd>template-literals</kbd> <kbd>es6-in-depth</kbd></p>

<blockquote><p>Yesterday we&#x2019;ve covered <a href="https://ponyfoo.com/articles/es6-destructuring-in-depth">ES6 destructuring in depth</a>, as well as some of its most common use cases. Today we&#x2019;ll be moving to <strong>template literals</strong>. What they &#x2026;</p></blockquote>

<div><p>Yesterday we&#x2019;ve covered <a href="https://ponyfoo.com/articles/es6-destructuring-in-depth">ES6 destructuring in depth</a>, as well as some of its most common use cases. Today we&#x2019;ll be moving to <strong>template literals</strong>. What they are, and how we can use them and what good they&#x2019;re for.</p></div>

<blockquote></blockquote>

<div><p>Template literals are a new feature in ES6 to make working with strings and string templates easier. You wrap your text in <code class="md-code md-code-inline">`backticks`</code> and you&#x2019;ll get the features described below.</p> <ul> <li>You can interpolate variables in them</li> <li>You can actually interpolate using <em>any kind of expression</em>, not just variables</li> <li>They can be <strong>multi-line</strong>. <em>Finally!</em></li> <li>You can construct <em>raw templates</em> that don&#x2019;t interpret backslashes</li> </ul> <p>In addition, you can also define <em>a method</em> that will decide what to make of the template, instead of using the default templating behavior. There are some interesting use cases for this one.</p> <blockquote> <p>Let&#x2019;s dig into template literals and see what we can come up with.</p> </blockquote></div>

<div><h2 id="using-template-literals">Using Template Literals</h2> <p>We&#x2019;ve already covered the basic <em><code class="md-code md-code-inline">`I&apos;m just a string`</code></em>. One aspect of template literals that may be worth mentioning is that you&#x2019;re now able to declare strings with both <code class="md-code md-code-inline">&apos;</code> and <code class="md-code md-code-inline">&quot;</code> quotation marks in them without having to escape anything.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript">var text = `I&apos;m &quot;amazed&quot; that we have so many quotation marks to choose from!`
</code></pre> <p>That was neat, but surely there&#x2019;s more useful stuff we can apply template literals to. How about some <em>actual interpolation</em>? You can use the <code class="md-code md-code-inline">${expression}</code> notation for that.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> host = <span class="md-code-string">&apos;ponyfoo.com&apos;</span>
<span class="md-code-keyword">var</span> text = `<span class="md-code-keyword">this</span> blog lives at <mark class="md-mark md-code-mark">${host}</mark>`
<span class="md-code-built_in">console</span>.log(text)
<span class="md-code-comment">// &lt;- &apos;this blog lives at ponyfoo.com&apos;</span>
</code></pre> <p>I&#x2019;ve already mentioned you can have any kind of expressions you want in <mark class="md-mark">there</mark>. Think of whatever expressions you put in there as defining a variable before the template runs, and then concatenating that value with the rest of the string. That means that variables you use, methods you call, and so on, should all be available to the current scope.</p> <p>The following expressions would all work just as well. It&#x2019;ll be up to us to decide how much logic we cram into the interpolation expressions.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> text = `<span class="md-code-keyword">this</span> blog lives at ${<span class="md-code-string">&apos;ponyfoo.com&apos;</span>}`
<span class="md-code-built_in">console</span>.log(text)
<span class="md-code-comment">// &lt;- &apos;this blog lives at ponyfoo.com&apos;</span>
</code></pre> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> today = <span class="md-code-keyword">new</span> <span class="md-code-built_in">Date</span>()
<span class="md-code-keyword">var</span> text = `the time and date is ${today.toLocaleString()}`
<span class="md-code-built_in">console</span>.log(text)
<span class="md-code-comment">// &lt;- &apos;the time and date is 8/26/2015, 3:15:20 PM&apos;</span>
</code></pre> <pre class="md-code-block"><code class="md-code md-lang-javascript">import moment from <span class="md-code-string">&apos;moment&apos;</span>
<span class="md-code-keyword">var</span> today = <span class="md-code-keyword">new</span> <span class="md-code-built_in">Date</span>()
<span class="md-code-keyword">var</span> text = `today is the ${moment(today).format(<span class="md-code-string">&apos;Do [of] MMMM&apos;</span>)}`
<span class="md-code-built_in">console</span>.log(text)
<span class="md-code-comment">// &lt;- &apos;today is the 26th of August&apos;</span>
</code></pre> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> text = `such ${<span class="md-code-literal">Infinity</span>/<span class="md-code-number">0</span>}, very uncertain`
<span class="md-code-built_in">console</span>.log(text)
<span class="md-code-comment">// &lt;- &apos;such Infinity, very uncertain&apos;</span>
</code></pre> <p>Multi-line strings mean that you no longer have to use methods like these anymore.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> text = (
  <span class="md-code-string">&apos;foo\n&apos;</span> +
  <span class="md-code-string">&apos;bar\n&apos;</span> +
  <span class="md-code-string">&apos;baz&apos;</span>
)
</code></pre> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> text = [
  <span class="md-code-string">&apos;foo&apos;</span>,
  <span class="md-code-string">&apos;bar&apos;</span>,
  <span class="md-code-string">&apos;baz&apos;</span>
].join(<span class="md-code-string">&apos;\n&apos;</span>)
</code></pre> <p>Instead, you can now just use backticks! Note that spacing matters, so you might still want to use parenthesis in order to keep the first line of text away from the variable declaration.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> text = (
`foo
bar
baz`)
</code></pre> <p>Multi-line strings really shine when you have, <em>for instance</em>, a chunk of HTML you want to interpolate some variables to. Much like with <a href="https://ponyfoo.com/articles/react-jsx-and-es6-the-weird-parts" aria-label="React, JSX and ES6: The Weird Parts on Pony Foo">JSX</a>, you&#x2019;re perfectly able to use an expression to iterate over a collection and <code class="md-code md-code-inline">return</code> yet another template literal to declare list items. This makes it a breeze to declare sub-components in your templates. Note also how I&#x2019;m <a href="https://ponyfoo.com/articles/es6-destructuring-in-depth" aria-label="ES6 JavaScript Destructuring in Depth on Pony Foo">using destructuring</a> to avoid having to prefix every expression of mine with <code class="md-code md-code-inline">article.</code>, I like to think of it as <em>&#x201C;a <code class="md-code md-code-inline">with</code> block, but not as insane&#x201D;</em>.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> article = {
  title: <span class="md-code-string">&apos;Hello Template Literals&apos;</span>,
  teaser: <span class="md-code-string">&apos;String interpolation is awesome. Here are some features&apos;</span>,
  body: <span class="md-code-string">&apos;Lots and lots of sanitized HTML&apos;</span>,
  tags: [<span class="md-code-string">&apos;es6&apos;</span>, <span class="md-code-string">&apos;template-literals&apos;</span>, <span class="md-code-string">&apos;es6-in-depth&apos;</span>]
}
<span class="md-code-keyword">var</span> {title,teaser,body,tags} = article
<span class="md-code-keyword">var</span> html = `&lt;article&gt;
  <span><span class="md-code-tag">&lt;<span class="md-code-title">header</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">h1</span>&gt;</span>${title}<span class="md-code-tag">&lt;/<span class="md-code-title">h1</span>&gt;</span>
  <span class="md-code-tag">&lt;/<span class="md-code-title">header</span>&gt;</span>
  <span class="md-code-tag">&lt;<span class="md-code-title">section</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">div</span>&gt;</span>${teaser}<span class="md-code-tag">&lt;/<span class="md-code-title">div</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">div</span>&gt;</span>${body}<span class="md-code-tag">&lt;/<span class="md-code-title">div</span>&gt;</span>
  <span class="md-code-tag">&lt;/<span class="md-code-title">section</span>&gt;</span>
  <span class="md-code-tag">&lt;<span class="md-code-title">footer</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">ul</span>&gt;</span>
      <mark class="md-mark md-code-mark">${tags.map(tag =&gt; `<span class="md-code-tag">&lt;<span class="md-code-title">li</span>&gt;</span>${tag}<span class="md-code-tag">&lt;/<span class="md-code-title">li</span>&gt;</span>`).join(&apos;\n      &apos;)}</mark>
    <span class="md-code-tag">&lt;/<span class="md-code-title">ul</span>&gt;</span>
  <span class="md-code-tag">&lt;/<span class="md-code-title">footer</span>&gt;</span>
<span class="md-code-tag">&lt;/<span class="md-code-title">article</span>&gt;</span>`
</span></code></pre> <p>The above will produce output as shown below. Note how the spacing trick was enough to properly indent the <code class="md-code md-code-inline">&lt;li&gt;</code> tags.</p> <pre class="md-code-block"><code class="md-code md-lang-xml"><span class="md-code-tag">&lt;<span class="md-code-title">article</span>&gt;</span>
  <span class="md-code-tag">&lt;<span class="md-code-title">header</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">h1</span>&gt;</span>Hello Template Literals<span class="md-code-tag">&lt;/<span class="md-code-title">h1</span>&gt;</span>
  <span class="md-code-tag">&lt;/<span class="md-code-title">header</span>&gt;</span>
  <span class="md-code-tag">&lt;<span class="md-code-title">section</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">div</span>&gt;</span>String interpolation is awesome. Here are some features<span class="md-code-tag">&lt;/<span class="md-code-title">div</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">div</span>&gt;</span>Lots and lots of sanitized HTML<span class="md-code-tag">&lt;/<span class="md-code-title">div</span>&gt;</span>
  <span class="md-code-tag">&lt;/<span class="md-code-title">section</span>&gt;</span>
  <span class="md-code-tag">&lt;<span class="md-code-title">footer</span>&gt;</span>
    <span class="md-code-tag">&lt;<span class="md-code-title">ul</span>&gt;</span>
      <span class="md-code-tag">&lt;<span class="md-code-title">li</span>&gt;</span>es6<span class="md-code-tag">&lt;/<span class="md-code-title">li</span>&gt;</span>
      <span class="md-code-tag">&lt;<span class="md-code-title">li</span>&gt;</span>template-literals<span class="md-code-tag">&lt;/<span class="md-code-title">li</span>&gt;</span>
      <span class="md-code-tag">&lt;<span class="md-code-title">li</span>&gt;</span>es6-in-depth<span class="md-code-tag">&lt;/<span class="md-code-title">li</span>&gt;</span>
    <span class="md-code-tag">&lt;/<span class="md-code-title">ul</span>&gt;</span>
  <span class="md-code-tag">&lt;/<span class="md-code-title">footer</span>&gt;</span>
<span class="md-code-tag">&lt;/<span class="md-code-title">article</span>&gt;</span>
</code></pre> <p>Raw templates are the same in essence, you just have to prepend your template literal with <code class="md-code md-code-inline">String.raw</code>. This can be very convenient in some use cases.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript">var text = String.raw`The &quot;\n&quot; newline won&apos;t result in a new line.
It&apos;ll be escaped.`
console.log(text)
// The &quot;\n&quot; newline won&apos;t result in a new line.
// It&apos;ll be escaped.
</code></pre> <p>You might&#x2019;ve noticed that <code class="md-code md-code-inline">String.raw</code> seems to be a special part of the template literal syntax, and you&#x2019;d be right! The method you choose will be used to parse the template. Template literal methods &#x2013; called <em>&#x201C;tagged templates&#x201D;</em> &#x2013; receive an array containing a list of the static parts of the template, as well as each expression on their own variables.</p> <p>For instance a template literal like <code class="md-code md-code-inline">`hello ${name}. I am ${emotion}!`</code> will pass arguments to the <em>&#x201C;tagged template&#x201D;</em> in a function call like the one below.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript">fn([<span class="md-code-string">&apos;hello &apos;</span>, <span class="md-code-string">&apos;. I am&apos;</span>, <span class="md-code-string">&apos;!&apos;</span>], <span class="md-code-string">&apos;nico&apos;</span>, <span class="md-code-string">&apos;confused&apos;</span>)
</code></pre> <p>You might be confused by the seeming oddity in which the arguments are laid out, but they start to make sense when you think of it this way: for every item in the template array, there&#x2019;s an expression result after it.</p> <h2 id="demystifying-tagged-templates">Demystifying Tagged Templates</h2> <p>I wrote an example <code class="md-code md-code-inline">normal</code> method below, and it works <em>exactly like the default behavior</em>. This might help you better understand what happens under the hood for template literals.</p> <blockquote> <p>If you don&#x2019;t know what <code class="md-code md-code-inline">.reduce</code> does, refer to <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce" target="_blank" aria-label="Array.prototype.reduce() &#x2013; MDN">MDN</a> or my <a href="https://ponyfoo.com/articles/fun-with-native-arrays#computing-with-reduce-reduceright" aria-label="Computing with .reduce, .reduceRight on Pony Foo">&#x201C;Fun with Native Arrays&#x201D;</a> article. Reduce is always useful when you&#x2019;re trying to map a collection of values into a single value that can be computed from the collection.</p> </blockquote> <p>In this case we can reduce the <code class="md-code md-code-inline">template</code> starting from <code class="md-code md-code-inline">template[0]</code> and then reducing all other parts by adding the preceding <code class="md-code md-code-inline">expression</code> and the subsequent <code class="md-code md-code-inline">part</code>.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-function"><span class="md-code-keyword">function</span> <span class="md-code-title">normal</span> <span class="md-code-params">(template, <mark class="md-mark md-code-mark">...expressions</mark>)</span> </span>{
  <span class="md-code-keyword">return</span> template.reduce((accumulator, part, i) =&gt; {
    <span class="md-code-keyword">return</span> accumulator + expressions[i - <span class="md-code-number">1</span>] + part
  })
}
</code></pre> <p>The <code class="md-code md-code-inline">...expressions</code> syntax is new in ES6 as well. It&#x2019;s called the <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/rest_parameters" target="_blank" aria-label="Rest parameters in ES6 &#x2013; MDN"><em>&#x201C;rest parameters syntax&#x201D;</em></a>, and it&#x2019;ll basically place all the arguments passed to <code class="md-code md-code-inline">normal</code> that come after <code class="md-code md-code-inline">template</code> into a single array. You can try the tagged template as seen below, and you&#x2019;ll notice you get the same output as if you omitted <code class="md-code md-code-inline">normal</code>.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-keyword">var</span> name = <span class="md-code-string">&apos;nico&apos;</span>
<span class="md-code-keyword">var</span> outfit = <span class="md-code-string">&apos;leather jacket&apos;</span>
<span class="md-code-keyword">var</span> text = <mark class="md-mark md-code-mark">normal</mark>`hello ${name}, you look lovely today <span class="md-code-keyword">in</span> that ${outfit}`
<span class="md-code-built_in">console</span>.log(text)
<span class="md-code-comment">// &lt;- &apos;hello nico, you look lovely today in that leather jacket&apos;</span>
</code></pre> <p>Now that we&#x2019;ve figured out how tagged templates work, what can we do with them? Well, whatever we want. One possible use case might be to make user input uppercase, turning our greeting into something that sounds more satirical &#x2013; <em>I read the result out loud in my head with Gob&#x2019;s voice from Arrested Development, now I&#x2019;m laughing alone. I&#x2019;ve made a huge mistake</em>.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript"><span class="md-code-function"><span class="md-code-keyword">function</span> <span class="md-code-title">upperExpr</span> <span class="md-code-params">(template, ...expressions)</span> </span>{
  <span class="md-code-keyword">return</span> template.reduce((accumulator, part, i) =&gt; {
    <span class="md-code-keyword">return</span> accumulator + expressions[i - <span class="md-code-number">1</span>].toUpperCase() + part
  })
}
<span class="md-code-keyword">var</span> name = <span class="md-code-string">&apos;nico&apos;</span>
<span class="md-code-keyword">var</span> outfit = <span class="md-code-string">&apos;leather jacket&apos;</span>
<span class="md-code-keyword">var</span> text = <mark class="md-mark md-code-mark">upperExpr</mark>`hello ${name}, you look lovely today <span class="md-code-keyword">in</span> that ${outfit}`
<span class="md-code-built_in">console</span>.log(text)
<span class="md-code-comment">// &lt;- &apos;hello NICO, you look lovely today in that LEATHER JACKET&apos;</span>
</code></pre> <p>There&#x2019;s obviously much more useful use cases for tagged templates than laughing at yourself. In fact, you could go crazy with tagged templates. A decidedly useful use case would be to sanitize user input in your templates automatically. Given a template where all expressions are considered user-input, we could use <a href="https://github.com/bevacqua/insane" target="_blank" aria-label="bevacqua/insane on GitHub"><code class="md-code md-code-inline">insane</code></a> to sanitize them out of HTML tags we dislike.</p> <pre class="md-code-block"><code class="md-code md-lang-javascript">import insane from &apos;insane&apos;
function sanitize (template, ...expressions) {
  return template.reduce((accumulator, part, i) =&gt; {
    return accumulator + <mark class="md-mark md-code-mark">insane</mark>(expressions[i - 1]) + part
  })
}
var comment = &apos;haha xss is so easy <mark class="md-mark md-code-mark">&lt;iframe src=&quot;http://evil.corp&quot;&gt;&lt;/iframe&gt;</mark>&apos;
var html = <mark class="md-mark md-code-mark">sanitize</mark>`&lt;div&gt;${comment}&lt;/div&gt;`
console.log(html)
// &lt;- &apos;&lt;div&gt;haha xss is so easy &lt;/div&gt;&apos;
</code></pre> <p><em>Not so easy now!</em></p> <blockquote> <p>I can definitely see a future where the only strings I use in JavaScript begin and finish with a backtick.</p> </blockquote></div>
