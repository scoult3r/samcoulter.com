---
layout: post
title: "Distracted by Javascript"
description: "Site Updates"
category: "Meta"
tags: [javascript, blog-meta, web-development]
---
{% include JB/setup %}

Before yesterday, I had never written even a single line of javascript. It seems almost unbelievable that in 4 years of Sotware Engineering education, and another half-decade before that of teaching myself to code, I never touched the programming language responsible for the vast majority of interactive content on the internet. Always having been in love with C and its siblings, I admittedly felt a little "above" javascript and web development on the whole, which is absolutely an awful thing for any decent engineer to feel. Programming languages are tools, and only a fool ignores the right tool for the job because it "feels beneath him".

**Anyway,**

On page loading, I wanted to randomly select a tagline for this website from a pool. This <del>unfortunately</del> fortunately wasnt a default option on the jekyll config, and so I had to figure out how to do it myself. After a quick browse through the Jekyll site structure, and a little googling, the approach became obvious: a tiny embedded javascript script. Having been an avid reader of the javascript hating [proggit](http://www.reddit.com/r/programming), I expected a nightmare. I expected a dynamically typed hell. I expected random errors and no way to quickly debug them. I expected lions and tigers and crocodiles.

It was easy. The script itself is tiny, barely 3 lines. The only part that stumped me for more than a few seconds was figuring out how to wait for the html dom to load before running the script, which was actually as simple as <code>window.onload = main</code>. Even easier was using the Jekyll _data folder to *not* put my list of taglines in the layout document, and instead list them all in a nice simple CSV file, and access them with the Liquid templating engine.

	var tags = [
            {% for tagline in site.data.taglines %}
                        "{{tagline.line}}", 
                        {% endfor %}
                        "{{site.description}}"];

