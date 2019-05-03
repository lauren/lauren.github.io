---
id: 1026
title: Building software at Etsy
date: 2016-02-25T16:01:52+00:00
author: Lauren Sperber
excerpt: A presentation on the culture of engineering at Etsy, given at CareerZoo in Dublin in February 2016.
layout: post
guid: http://www.laurensperber.com/?p=1026
permalink: /2016/02/25/presentation-building-software-at-etsy/
dsq_thread_id:
  - "4610567459"
image: /wp-content/uploads/2016/02/cover-1.jpg
categories:
  - internet
  - projects
  - software development
tags:
  - public speaking
comments: true
---
Last week I had the pleasure of traveling to Etsy&#8217;s Dublin office to speak at [CareerZoo](http://www.careerzoo.ie/), which is a large career fair. I gave two presentations about Etsy&#8217;s work culture: One called [&#8220;Crafting an Empowering Environment,&#8221;](/2016/02/29/crafting-an-empowering-environment/) which I&#8217;ll publish next week, and this one, which I titled &#8220;Building Software at Etsy.&#8221;

Huge thanks to [Lara Hogan](http://larahogan.me/), [Moishe Lettvin](http://www.moishelettvin.com/), [Ian Malpass](http://indecorous.com), [Jeremy Pharo](https://twitter.com/jeremypharo), [Russ Posluszny](http://www.russposluszny.com/), and [Stefanie Schirmer](http://linse.me/) for their feedback on early drafts of this talk, and to [Jennifer Butler](http://twitter.com/jennbc), [Tara Hayes](http://twitter.com/tarasianhayes), [Lara Hogan](http://larahogan.me/) (again!), and [Michael Rembetsy](http://twitter.com/mrembetsy) for providing the opportunities and support I needed to give it.

I illustrated my slides with photos from the shops of Irish Etsy sellers, whose work you&#8217;ll see in the transcript below with links to their shops.

#### [See the slides](https://www.slideshare.net/kenspeckle/building-software-at-etsy)



## Transcript

_The opinions expressed are mine and do not necessarily reflect those of Etsy. All stats referenced are valid as of September 30, 2015._

Hi everyone! My name is Lauren Sperber and I’m a senior software engineer at Etsy. If you’re not familiar with Etsy, we’re an online marketplace where people connect to buy and sell unique handmade and vintage goods. We help 1.5 million active sellers make a living by providing a platform that helps them run their creative small businesses.

I’m going to tell you about the culture of engineering at Etsy and shared values that enable our engineers to work together productively and happily. I’ll start by giving you an overview of my daily work life and then sharing the principles of Etsy engineering that help me work this way.

### How I Work

<img src="/images/2016/02/4-dumbo-office-cropped-1024x655.jpg" alt="working in the Etsy office" width="1024" height="655" class="alignnone size-large wp-image-1039" srcset="/images/2016/02/4-dumbo-office-cropped-1024x655.jpg 1024w, /images/2016/02/4-dumbo-office-cropped-300x192.jpg 300w, /images/2016/02/4-dumbo-office-cropped-768x491.jpg 768w" sizes="(max-width: 1024px) 100vw, 1024px" />

There are two main types of programming work at Etsy. Product engineering directly affects the features that buyers and sellers see on Etsy.com and our mobile apps, while infrastructure engineering creates the underlying architecture that product engineers work on. I mainly do product engineering work, so I’ll give you a sense of what the daily work of a product engineer looks like.

[<img src="/images/2016/02/il_fullxfull.780761086_40e2-1024x1024.jpg" alt="a ceramic celtic knot" width="1024" height="1024" class="alignnone size-large wp-image-1040" srcset="/images/2016/02/il_fullxfull.780761086_40e2-1024x1024.jpg 1024w, /images/2016/02/il_fullxfull.780761086_40e2-150x150.jpg 150w, /images/2016/02/il_fullxfull.780761086_40e2-300x300.jpg 300w, /images/2016/02/il_fullxfull.780761086_40e2-768x768.jpg 768w, /images/2016/02/il_fullxfull.780761086_40e2.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" />](https://www.etsy.com/shop/CelticValleyCeramics)

<div class="caption">
  <a href="https://www.etsy.com/shop/CelticValleyCeramics">by CelticValleyCeramics</a>
</div>

Every programmer at Etsy has a “Virtual Machine,” which is our own personal version of Etsy.com. It has all the same code as the real thing, but uses test data instead of the real data that our buyers and sellers are using to do business. I edit code on my Virtual Machine and make sure it works the way I’m hoping. Once I have finished the smallest part of the feature I’m making, such as an API endpoint to supply the data, or a controller to call the endpoint and send the data to views, I make a small commit.

When I’ve made a few small commits that together create a feature or resolve a bug, I make a pull request on GitHub and email it to the programmers on my team. My coworkers comment on the pull request with suggestions or questions and I continue pushing commits based on their comments to the review branch until we all feel good about the changes.

Next, I run our automated tests to make sure my changes didn’t mistakenly affect other areas of the site. Testing your code isn&#8217;t formally required at Etsy, but there is cultural motivation to do so. These tests aren’t comprehensive, but they ensure that the main features of Etsy still work after my change. They also verify I haven’t made any syntax errors that my coworkers might not have spotted in the code review.

[<img src="/images/2016/02/il_fullxfull.669538094_94u5-1024x768.jpg" alt="small Irish flags" width="1024" height="768" class="alignnone size-large wp-image-1041" srcset="/images/2016/02/il_fullxfull.669538094_94u5-1024x768.jpg 1024w, /images/2016/02/il_fullxfull.669538094_94u5-300x225.jpg 300w, /images/2016/02/il_fullxfull.669538094_94u5-768x576.jpg 768w, /images/2016/02/il_fullxfull.669538094_94u5.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" />](https://www.etsy.com/shop/ooakie)

<div class="caption">
  <a href="https://www.etsy.com/shop/ooakie">from ooakie</a>
</div>

A little background: Etsy has more features on it than anyone—even people who work for Etsy—can see at a given time. We have a configuration system in which we keep an array of all the the features whose availability we want to be able to control easily, including features that are still under development. 

My new code will be hidden behind a feature flag, so it’s unlikely that any buyers or sellers will be affected by my change. This configuration setup allows us to deploy our code as soon as it’s written and tested&mdash;a working style commonly called “continuous deployment.” Since we have about 200 programmers continuously deploying, the website gets updated more than 40 times a day!

To organize the many programmers trying to deploy at any given time, we use IRC, which is a group chat program. We have a channel called “Push” that creates a queue for us to deploy in groups. The first person in each deploy group is in charge of driving their push. If that person is you, you’ll simply click a button to deploy the code to our staging environment, which is called “Princess.” Princess has the same code and data as Etsy.com, but is hosted by a separate server, so we can test our new code there without affecting all of Etsy’s users.

Once we’ve all confirmed our changes on Princess and the automated tests pass, the push driver presses another button to deploy to the production site. We check our code there and watch the error logs and graphs until we’re sure that we haven’t caused any unexpected issues. Once the driver declares the push complete, the next group can deploy.

[<img src="/images/2016/02/il_fullxfull.747194166_gvvg-1024x663.jpg" alt="pencil case made of fabric printed with beakers and test tubes" width="1024" height="663" class="alignnone size-large wp-image-1043" srcset="/images/2016/02/il_fullxfull.747194166_gvvg-1024x663.jpg 1024w, /images/2016/02/il_fullxfull.747194166_gvvg-300x194.jpg 300w, /images/2016/02/il_fullxfull.747194166_gvvg-768x497.jpg 768w, /images/2016/02/il_fullxfull.747194166_gvvg.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" />](https://www.etsy.com/shop/TheCuriousNeedle)

<div class="caption small">
  <a href="https://www.etsy.com/shop/TheCuriousNeedle">by TheCuriousNeedle</a>
</div>

Once my team has developed a new feature enough to see how it works for our sellers, we have two main options for finding out how it works. One is creating a “prototype group” of sellers who we ask to test out the new feature and let us know how it works for them. This is helpful for getting qualitative feedback from our top sellers, who can leave the group if the revised feature isn’t working for them. Developing a new feature collaboratively with sellers in a prototype group helps us deepen their engagement with Etsy and often they help us evangelize the new feature to other sellers as it gets released to more people. The other option is to turn on new features for a small percentage of users to see how they affect rates of viewing, favoriting, purchasing, and other important metrics. This is helpful for getting quantitative feedback on how the changes affect users’ behavior on the site. 

After validating that a new feature has improved the experience for our buyers or sellers, we’ll make it available for all users, but continue to improve on it based on feedback and data.

### Etsy’s Engineering Practices

Now that I’ve given you a sense of how product engineers build and release new features for Etsy, I want to talk about some of the major practices for building software at Etsy. The first two are deeper looks at some daily practices I mentioned in my overview of my daily work life.

#### Code Reviews

[<img src="/images/2016/02/il_fullxfull.648386817_s0lk-1024x762.jpg" alt="illustration of a cat reading a book" width="1024" height="762" class="alignnone size-large wp-image-1044" srcset="/images/2016/02/il_fullxfull.648386817_s0lk-1024x762.jpg 1024w, /images/2016/02/il_fullxfull.648386817_s0lk-300x223.jpg 300w, /images/2016/02/il_fullxfull.648386817_s0lk-768x571.jpg 768w, /images/2016/02/il_fullxfull.648386817_s0lk.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" />](https://www.etsy.com/shop/Victorianaprint)

<div class="caption small">
  <a href="https://www.etsy.com/shop/Victorianaprint">from Victorianaprint</a>
</div>

I send almost every line of code I write out to my coworkers in a pull request on GitHub. Even if I make a one-line change to a feature flag configuration, I try to get at least one set of eyes on it before deploying so that there’s a chance for someone to catch a non-fatal typo or logical error. This is super easy to do by creating a GitHub gist of the change and pasting it in our team IRC channel.

For more significant change sets, such as creating a new API endpoint or a new set of controllers and views, the code review is even more important.

<img src="/images/2016/02/6-virtual-machine.gif" alt="gif of a woman laughing evilly at a pink laptop" class="rightpic" />

##### Reduce Ego

There’s no single correct solution to any programming problem, especially within an environment as complex as Etsy’s very large ten-year-old code base. By inviting my teammates to collaborate on my code, I’m working to ensure that the code I push out is the best overall solution for the problem I’m trying to solve, not just the one that I thought of first, or the one that I thought was the most clever.

##### Reduce Cleverness

Code reviews have an enormous impact in reducing excessive cleverness in code. One of the issues I look for when doing a code review for a coworker is any time I have to stop, scratch my head, and re-read the code to figure out what it’s doing. This is a possible indicator that the code could be simplified, or could use re-use existing tools in our codebase.

<img src="/images/2016/02/16-readability.gif" alt="gif of Scully from the X-Files reading a book about aliens" class="rightpic" />

##### Increase Readability

Code gets written once and read many, many times over by other programmers looking to track down the source of a bug or add functionality to an existing feature. Code reviews help to ensure that classes, methods, and variables are named with an eye to long-term clarity. If the reviewer doesn’t understand what I meant with a variable name, there&#8217;s no way that the next person to read it will either—even if that next person is myself in a few months. Reviewers also often suggest opportunities to introduce type hints and comments to further clarify what the code is intending to do.

##### Increase Awareness

Perhaps the most important benefit of code reviews is increasing communal awareness of the code. If I’ve read the code that my teammates wrote carefully before they push it, I have more context to debug it if something goes wrong later, or to work with it to add new features.

Reading my colleagues’ code consistently also helps me learn how my other programmers approach problems and expands the breadth of ideas at my disposal.

#### Continuous Deployment

[<img src="/images/2016/02/il_fullxfull.677069120_fx4x-1024x768.jpg" alt="silkscreen print of knuckles tattooed with the words 'just ship'" width="1024" height="768" class="alignnone size-large wp-image-1047" srcset="/images/2016/02/il_fullxfull.677069120_fx4x-1024x768.jpg 1024w, /images/2016/02/il_fullxfull.677069120_fx4x-300x225.jpg 300w, /images/2016/02/il_fullxfull.677069120_fx4x-768x576.jpg 768w, /images/2016/02/il_fullxfull.677069120_fx4x.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" />](http://laughingmeme.org/)

<div class="caption small">
  <a href="http://laughingmeme.org/">by Kellan Elliott-McCrea</a>
</div>

As I mentioned earlier, I deploy code as I’ve gotten a code review and run integration tests. The live site is usually deployed more than 40 times a day. 

If you’ve never worked this way, updating a site with millions of dollars in sales per day that frequently might sound a bit terrifying, but deploying so often actually helps us keep the website stable.

<img src="/images/2016/02/14-code-review.gif" alt="animated gif of Moss from The IT Crowd working while his desk is on fire" width="640" height="360" class="alignright size-full wp-image-1048" />

##### Reduce Fear

I personally update Etsy.com between 1 and 5 times per day, so it’s a normal part of my work day. Since I do it so frequently, I don’t feel nearly as nervous as I might when deploying another website that changes less frequently.

##### Reduce Risk

If something goes wrong, either due to a deployment or an unexpected situation, we can push a fix out for it almost as soon as we have it ready. Since the changesets we deploy are relatively small and contained, it&#8217;s easier to detect if something&#8217;s gone wrong without QAing the entire site.

<img src="/images/2016/02/confidence.gif" alt="animated gif of Beyonce flipping her hair" class="rightpic" />

##### Increase Experience

Since all of our programmers deploy frequently, there are a lot of people who know how to help if something goes wrong.

##### Increase Confidence

By pushing out the smallest possible changes as frequently as possible, we ensure that our changes have a limited range of impact and are easy to test.

#### Architecture Reviews

[<img src="/images/2016/02/il_fullxfull.892542903_sm7l-1024x639.jpg" alt="il_fullxfull.892542903_sm7l" width="1024" height="639" class="alignnone size-large wp-image-1064" srcset="/images/2016/02/il_fullxfull.892542903_sm7l.jpg 1024w, /images/2016/02/il_fullxfull.892542903_sm7l-300x187.jpg 300w, /images/2016/02/il_fullxfull.892542903_sm7l-768x479.jpg 768w" sizes="(max-width: 1024px) 100vw, 1024px" />](https://www.etsy.com/shop/DublinStreet)

<div class="caption small">
  <a href="https://www.etsy.com/shop/DublinStreet">by DublinStreet</a>
</div>

The next two engineering practices I&#8217;ll discuss are higher-level practices that take place less frequently than code reviews and deployment. The first is Architecture Reviews. When a group of engineers feels that they need to implement a new architecture that departs in a significant way from existing technology or processes, they document their proposed design, highlighting the goals, trade-offs, and rejected alternatives, then hold workshops with other engineers from across the company to get feedback on the proposal. After the submitting engineers feel confident in their proposal, they hold an Architecture Review meeting that is open to all engineers at the company. Those proposing the new architecture present for only 10 minutes and allow 50 minutes of questions and answers from other engineers.

<img src="/images/2016/02/novelty.gif" alt="animated gif of a cat chasing a laser toy" class="rightpic" />

##### Reduce Novelty

By going through this process for every new architectural decision, we ensure that we use the most simple and well-known solution unless there is no other option. We avoid switching technologies purely because they are interesting or exciting.

##### Reduce Ego

As with code reviews, the collaborative nature of the architecture review process helps to transform the proposal of a technical design from the work of a single engineer or group thereof and into the collaborative output of a larger group working to create the best solution for our buyers and sellers regardless of their personal interests.

<img src="/images/2016/02/cat-reading.gif" alt="animated gif of a cat reading a book on military strategy" class="rightpic" />

##### Increase Perspectives

By making the Architecture Review open to engineers across the company, we encourage participation from a variety of programmers, including those not directly affected by the proposed new technology. This helps the team embarking on a new project get fresh perspectives on their problem that they wouldn’t otherwise have access to.

##### Increase Awareness

Much like the daily practice of code reviews, architecture reviews ensure that engineers across Etsy know about how different parts of our technology stack work and why those decisions were made. 

#### Blameless Post-Mortems

[<img src="/images/2016/02/il_fullxfull.797221886_o8xm-1024x1024.jpg" alt="embroidered tombstone" width="1024" height="1024" class="alignnone size-large wp-image-1053" srcset="/images/2016/02/il_fullxfull.797221886_o8xm-1024x1024.jpg 1024w, /images/2016/02/il_fullxfull.797221886_o8xm-150x150.jpg 150w, /images/2016/02/il_fullxfull.797221886_o8xm-300x300.jpg 300w, /images/2016/02/il_fullxfull.797221886_o8xm-768x768.jpg 768w, /images/2016/02/il_fullxfull.797221886_o8xm.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" />](https://www.etsy.com/shop/TrashMagic)

<div class="caption small">
  <a href="https://www.etsy.com/shop/TrashMagic">TrashMagic</a>
</div>

The final engineering practice I&#8217;ll discuss is Blameless Post-Mortems. Even though we have so many ways to check our work, things still go wrong at Etsy. After any incident that caused a substantial negative impact on Etsy’s website, apps, or developer time, we hold a Blameless Post-Mortem open to everyone at the company in which a trained facilitator reviews a timeline of the decisions and actions that led to the incident as well as the troubleshooting and rectification of the incident that followed. Once a clear timeline is established, the facilitator asks all involved why they believed their decisions and actions were correct at the time, in order to establish gaps in knowledge or tooling that could be corrected in the future.

<img src="/images/2016/02/fear.gif" alt="animated gif of a cat going bonkers" class="rightpic" />

##### Reduce Fear

Going into the post-mortem, all participants acknowledge that everyone involved in the incident is competent and intended to do the best thing for Etsy and our buyers and sellers. The aim of the post-mortem is to learn why their well-intentioned actions and decisions led to an incident and how we could improve our tooling or processes when similar circumstances arise in the future. This attitude, summarized in the adjective “Blameless,” helps those involved in an outage feel confident that their jobs or competence are not in question.

##### Reduce Repeated Incidents

Having an honest discussion about what beliefs or daily routines led to the outage helps us to identify processes or tools that should be improved to prevent similar incidents from happening in the future. We&#8217;ll never completely eliminate repeated incidents, but taking the time to look into why an outage occurred definitely helps us to reduce our chances of making the same mistake again.

<img src="/images/2016/02/learning.gif" alt="animated gif of information entering a human brain" class="rightpic" />

##### Increase Learning

By discussing the timeline and possible remediation items from an incident in an open setting, we demystify the exact details of what might otherwise turn into a legendary internal horror story that everyone laughs at but that doesn&#8217;t help us learn how to improve our tools and processes. This openness about outages spreads awareness about previously unknown risks and situations to others who may be in a similar situation in the future.

### Etsy’s Engineering Principles

Those are four of the key Engineering practices at Etsy: Code Reviews, Continuous Deployment, Architecture Reviews, and Blameless Post-Mortems. I want to leave you with the key principles that I take away from these practices and from my daily work at Etsy. These shared values guide us to make decisions that are best for our buyers and sellers and the long-term stability of our platform.

#### Empowering Trust

[<img src="/images/2016/02/il_fullxfull.905092584_2ilh-768x1024.jpg" alt="painting of an angel" width="768" height="1024" class="alignnone size-large wp-image-1056" srcset="/images/2016/02/il_fullxfull.905092584_2ilh-768x1024.jpg 768w, /images/2016/02/il_fullxfull.905092584_2ilh-225x300.jpg 225w, /images/2016/02/il_fullxfull.905092584_2ilh.jpg 1125w" sizes="(max-width: 768px) 100vw, 768px" />](https://www.etsy.com/shop/SarahMurphyInspires)

<div class="caption small">
  <a href="https://www.etsy.com/shop/SarahMurphyInspires">SarahMurphyInspires</a>
</div>

Etsy aims to empower the engineers working on a particular project to make the technical decisions necessary to its implementation. This definitely doesn’t mean that we can do “whatever we want”—in fact, we have to work very hard to convince our peers of the validity of any new technology in an architecture review—but it does mean that we’re empowered to propose and justify the technical design that we want to see for our project, rather than having architectural decisions made by engineering leaders and passed down to engineers to implement.

#### Collaborative Accountability

[<img src="/images/2016/02/il_fullxfull.786268850_dc1p-1024x1024.jpg" alt="wax painting of two women" width="1024" height="1024" class="alignright size-large wp-image-1057" srcset="/images/2016/02/il_fullxfull.786268850_dc1p-1024x1024.jpg 1024w, /images/2016/02/il_fullxfull.786268850_dc1p-150x150.jpg 150w, /images/2016/02/il_fullxfull.786268850_dc1p-300x300.jpg 300w, /images/2016/02/il_fullxfull.786268850_dc1p-768x768.jpg 768w, /images/2016/02/il_fullxfull.786268850_dc1p.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" />](https://www.etsy.com/shop/LittleWaxyArtSpace)

<div class="caption small">
  <a href="https://www.etsy.com/shop/LittleWaxyArtSpace">by LittleWaxyArtSpace</a>
</div>

Through code reviews and architecture reviews, Etsy engineers work collaboratively to come to technical decisions. Although I may have written the initial code, the contributions that my colleagues make through questions and suggestions on a code review make the code better by reducing the risk that I’ve introduced a bug or logical error and by ensuring that it’s easy to understand for the next person who needs to read and maintain it. Although my colleague may have written the initial design documentation for a new piece of architecture, critiques from a working group lead to an informed decision about whether or not to move forward with it. By collaborating on the design and implementation of technical decisions, we develop a shared accountability for the outcomes of our projects.

#### Continuous Learning

[<img src="/images/2016/02/il_fullxfull.860309167_bab9.jpg" alt="il_fullxfull.860309167_bab9" width="570" height="570" class="alignnone size-full wp-image-1058" srcset="/images/2016/02/il_fullxfull.860309167_bab9.jpg 570w, /images/2016/02/il_fullxfull.860309167_bab9-150x150.jpg 150w, /images/2016/02/il_fullxfull.860309167_bab9-300x300.jpg 300w" sizes="(max-width: 570px) 100vw, 570px" />](https://www.etsy.com/shop/ThingsWeLeftBehind)

<div class="caption small">
  <a href="https://www.etsy.com/shop/ThingsWeLeftBehind">by ThingsWeLeftBehind</a>
</div>

In addition to continuous deployment, engineers at Etsy informally practice what I like to call &#8220;continuous learning.&#8221; Although we’re all considered “full-stack” engineers, meaning that we work on server- and client-side code, we naturally have our own special niches of the code base—or about programming in general—that we know more about

When I encounter a new part of the technology stack, I strive to ask as many questions as possible so that I have a complete understanding of how something works. I inevitably find thorough and enthusiastic answers from my colleagues that help me feel confident in my understanding, and also good about having asked. In turn, when someone else asks a question in an IRC channel or a meeting, I welcome the opportunity to share my knowledge.

It would be a big cultural _faux pas_ at Etsy to express surprise that a questioner did not know the answer or to otherwise mock them for their question. This readiness to learn and teach in equal measure makes it fun and easy to continue to expand my skills and knowledge.

#### Good Lookin’ Out

[<img src="/images/2016/02/looking-out.jpg" alt="looking-out" width="420" height="274" class="alignnone size-full wp-image-1059" srcset="/images/2016/02/looking-out.jpg 420w, /images/2016/02/looking-out-300x196.jpg 300w" sizes="(max-width: 420px) 100vw, 420px" />](https://www.etsy.com/shop/ModelsAndCraftShop)

<div class="caption small">
  <a href="https://www.etsy.com/shop/ModelsAndCraftShop">from ModelsAndCraftShop</a>
</div>

In addition to helping each other learn through informal questions in IRC and meetings, Etsy engineers strive to look out for each other. This means that we read each other’s code carefully in a code review and ask thoughtful and critical questions. It also means that we double- and triple-check commit history and error logs for each other while deploying, and alert our colleagues to errors that pertain to their products or tools.

Engineers also help anyone in a non-technical role at Etsy who’s interested write the code to add their picture to our About page and deploy it to the website. We call this collaboration the First Push Program. It helps to build the same trust and empathy shared amongst engineers across teams. [Katie Rose Crosswhite](https://twitter.com/ktrose), who manages our twice-weekly catered lunch, called Eatsy, was so impressed by the trust and support she saw in the Push queue that she said, “I had no idea how much engineers have each other’s backs.” 

### Conclusion

These four principles—empowering trust, collective accountability, continuous learning, and looking out for each other—help our programmers work productively by minimizing our fear of being judged negatively for not knowing something about our code base or making a mistake. Missteps are actively embraced as part of the ongoing process of learning and innovation.

<img src="/images/2016/02/3as-1024x524.png" alt="screenshot of etsy's error page featuring an illustration of a woman knitting a sweater with three arms" width="1024" height="524" class="alignnone size-large wp-image-1060" srcset="/images/2016/02/3as-1024x524.png 1024w, /images/2016/02/3as-300x154.png 300w, /images/2016/02/3as-768x393.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" />

In fact, each year we even celebrate the incident in which one of our engineers caused the most surprising unintended consequences while trying to improve our technology with an award that we call the Three-Armed Sweater after this adorable illustration on our error page. This annual reflection on the previous year’s learnings reminds us that we must take risks to keep our product and technology moving forward, and that unintended consequences of these calculated risks are worthwhile if we analyze their causes and learn from them rather than covering them up from fear of retribution. 

My colleague [Ian Malpass](http://indecorous.com) has spoken of the balance we strive for as one of “calculated risk.” Fear of change would keep us from making forward progress, while reckless behavior would destabilize our service and cost us time and cost us money, time, and the trust of our buyers and sellers. Our sellers rely on our Etsy for income, so we have to be extremely careful to not jeopardize their success, because our success comes from their success. A calculated risk is one in which we&#8217;ve done the work to consider the ways in which our plan could fail, worked to mitigate those, and then put in place practices that allow us to recover if the unexpected happens.

The space we have for honest analysis of failures, combined with our sense of empowerment to suggest the solution that we think will be most effective, allows engineers at Etsy feel true ownership of our work take responsibility for maintaining it when requirements or circumstances change in the future. Perhaps most importantly, we also feel accountability for our colleagues’ work and professional growth. Adding to our peers’ knowledge and improving processes and tools for all engineers helps us to build a better environment for ourselves others, and, most importantly, a better platform for our sellers and buyers.

##### My work:

  * [public speaking](/tag/public-speaking/)

##### Links: 

  * [slides](https://www.slideshare.net/kenspeckle/building-software-at-etsy)