---
layout: post
title: THIS CHANGES EVERYTHING
---

So I'm scrolling through my twitter feed (which is actually bluesky I call bsky twitter) and I come across a [post from Nathan Lambert](https://bsky.app/profile/natolambert.bsky.social/post/3lh5jih226k2k) where he's sharing his book that he's writing on RLHF and reasoning fine tuning. And I discover [pandoc](https://pandoc.org/) and I'm like "oh shit I am going to take over the world with this". The book he's writing looks great by the way. I can't wait to read it once it's finished. I started reading it already, otherwise I wouldn't have learned about pandoc. I was impressed by the webpage and everything enough to be like hey what's the github for this.

## Pandoc

Anyway next thing you know I've gone and cloned the [pandoc book template repo](https://github.com/wikiti/pandoc-book-template) and I'm like "oh shit I am going to take over the world with THIS". Which is cool. I've got a lot of things I want to write and markdown is a simple enough format that I can just get it out of my head. Also I write code and I've become very comfortable with markdown as the basic format for all of my documentation.


So I'm `make pdf`-ing and `make html`-ing and I get to the epub format, I output an epub, and I'm like how the shit do I look at this?  

Here's something you have to understand about me. I am an avid reader. I read a lot of fucking books. Like a lot. I've read over 1000 books on kindle since 2014 and probably a 1000 more in 2004-2014 or close to it. I read a lot. 

## Foliate

So I'm looking for epub readers on linux suggestions and I find [foliate](https://github.com/johnfactotum/foliate), which is totally rad and I have a bunch of trouble installing it because I'm looking at the github page and trying to build from source with meson and it's giving me "wrong version of gjs-1.0" errors and in the process of learning all about how the version of gfs is tied to the version of ubuntu and I really really *really* need to use the flatpak, I discover gjs and builder and now I'm ready to make applications for linux and if people want to run them on windows install flatpak and if they want to run them on mac install flatpak and if they want to run them on linux install flatpak lol. 

Reason it's so exciting is I can try to find other ways to get epubs than through subscribing to kindle unlimited. The books on there are bad. I want to put together some scripts like storm except for writing books, which I can then feed to pandoc and turn into epubs and read on my laptop or my phone. I think I can find a way to read epubs on my phone besides kindle reader. Anyway I've got an epub reader for linux now and I'm stoked about it. I'm also stoked I can write epubs now too!

You might be saying "scripts like storm" what the hell is this guys talking about. Well I'm getting to that give me a damn minute. It's been an incredibly productive past few hours! I can't hardly believe it. I don't normally blog about my internet history on a Saturday night lol.

So yeah okay anyway quick recap up to this point:
- Awesome book on RLHF and fine tuning
- Pandoc
- foliate
- gfs

And now to the next part of the story.

## Storm
So I've been using this intelligent search agent in [you.com](http://you.com) that takes your query, turns it into several other better, more coherent queries that are interelated, then generates a bunch of wikipedia articles about the queries before responding to your original question. I'm impressed by this and I work in the LLM system space so I decide to try out the [storm](https://github.com/stanford-oval/storm) locally. I tried the online demo when it first came out and thought it was awesome but I was still under the impression that Search API access was limited to a few companies and people had to pay for it. Pay well for it. I was wrong. I'm looking through the storm code at the various retrieval models and SearXNG stood out to me. Like if this was corporate they'd probably choose something that actually rolls of the tongue. Anyway, **SearXNG**:

## SearXNG

Oh my goodness I couldn't be happier finding SearXNG. Took me a minute figuring out how to change the settings.yaml so I could get the json responses that storm was looking for and it took 100 seconds for storm to get the results, but I was able to get it to work. Now I have a local search engine instance running on my laptop that I can access programmatically. I think I'm going to have to say this again because I didn't really understand how big of a deal it is/was/is going to be.

| **I** | **Have** | **A** | **Local** | **Search** | **Engine** | **I** | **Can** | **Programmatically** | **Access** |
| **Have**               | *AM*| | | | | | | | |
| **A**                  | | *GOING*| | | | | | | |
| **Local**              | | | *TO*| | | | | | |
| **Search**            | | | |*TAKE* | | | | | |
| **Engine**           | | | | |*OVER* | | | | |
| **I**                  | | | | | |*THE* | | | |
| **Can**                | | | | | | | *WORLD* | | |
| **Programmatically**   | | | | | | | | *WITH*| |
| **Access**             | | | | | | | | | *THIS*|

So I set it up as my default search engine in firefox and now I don't feel like I am contributing to the psychological profile google is building and constantly refining on me like I'm one of those people who work at Area 51 and can't use the internet to find answers to their questions lol. My idea about doing tons of queries to bury what I'm actually interested in is all the more feasible now, especially since I want to use it programmatically for my projects anyway.

Seems like there's a lot of low hanging fruit to be had just by having an LLM read scientific articles and fill out a knowledge graph. Find contradictions. Synthesize possible solutions and explanations. Fill in the gaps. Huge dark areas of understanding buried in the literature.

## OpenWebUI
I realize after I'm adding SearXNG as my default search engine in firefox that I can probably use it in [OpenWebUI](https://openwebui.com/) and even though the search results weren't that great, I was able to add search to my locally hosted open source chatbot. So talking about gaps in the literature. Consider github the literature and you can see how this type of thing can be useful. Find some way to add the two together where you're searching for gaps in the literature and gaps in the knowledge graph of scientific understanding and you can link that to github and find actionable ways to address the gaps with PRs and novel development. Part of any research article is writing a bunch of code and going through the steps and you know the whole grad student/researcher experience. Automate it and turn it loose. Turn a thousand of them loose and have them work together. Check in with them constantly. Make it into a platform. Open source it all. Let people contribute compute like foldit or seti. Federate it.

That's the kind of thing I'm working on. I'm not just thinking about it any more. I have SearXNG as my default search engine. I'm working on it.

So yeah I'm doing great. I've been saying I'm doing great and dammit if I'm not doing even better than I was before when I was just like "you know everyone else is not feeling so hot and I get that but I'll be god damned if I let the bastards steal my sunshine. My joy is an act of rebellion." and holy fucking shit I've been doing great since then. Y'all should try it.

Sack clothe and ashes solves nothing.
