---
layout: post
title: "Humble Beginnings"
description: "First Post"
category: "Thoughts"
tags: [reddit, professional, blog-meta]
---
{% include JB/setup %}

So I finally redesigned my website and started a blog. 

I was ultimately inspired to do so after reading [a post](http://www.reddit.com/r/programming/comments/2lyeqc/larry_pages_java_question_1996_every_journey/) on [proggit](http://www.reddit.com/r/programming) that has since exploded to over 700/3000 comments/upvotes. 

I'm currently looking for my first post-graduation position and I think every soon-to-be engineering grad feels some *anxiety* during that job search, even if they do have a few successful internships under their belt.

<!--more-->

Now, I don't quite have the ego to consider myself a [Larry Page](https://groups.google.com/forum/#!msg/comp.lang.java/aSPAJO05LIU/ushhUIQQ-ogJ), [Linus Torvolds](https://groups.google.com/forum/#!msg/comp.os.minix/dlNtH7RRrGA/SwRavCzVE7gJ), or [Vladimir Kajalin](https://groups.google.com/forum/m/#!topic/comp.graphics.api.opengl/_MslsWO7LL0), but it is still incredibly comforting to see that a few giants left some footprints small enough for my feet.


**Anyway, lets talk about the blog.**

I decided to go with a minimilistic Jekyll generated static site hosted on github pages. It makes it pretty easy for me to write new posts, and mess around with drafts/site changes all from the comfort of the command line and with the protection of one of my favourite tools, [git branching models](http://nvie.com/posts/a-successful-git-branching-model/). Setting up the custom domain name (blog.samcoulter.com <==> scoult3r.github.io) proved to be pretty easy by following the github pages tutorial for it, but the ~24 hours in-between making the DNS changes and actually getting my blog to show up at the new domain was infuriating. My generation is of instant gratification. 

Speaking of, I'm planning to spend the next week getting started on the 'Data Driven'*ness* of the game engine I'm writing. I'll be [streaming it](http://www.twitch.tv/akzever), as apparently there is a small number of people that like watching me tinker around with C++/OpenGL, and in the next week YAML parsing. The plan is to get a simple graphics material/shader/scene loading system set up, so I can start adding in rendering features without having to re-compile all the time. Instant shader and material updates with a single key-press? Sounds awesome.

My next post will probably be all about YAML parsing and the gory details of trying to write a robust 2d Rendering system without actually knowing all the features a 2d rendering system might need, aka the joys of newbie gamedev.

**Edit:** My fantastic partner Sarah pointed out that I should probably explain the tentative name of the blog/site "Systems in the Rain". Simply put: I enjoy systems (embedded/real time/networking etc etc) programming, and it rains a lot in the beautiful city of Vancouver. I actually think I'm going to implement a random selector from a pool of phrases for the site tagline, seems like it would be a fun hack to experiment with ruby/Jekyll, and I know I'll get bored of one name/tagline pretty darn quickly.