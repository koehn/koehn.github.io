---
layout: post
title: Thoughts on software estimating
---

Often when I'm working at a client I get pulled into discussions about estimating; the people writing the checks want to have some idea about how much and how long, which is understandable: having an estimate from the people who are going to do the work gives one a measure, allows one to make strategic decisions about what projects to fund, and lets one monitor actual progress against the estimate. All good things.

I'll typically demure on the topic if the person asking the question isn't my project/program manager, partially because I don't want to undermine their authority, and partially because the time/money it takes to do testing, change control, etc. varies so wildly from client to client that I simply cannot take it into account. I understand pretty well how long it will take to get a piece of software written to solve a particular problem, but there's more to it than that. 

When it _is_ the project manager asking, I'll give them my best guess based on the requirements that as I understand them at the moment. 

There are three possible responses from the PM:

1. Fine. The estimate I came up with aligns well with the one they've got to work with.
2. ZOMG! How could it possibly be that much!

In the case of (2), the PM asks me why I think the estimate is so large. And then the dance begins.

So in my mind as I learn about a project I try to understand what the various changes are going to need to be, in terms of people, technology, and software. The cheapest thing to change is software, the next is technology, the most expensive are people, and you can combine them using fairly straightforward multiplication. 

    Estimate = change_of_people * change_of_technology * change_of_software

That gets you an astonishing way to a very accurate estimate of costs. So I spend a lot of time with the PM explaining the changes that I understand have to happen and their cumulative effect. Often times there are misunderstandings of the scope of the individual changes, and I'll explain how I see it and give the PM their chance to reflect on that. We can often quickly get to an agreement on the costs of changing software, but many PMs fall woefully short on understanding the impact of changing technology and people, and that's all to often what makes projects take so long: it's hard to estimate how long it will take a particular person to absorb and become productive in a new technical stack, and a key person making an error on a particular spot can quickly spend the entire budget. 

