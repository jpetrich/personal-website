---
title: "Code Reviews For All"
published: true
---

A friend of mine remarked recently that they don't really teach you how to do real software development
in school. Sure, you learn a language, hopefully a bunch of data structures and algorithms, and some
approximation of how computers work. All of this helps when it comes down to writing performant software,
but it's unlikely that you come out of school knowing how to write readable code, code someone else will
enjoy modifying and maintaining, code that will stand up to users misusing it in ways you didn't expect.
These skills come through collaboration, and, in my experience, came most quickly through the mentorship
of other software developers, and their reviews of my code.

The code review process can seem onerous, and I understand why some developers dread it. It can feel like
an exam, and, in a field where imposter syndrome runs rampant, it might seem unhealthy to subject
oneself to the criticism, however constructive, of one's peers. I like to think of code reviews as a sort
of "opposition research," and I think this helps me to view the process constructively. My colleagues
aren't trying to pick my code to pieces, or prove me to be incompetent. They're trying to strengthen my code
by finding its weaknesses, bringing the perspective of an outsider to reveal deficiencies I couldn't see
myself. What's more, not only does my code get better, I become a better software developer as I start to
anticipate the questions that reviewers will ask, and I get better at reviewing my own code through having
to perform code reviews myself.

In my first full-time software development job after college, I never had a code review. The pace of the
company was so fast, deadlines so urgent, and business growing so quickly that code reviews, unit testing,
and any sort of automation to ensure code quality were very low on the priority list. I learned a ton
in that job and it helped me grow my career, but the code I wrote wasn't great. I became biased towards
pushing code quickly, and relying on manual testing to verify the correct behavior. Inheriting a giant
codebase that only grew during my tenure, writing a single unit test didn't seem worthwhile when we had 0%
code coverage. I bought in fully to the idea that to move fast and deliver products quickly, testing just
had to be left by the wayside until some nonexistent future day would come when our team would have time
to stop feature development and start writing tests.

My perspective changed quickly when I took a new job for a smaller company, with a more complex codebase,
that had upwards of 90% test coverage. At this company, the engineering director fostered a healthy
engineering culture. He ensured the team performed regular code reviews of each other's code, enforced
a policy of keeping the test coverage up, and went to bat for the development team when there was an
apparent conflict between delivery timelines and code quality. I was initially intimidated to have my
code reviewed regularly, but it didn't take long for me to realize how quickly my code was improving
through the code review process. Even though we didn't have code reviews for every change, I began reading
more about general and language-specific best practices, reviewing my own code with a more critical eye,
and discussing designs more with my team instead of jumping into implementation. All of this led me to
become a much better developer, and to deliver much higher quality code.

Now that I'm at Google, I'm surrounded by people who share my view about code reviews. Every change is
reviewed by at least one other person, and my code quality has consistently improved as I've gone through
the review process here. I feel very fortunate that I had the mentorship of that engineering director before
coming to Google, and a little bit disappointed I didn't have that experience right out of college. I'd
like for more software engineers, and especially aspiring and junior engineers, to have the benefit of
code reviews. If you write code and don't have someone to review it, please reach out
and I'd be happy to review your code for you. I'm not the best software engineer out there, or the most
experienced, but I have reviewed many thousands of lines of code at this point, and I'd be happy to take
a look at yours as well. If you'd like to take me up on this offer, just
[add me to your pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/requesting-a-pull-request-review)
on a public GitHub repo.