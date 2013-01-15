---
layout: post
title: "How I went about introducing High Schoolers to C"
date: 2013-01-14 00:24
comments: true
categories: 
---

Thanks to a good deal of luck, I attended the
[Illinois Mathematics and Science Academy](https://www3.imsa.edu/).
[IMSA](http://en.wikipedia.org/wiki/Illinois_Mathematics_and_Science_Academy)
is reported to be one of the best schools in America for mathematics
and science.
[Leon Lederman](http://en.wikipedia.org/wiki/Leon_M._Lederman) helped
found the school. Alumni have gone on to help found YouTube, Paypal,
Yelp, Palantir and OkCupid. My graduating class had about 180 people
in it, but we had about fifty national merit scholars and seven kids
who went to MIT. The chess team was great and the football team was
nonexistent. IMSA was, to say the least, a weird and intense place to
spend my teenage years.

One of the programs that IMSA puts is called
[intersession](https://www3.imsa.edu/learning/Intersession%202013).
Every year at the end of winter break, the kids have a week off to
focus on something neat. When I was there, I took a class on the
meaning of life, the mathematics of chess, and traveled down to New
Orleans a few years after Hurricane Katrina to help rebuild homes with
Habitat for Humanity. The intersession program made a large impact on
me for the better and so I've returned twice since graduating to
teach. Last year, I taught a week long course on Clojure to some
thirty students. This year I did an introduction to C programming via
some simple number theory for, an infinitely more manageable, eight
students. I've learned a bit about how to teach an intersession and
this post aims to share some of what I've learned so far by explaining
how I structured this year's intersession.

_N.B._ These kids were explicitly selected to attend IMSA because they
were some of the best students in Illinois, in terms of scholastic
aptitude and intelligence. The philosophy and resulting techniques I
outline here seemed to work well, but, truth be told, it's pretty
straightforward to teach kids who want to learn. I have no idea if any
of the below will work outside of IMSA or with students who aren't
that interested about learning to program.

## Everybody gets a book

With the vast riches I made during my last internship, I bought the
students used copies of "The C Programming Language". While K&R is
about twice my age, it still serves as an excellent introduction to C.
The format of the class was pretty straightforward: read the book, ask
questions and review, and do most of the exercises. I have no
delusions about being an amazing C programmer and so I let the
creators of the language do all of the heavy lifting. My role in the
class wasn't explaining all the material and enforcing a strict pace
on the kids, but rather answering tough questions about seg faults and
syntax errors while helping the kids learn as fast as they can.

## Circle the desks and prepare the troops

{% img right /images/desks.jpg 400%}

The plan was that the kids would be learning more from the books and
each other than from me. To that effect, the first day we circled the
desks together so that anybody was close enough to talk to everybody.
The class met for three hours in the morning and then three hours in
the afternoon. Every class I tried to have the kids switch it up and
sit next to somebody new. 

All of the students had windows installed on their machines, so we
spent the first morning setting up Cygwin and Notepad++ as a
development environment. Besides remembering to select the
correct packages during installation of Cygwin, there wasn't any major
problems at this stage. I taught them a few bash commands like `rm`,
`touch`, `ls`, `cat`, `make`, and `time`. After that, they were off
and running. 

I was really happy when a kid went through and started
typing in all the single letter commands and then all of the two
letter commands. He eventually found `ps` and we had a good discussion
about background processes and `kill`. (Way to go, Sean!) 

## Severe punishment for Facebook and Tumblr

One of the first things I told the kids was that the only way to fail
the class was if I caught them on Facebook or Tumblr twice.
Thankfully, I didn't have to fail anyone. I
only once caught a kid accessing Facebook and it seemed to be a reflex
of opening a browser window, not actually going on there to mess
around. 

The group was, sadly, all dudes and so Tumblr probably wouldn't have
been much of an issue. I included a second popular website though to
instill the fear into them of accessing any other popular websites. I
could have listed off a ton of websites that they should not be on,
but I left it somewhat vague so that the fear would carry over to
every website that wasn't related to programming. This scare tactic seemed to have
worked well enough.

## Explain why computers are hard 

Imagine everyone you've ever interacted with. The pretty woman in the
checkout line from last week, your friend from fifth grade who really
liked the book Hatchet, the representative you spoke to on the phone
about those nasty ATM fees a year ago. How long have each of these
thousands of people lived and worked? If you total all of that up,
you'd probably be on the order of a billion hours. Take that massive
sum, this gargantuan amount of time and effort, and you'll have a good
approximation of how much work has gone into making your computer
exist and function as well as it currently does. It would take a
lifetime to learn and understand everything that happens when you
Instagram a picture of a cat with your iPhone. Most of the kids in my
class were jumping head first into a body of knowledge that has gotten
bigger than any one person could ever hope to understand. So, of
course, some times what I asked of them was hard to do. I tried to
limit my questions in scope so that they wouldn't become overwhelmed
and give up. I warned them from the very beginning that programming is
hard and that they will need to know a thousand things before they
really feel like they understand what is going on.

## Frequent reviews of previous material

I like
[spaced repetition](http://en.wikipedia.org/wiki/Spaced_repetition) as
a way to learn material quickly and effectively. There are basic
things about a language that you need to be familiar with: types in
the language, hierarchy of operators, syntax for various control
structures, how char's are represented in C, etc. In addition to the basic
things, there are more complicated issues like what ASCII is, why
`c-'0'` converts a char of a digit into an appropriate int, and
various other big topics. I wanted to make sure students understand
all of the small topics that the big topics were built upon. To make
sure that students were picking up on what the book was covering, we
would have breaks every 45-90 minutes and either review what we
learned or write up exercises (see next section).

To review what we had learned, I would start by saying one fact I had
learned so far, including material from previous days, and then the
person to my left or right would say one fact. We would then continue
on around the circle, each person either saying one fact or asking a
question. If they said something vague like "I learned a lot about how
`if` work, I would push for more information about how `if` worked,
e.g. 
"How does `if-else` work then?" If a student brought up a good topic
or asked a question, I and Dr. Fogel (faculty at IMSA supervising the
interssion) would go some more detail about the topic. We would go
around the circle several times until the facts stopped coming as
quickly and then we would get back to work. 

## Pairs write up and explain exercises on whiteboards

{% img right /images/present.jpg 400 %}
{% img right /images/whiteboard.jpg 400 %}

From the very beginning, I knew I wanted students getting up and
explaining what they had been working on. It's pretty easy to get
trapped in your own head when you are learning to program. Getting
stuck on a problem and skipping over it is fine if you are the only
one who knows that you did that. However, if you have to get up and
present the problem to your peers, you will work much harder to figure
out everything you need to know to not be embarrassed. 

I made all of the students get up and go to the whiteboard at least
once per session to explain their work. We settled into a routine of
pairs of students working together to complete and write up the
exercises. The goal was to get them thinking and talking about
programming in as many contexts as possible. In addition, it got them
up and moving around, which is always good in a knowledge based class. 

## Discipline, sort of

The level of discipline I enforced was that if a conversation got off
topic for longer than ten minutes, I would yell "Study!" over their
conversation until they went back to work. It worked well enough.

## Programming Tangents

Once I figured out the
[Rails security bug](http://weblog.rubyonrails.org/2013/1/8/Rails-3-2-11-3-1-10-3-0-19-and-2-3-15-have-been-released/)
was serious business, we took the afternoon off and switched all of
our passwords. I explained why this mattered so much right now and how
one account on a site getting hacked could affect your account on
another website. We got to talking about security and why it can be so
hard to make sure your program only does what you intend it to do.

## All in all

The kids learned something. I can say that much. I'd like to hope that
I gave them a glimpse of why I enjoy programming so much and the
benefits it can bring into your life. When there is a billion hours of
background to cover before you can understand everything, there is
only so much that you can cover in thirty hours. I'm proud of all the
students who took the class and I'm really happy with how much they
learned. My two hopes are that this post helps you structure similar
classes and that the students continue on with their study of
programming and computer science.

{% img right /images/group.jpg %}

Way to go Tahj, Vimal, Jacob, Kieran, Eric, Andrew, Sean, and Dennis! 
