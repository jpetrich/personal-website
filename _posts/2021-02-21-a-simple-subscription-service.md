---
title: "A simple email signup and verification service using Google Cloud Functions"
published: true
---

As I've been working on this website and considering what to share on it, I remembered
the advice of a friend of mine, Zak, in an article he wrote called
[How to Stay In Touch With Your Network](https://zakslayback.com/stay-in-touch/). In it,
he recommends having a personal website and an email list to use when sharing a personal
newsletter. I've been reluctant to start sending out a newsletter as I can't share most
of my work at Google, but I have enjoyed writing here on my own website, and I decided to
build an email list to share the thoughts and projects I put here. As a software engineer,
I thought it would be fun to build my own email signup and verification service instead
of using one of the many free or paid options. This post explains how I did it. If you want
to jump straight to the code, you can
[check it out on my GitHub here](https://github.com/jpetrich/email-signup-and-verification).

## Choosing an architecture

I wanted to build an email signup service that I wouldn't have to think about after deploying
it. If, for some reason, my email list grows to the point where I need to worry about scaling
I'll likely migrate to another solution, so I decided to focus on something that would be
quick to spin up and scale out to dozens or hundreds of emails easily. Given these requirements,
I ruled out hosting my own server, which would require monitoring and consistent maintenance. I've
used Google App Engine, and that was my first thought, but then I remembered the simplicity of
AWS Lambda, which lets you run simple functions in a variety of languages without worrying about
even the serving framework. I decided to see if Google Cloud has a similar offering since I don't
have a personal AWS account, and I found [Cloud Functions](https://cloud.google.com/functions).
Similar to App Engine, Cloud Functions allows using a variety of languages. I chose Node.js because
it's quick to prototype and I've written App Engine apps in Node before.

After picking Cloud Functions for hosting, I needed to figure out how to collect emails, send
a verification email, and accept confirmation of receipt of that email. Collecting is easy - host
a form here on joepetrich.com that POSTs to my Cloud Function. I decided to use Cloud Firestore
for my database as it's easy to get going and has a high free quota. It would have been just as
reasonable to create a structured database, but I didn't want to worry about a schema while building
out the prototype. For sending a verification email, I found the
[nodemailer](https://www.npmjs.com/package/nodemailer) package which clearly documented how to send
emails through Gmail [using OAuth2](https://nodemailer.com/smtp/oauth2/). For receiving confirmation
of receipt of the verification email, I decided on a second Cloud Function that would take a URL
parameter identifying the user to mark the address as verified. A final feature I haven't implemented
yet is unsubscribe. I plan on building a third Cloud Function that will be accessible through a unique
link in each email that a user can click on to remove themselves from my email list.

## Email verification

Though this is a toy project, I am using it on my website, and wanted to take reasonable steps to prevent
abuse. For this reason, I wanted to make users verify their emails before they're added to my list, and
I wanted this verification to need to be done through an email they receive, so it will be impossible
for someone to subscribe email addresses they do not own. To do this, I decided to generate a random and
unique string for each email address that subscribes. This string is appended to the verification URL
as a query parameter, and the URL is sent in the verification email. The `emailVerification` Cloud
Function checks the verification code against the value in the database and only activates the subscription
if the code in the URL matches. I'm only using random numbers from the `Math.random` package, which does not
generate cryptographically sound random numbers, but the code is only used for email subscription, not
authentication, so I was happy to make the tradeoff of security for simplicity.

## User experience

Since I'm hosting the signup and verification endpoints using Cloud Functions and my website is hosted
on GitHub pages, hosting the endpoints on the joepetrich.com domain was going to be more difficult
than I thought it was worth. Ideally, the endpoints would be at joepetrich.com/emailSignup and
joepetrich.com/emailVerification, which would allow me to call them from frontend JavaScript on my
website, and either redirect to a confirmation page or simply change content on the home page in response
to the signup request. Since they're hosted on different domains, the POST request is done through
specifying the `action` on the HTML form element itself, so I redirect the user to a "thank you" page by
returning a redirect status code in the response from the Cloud Function. This works to make the user
experience what I want it to be, but limits my flexibility in the future. I'll probably switch to hosting
these endpoints on joepetrich.com pretty soon.

## Final thoughts

What did you think of this article? What could I have improved in building out this email subscription
service? Let me know by sending me an email at joe@petrich.xyz. If you'd like to receive future posts
via email, you can sign up using the service described here by entering your email address in the form
underneath my picture.