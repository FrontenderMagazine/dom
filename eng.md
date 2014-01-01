# What is the DOM?

A reader recently wrote in asking me what the DOM was. They said they've heard 
it mentioned and alluded to, but aren't sure they really understand it.

We can fix that.

![Figure 1][Figure 1]

But the HTML you write is parsed by the browser and turned into the DOM.

![Figure 2][Figure 2]

View Source just shows you the HTML that makes up that page. It's probably the 
exact HTML that you wrote.

It might look like different code if, for example, you work in template files 
in a backend language and don't look at the compiled HTML output very often. Or 
there is a "build process" that happens after you write your HTML and the code 
is put out to the live website. Perhaps that HTML is compressed or otherwise 
changed.

View Source is a little weird actually. The only people that would care to look 
at that code are developers and all the major browsers have built in developer 
tools now. It has probably out-lived its usefulness.

![Figure 3][Figure 3]

When you're looking at the panel in whatever DevTools you are using that shows 
you stuff that looks like HTML, that is a visual representation of the DOM! We 
made it!

![Figure 4][Figure 4]

Well, yeah, it does. It was created directly from your HTML remember. In most 
simple cases, the visual representation of the DOM will be just like your 
simple HTML.

But it's often not the same...

## When is the DOM different than the HTML?

Here's one possibility: there are mistakes in your HTML and the browser has 
fixed them for you. Let's say you have a `<table>` element in your HTML and 
leave out the required `<tbody>` element. The browser will just insert that 
`<tbody>` for you. It will be there in the DOM, so you'll be able to find it 
with JavaScript and style it with CSS, even though it's not in your HTML.

The most likely case though, is...

## JavaScript can manipulate the DOM

Imagine you have an empty element like this in your HTML:

	<div id="container"></div>
	
Then later in your HTML, there is a bit of JavaScript:

	<script>
		var container = document.getElementById("container");
		container.innerHTML = "New Content!";
	</script>
	
Even if you don't know JavaScript, you can reason that bit of code out. On the 
screen you'll see *New Content!* rather than nothing, because that empty `div` 
was filled with some, ahem, new content.

If you use DevTools to check out the visual representation of the DOM, you'll 
see:

	<div id="container">New Content!</div>
	
Which is different than your original HTML or what you would see in View Source.

## Ajax and Templating

Let's not go off the deep end here, but I bet you can imagine if you were to 
use Ajax to snag content from elsewhere and put it onto the page, the DOM is 
going to be very different than your original HTML. The same with loading in 
data of some sort and using [client side templating][1].

Try going to Gmail and viewing source. It's just a bunch of scripts and data 
from the original page load. Barely recognizable compared to what you see on 
the screen.

## JavaScript vs. the DOM

JavaScript is a language that the browser reads and does stuff with. But the 
DOM is where that stuff happens. In fact a lot of what you might think of as a 
"JavaScript Thing" is more accurately a "DOM API".

For instance, we can write JavaScript that watches for a `mouseenter` event on 
an element. But that "element" is really a DOM node. We attach that listener 
via a DOM property on that DOM node. When that event happens, it's the DOM node 
that emits that event.

![Figure 5][Figure 5]

Appologies if I worded any of that stuff incorrectly. But you get the point I 
hope. The DOM is the lifeblood here. It's where everything goes down in the 
browser. JavaScript is just the syntax, the language. It can be used totally 
outside the browser with no DOM APIs at all (see Node.js).

## This article isn't nearly nerdy and in-depth enough for me.

Well, the DOM stands for "Document Object Model" blah blah blah. I didn't want 
to (and am not qualified) to write that article. Here's some meaty ones:

* W3C: [What is the Document Object Model?][2]
* MDN: [Introduction - Document Object Model][3]
* Wikipedia: [Document Object Model][4]

[1]: http://css-tricks.com/video-screencasts/127-basics-of-javascript-templating/
[2]: http://www.w3.org/TR/DOM-Level-2-Core/introduction.html
[3]: https://developer.mozilla.org/en-US/docs/DOM/DOM_Reference/Introduction
[4]: http://en.wikipedia.org/wiki/Document_Object_Model

[Figure 1]: img/is-html-the-dom.jpg
[Figure 2]: img/view-source-no.jpg
[Figure 3]: img/devtools-dom.jpg
[Figure 4]: img/looks-like-html.jpg
[Figure 5]: img/dom-dom-dom-dom.jpg