---
layout: post
title: The Monkey's Paw of Scheduling
subtitle: Why is it so hard to automate your work?
description: What's the deal with scheduling code?
tags: [python, orchestration, automation, scheduling]
thumbnail-img: /assets/img/bart-paw.png
share-img: /assets/img/bart-paw.png
comments: false
---
In the short story [The Monkey’s Paw](https://en.wikipedia.org/wiki/The_Monkey%27s_Paw), a couple come into possession of a preserved monkey’s paw with magical powers. After the couple makes a wish, the wish comes true - but with terrible consequences. The phrase “the monkey’s paw curls” has entered popular culture, notably driven by an appearance in a [Simpson’s Tree House of Horrors episode](https://simpsons.fandom.com/wiki/Monkey%27s_Paw). The phrase has taken on the meaning of having a wish come true, with unforeseen negative consequences.

![Bart Simpson and the Monkey's Paw](/assets/img/bart-paw.png)

Somebody used this phrase to me in reference to workflow orchestration the other day, and that really resonated with me, so I thought I’d explore it.

## People writing python

Python is ridiculously ubiquitous at this point - the [number one programming language](https://www.tiobe.com/tiobe-index/) globally as of the writing of this piece. Maybe I’m biased (I do work in the PyData ecosystem), but it seems like everybody and their cousin are writing scripts these days.

I started writing python initially in 2011, when I was scraping gambling odds from sportsbooks in order to find arbitrage (1). I used Windows Task Scheduler to schedule that scraping. It was running on my laptop, and it broke all the time. I was being rate limited, APIs were poorly documented and changing constantly, my laptop was off, etc.

The audience of python-literate people who want to automate their work is also large. There are an infinite number of python scripts holding together personal projects, small companies, and enterprises. 

## Everybody wants to set it and forget it

![Set it and forget it!](/assets/img/ronco.png)

The allure of automation is strong. I ******really****** wanted my gambling project to succeed - it would be free money! I also barely cared about it, but I was determined to automate it fully. I turned to cron, but AWS was nascent and my spare desktop computer had recently died in a freak drink spilling accident. Unfortunately, I gave up and the world will never know of the free money loop.

All of the little python engineers out there (or even the advanced ones) want to take the process that they’ve abstracted into code, and put that code on a schedule so they **********************************never have to think about it again**********************************. They soon come to learn that scheduling is the monkey’s paw.

## Be careful what you wish for

> There is no such thing as a free lunch.

-Pankaj Agrrawal, my professor from 2007 in my Finance 350 course at the University of Maine

Every user that tries to schedule something, soon learns that scheduling was just the beginning of their woes. 

### Infra

Remember those errors I talked about with my gambling odds script? Imagine what it would have taken to get that running on remote infrastructure somewhere. Now imagine trying to configure the exact type of infra that a script runs on. Good luck, person who just learned python!

Also, because of infra, you had better ship your shit in a container or else you’re going to have a bad time (and you’ll probably have a bad time, anyway).

### Time

In the real world, things change all the time. APIs, schema, versions, security, products are killed, products are born, the world marches on. In the period of a couple of weeks I experienced change negatively impacting my script. Imagine what a year looks like (Pydantic v2 anyone?).

### Dependencies & relationships

Oh, the thing you want to schedule relies on some undefined payload from Bovada and it changes all the time? Maybe the team name has a character you weren’t expecting in it? That’s going to fail and you’re going to have to figure out why.

### Just knowing what the hell is up

Speaking of failure, good luck knowing when or why the thing you scheduled even failed

## Orchestration is the treatment, not the disease

The monkey’s paw of scheduling wasn’t obvious to me, even after I encountered it. This is the whole reason for orchestration tools (heads up: I work at Prefect), which help deal with these unavoidable problems that you may have simplified away in your own head.

That’s just what they are, though: unavoidable. Scheduling is a hard problem because of everything else that it takes to make something run, not because of the schedule itself. The question you should be asking is not, “can I schedule this?”. Instead, the question should be, “do I have what it takes to make this thing bulletproof and visible?”.

1: Sidenote: arbitrage was out there, but I assessed transaction risk to be too high

{: .box-note}
**What was I listening to when writing this?**
<br>
[Depeche Mode - Policy of Truth](https://www.youtube.com/watch?v=M2VBmHOYpV8&pp=ygUcZGVwZWNoZSBtb2RlIHBvbGljeSBvZiB0cnV0aA%3D%3D)
