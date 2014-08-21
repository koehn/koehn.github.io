---
layout: essay
title: On software estimating
---

Often when I’m working at a client I get pulled into discussions about estimating; the people writing the checks want to have some idea about how much and how long, which is understandable: having an estimate from the people who are going to do the work gives one a measure, allows one to make strategic decisions about what projects to fund, and lets one monitor actual progress against the estimate. All good things.

I’ll typically demure on the topic if the person asking the question isn’t my project/program manager, partially because I don’t want to undermine their authority, and partially because the time/money it takes to do testing, change control, etc. varies so wildly from client to client that I simply cannot take it into account. I understand pretty well how long it will take to get a piece of software written to solve a particular problem, but there’s more to it than that.

When it _is_ the project manager asking, I’ll give them my best guess based on the requirements that as I understand them at the moment.

There are three possible responses from the PM:

1. Fine. The estimate I came up with aligns well with the one they’ve got to work with.
2. ZOMG! How could it possibly be that much!

In the case of (2), the PM asks me why I think the estimate is so large. And then the dance begins.

So in my mind as I learn about a project I try to understand what the various changes are going to need to be, in terms of people, technology, and software. The cheapest thing to change is software, the next is technology, the most expensive are people, and you can combine them using fairly straightforward multiplication.

    Estimate = change_of_people * change_of_technology * change_of_software

That gets you an astonishingly quick way to a very accurate estimate of costs. So I spend a lot of time with the PM explaining the changes that I understand have to happen and their cumulative effect. Often times there are misunderstandings of the scope of the individual changes, and I’ll explain how I see it and give the PM their chance to reflect on that. We can often quickly get to an agreement on the costs of changing software, but many PMs fall woefully short on understanding the impact of changing technology and people, and that’s all to often what makes projects take so long: it’s hard to estimate how long it will take a particular person to absorb and become productive in a new technical stack, and a key person making an error on a particular spot can quickly spend the entire budget.

The other data that must go along with estimates is risk. If there’s one thing that’s habitually misunderstood in software engineering (disproportionately to other engineering disciplines) it’s risk. Nobody likes risk and nobody wants to talk about it, and I think that’s because risk represents to some people a loss of control, which is antithetical to estimating. But things don’t always work out the way we’d like, and the things we can think of that might reasonably not turn out the way we’d like are captured as risks.

Very often a client wants to see a highly-detailed project plan, especially when the bill is much higher than they’d like. This is a psychological response to a desire for more control in the face of an unforeseen cost. The thinking being something like, “if I cannot get this project to fit within the original scope, at least I can make it survive additional scrutiny!” This mode of thinking is, by and large, desperate. If you’ve asked for an opinion from someone, there’s an implicit trust given to that person’s opinion; if you come back and demand a more detailed estimate you’re saying to that person, “I don’t think I believe you as much as I did originally.” What kind of message is that? If you’d like my reasoning, let’s talk it out and I’ll explain it to you, but the additional detail written into some template isn’t going to communicate anything to anybody: if I was hiding something in my original estimate that you didn’t like, how much easier will it be to hide it in a long, drawn-out document based on some template?

The project plan brings up the notion of value of an estimate:

	value = accuracy / cost

That is to say, the more your estimate costs without increasing accuracy, the less valuable it is. Now, when you’re asked to justify your estimate by filling in a form or providing some other secondary analysis, given the covert message about trust we discussed earlier, how likely are you to change your estimate? People will naturally rationalize their initial estimate into the new medium. Now all they’ve done is increased the cost of their estimate, thereby decreasing its value.

But let’s say you’re a really honest, rational actor who isn’t concerned with a change in your original estimate. You diligently go through the analysis and come up with a new number that’s more in line with what was expected. Has that increased the accuracy at all? How knowable is the data you’re looking to get, especially when the risks are applied?
