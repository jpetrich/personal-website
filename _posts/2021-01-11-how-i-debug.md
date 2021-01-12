---
title: "How to debug"
published: true
---

Debugging isn't just a skill for software developers and technical support - it's a mindset for problem solving
that is applicable in many spheres. In this article, I draw on my experience debugging production issues to give
you a framework for debugging. While I find it easiest to write about in the context of production software, the
methodology is also applicable to general problem solving, and I hope readers outside of software will appreciate
this way of thinking.

## Triage

Whether you're on call for a production service when a page comes in or you receive a call from a friend asking you
to help them "fix their internet," the first step in
debugging is to assess the issue and estimate its impact. This means answering two main questions:

1. Who is affected?
2. What is the impact on affected users?

For a production service, users could be internal developers, partners, or end users of your app or website. It's
important to identify if *all* users are affected, or a particular subset is. For example:

* Developers hitting the pre-production API from the Eastern US
* New users signing up
* All users in Australia

Your ability to refine the description of this subset will be limited by the monitoring you have set up for
your service, whether that's through your cloud provider or manually created systems. The priority of solving an
issue in production should be influenced by the number of users it affects, and who those users are.

The impact to affected users goes hand in hand with the number and kind of user affected when determining the
issue's severity and priority. When looking to assess impact, you can look at it from a service perspective or a
user perspective. From a service perspective, you want to ask about the type of traffic that is affected, and to
what degree. Some things to look at include error rates and latency across API methods, servers, clusters, or
data centers. Just like how you identified a subset of users that are impacted by the issue, here you describe
the subset of your service that is affected. For example:

* Inbound GET calls to the /profilePicture API are experiencing 100x latency compared to yesterday
* 5% of DELETE calls to /posts/id are returning a 500 error
* All calls to all APIs routed to your server in New Jersey are timing out

From a user perspective, assessing impact means identifying which user journeys aren't working as intended, and to
what degree. If your issue is user-reported, this means looking for details like "*every time* I try X, Y happens" or "Z didn't work *but I was still able to sign up*." Even if your investigation of impact started by investigating your service, you should figure out how users are affected to appropriately assign severity and prioritize the issue. Some examples of user impact (combined with the subsets identified above) include:

* Internal developers are getting a 500 error when calling the pre-production /healthCheck endpoint
* New users are unable to continue past picking their favorite widget in the signup flow
* All users in Australia are unable to see other users' profile pictures

When you combine the answers to the above questions - getting the "who" and the "what" - you can assign a severity
to the issue and prioritize it. More or higher-value users, at a high-rate or in an experience-breaking way, on
important user journeys means a higher severity. Fewer, lower-value users, at low rates, in inconvenient ways, on
less key user journeys means a lower severity.

In a general sense, when triaging you're attempting to boil the issue down to its simplest description while also
measuring the impact. If you're debugging your friend's internet, triaging the issue would mean finding out what
they mean when they say the internet "is not working." For example, what are they trying to do on the internet? Are
all apps and websites not working? What about other devices they have on the same internet connection? What about other people in their house? If you don't answer these questions first, trying to solve their problem is going to
be incredibly inefficient because you don't actually know what problem you're trying to solve. Even telling them to "turn it off and on again" is bad advice if what they meant by "is not working" is that a tree came down on their fiber line outside.

## Mitigate

Once you've assessed the issue's severity, move on to mitigation. The point of mitigation is not to solve the issue
forever, but to reduce or eliminate the impact of the issue. Some mitigation strategies include routing traffic
away from a single server that has high latency, rolling back a change that is correlated with an increase in
error rates, stopping a batch process that isn't critical to the end user experience when your servers are at
capacity, and disabling a broken feature so that users don't encounter the issue.

Beyond lessening the impact of an issue much more quickly than implementing the perfect long-term fix could,
mitigation allows you to think through what the "real" solution should be without the pressure of a user-facing
outage. In the morning after a now-mitigated outage, you might realize that the code change you rolled back as a
mitigation, instead of fixing as a solution, was submitted by mistake, or that the batch process you could have
purchased more capacity for but instead you paused, had been hacked and was mining altcoins instead of training
your ML models.

Outside the production world, mitigation is also a great debugging strategy. If your friend's internet is broken,
you might invite them over to use your internet while you debug it together, temporarily fixing their problem,
while also making it more likely they'll be able to fix their own internet next time. Or, you might suggest they
use their phone as a hotspot so you can help them tomorrow when you're less busy. Both of these are legitimate mitigation strategies!

## Learn

Now that users aren't affected, you can move on to designing a long-term solution, putting systems in place to
ensure the issue doesn't recur, and reflecting on how the issue could have been avoided in the first place. These
ideas are often included in a postmortem or retrospective that should be blameless and constructive. As a person
who worked on triaging and mitigating the issue, you should document how you did so, what went well, and what went
poorly - either by good/bad design, or by luck. For example:

* It took 3 hours to realize this issue was only happening in our QA environment because our logs are mixed
* It was clear 5 minutes after I received the alert that only Europe was affected because we have useful graphs that show traffic by region
* Rolling back the change alleviated the issue, but not because of a breaking change - it turns out the networking on our servers bugs out after 1024 hours and the restart required to roll back the change reset the clock!

It's important that a postmortem clearly outline how to prevent the same issue from happening again, and you
should make it a goal to never have to write the same one twice. Ideally, your postmortem not only results in
work that prevents the same exact problem happening again, but also makes similar problems easier to debug in the
future. As such, your postmortem should not be a secret - share it with everyone who works on and is on-call for
your service. At the least, it will provide a reference for the next person to encounter a similar issue.

## Final thoughts

What did you think of this article? Do you follow a similar thought process when doing any sort of debugging? How do you think these steps might be applicable outside the software world? Let me know by sending me an email at joe@petrich.xyz.