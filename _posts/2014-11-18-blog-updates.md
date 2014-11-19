---
layout: post
title: "Blog Updates"
description: "Site Updates"
category: "Meta"
tags: [javascript, blog-meta, web-development]
---
{% include JB/setup %}

I had promised my next blog post would be about my rendering engine, and data driven game design. Apparently I lied.

I've spent the last few days tweaking and updating this website. I added a nice colour gradient to the sidebar, I re-enabled comments and fixed the css for code syntax coloring. I wrote javascript for the first time in my life to randomly select website taglines from a pool.

The javascript was the most fun. On principle, I have avoided ever doing anything in javascript, or any web development at all. In retrospect that seems like one of the worst decisions I have ever made. I still am most interested in low level systems programming, but hacking away at Jekyll, the Liquid templates and with javascript was very entertaining, especially seeing how easy it was to pick up with zero web-dev experience.

I ended up implementing the random taglines with a single javascript function, called via <code>window.onload</code>. The function pulls a random element out of an array of taglines, provided via the Liquid Templating engine, and stored in a simple [CSV](http://en.wikipedia.org/wiki/Comma-separated_values) file within the Jekyll data directory. Sweet and Simple.

	{% highlight javascript linenos %}
	{% raw %}
	var tags = [
            {% for tagline in site.data.taglines %}
                        "{{tagline.line}}", 
                        {% endfor %}
                        "{{site.description}}"];
    {% endraw %}
    {% endhighlight %}

Now that I seemed to have tweaked the website to a decent level of polish I'll probably dive back into the rendering engine, more info on that to follow.
