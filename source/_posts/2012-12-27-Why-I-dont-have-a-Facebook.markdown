---
layout: post
title: Why I don't have a Facebook account
category: posts
---

[target]: http://www.nytimes.com/2012/02/19/magazine/shopping-habits.html?pagewanted=1&_r=2&hp&
[vpf]: http://www.economist.com/node/21556263
[nlp]: http://en.wikipedia.org/wiki/Natural_language_processing
[cv]: http://en.wikipedia.org/wiki/Computer_vision
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[ipo]: http://www.forbes.com/sites/danbigman/2012/05/23/facebook-ownership-structure-should-scare-investors-more-than-botched-ipo/

In the past past three years, I've lived in Chicago (IL), College
Station (TX), Urbana (IL), Cincinnati (OH), and Mountain View (CA).
I've spent at least three months in each place and gotten to know and
love a good number of people from all over. I have friends who travel
internationally, and friends from school who are now scattered all
over the world. All of this movement and change brings up the topic of
keeping in touch fairly often. The main method for keeping in touch
now seems to be adding each other on Facebook and letting
conversations happen "naturally". This poses an awkward problem for me
in that that **I don't have a Facebook account** and **I don't want to
create one**.

I got rid of my old Facebook account at the end of high school because
it had become a boring waste of time and I didn't have any good reason
to keep it around much longer. This would probably still be the case
now, but my reasons for not having an account have evolved and gotten
much stronger as I've learned more about
[natural language processing][nlp], [computer vision][cv],
[machine learning][ml], and how some [companies][target] make
[money][vpf].

I'll premise this all with the one really strong assumption I've made:
**I don't think Facebook can make enough money from advertising to
satisfy shareholders or even hit internal monetization targets**. While
there is [very little that shareholders can do to influence](ipo)
Facebook's decisions, everything could change very quickly in the near
future:

* Facebook hits a rough patch and has to sell more preferred stock to
finance operations.
* Zuckerburg needs vast quantities of cash to buy Brazil as his summer get away.
* Facebook uses "pressure" from shareholders as a valid reason to do
  whatever it wants.
* Zuckerburg dies/retires suddenly and somebody with a different vision for
  Facebook becomes CEO. 

In my mind, there is a nonzero chance of Facebook needing to find a
way to make way more money than advertising will allow them to in the
next few years. And so, with that assumption, let's put our
entrepreneur hats on and think: **What can Facebook do to make money
besides selling ads?** This exercise by itself is a fun challenge in trying to
figure out what resources Facebook has at its disposal. Maybe try
taking a few minutes and see what you can think up.
 
The most realistic option that I see happening is that Facebook takes
all that talent they've gathered from Stanford and other nerd farms to
mine all the data that they've accumulated. **For the typical user,
they probably have a few years worth of status updates, wall posts,
messages, Facebook relationships between members, events attended,
likes, location data based off of geo-tagged status updates and
reverse IP addresses, history of web sites visited
([collected from like counters on pages](http://www.businessinsider.com/this-is-how-facebook-is-tracking-your-internet-activity-2012-9?op=1))
and countless tagged photos**. There is probably more that they know,
but all this should be enough to get us started down the path of
understanding why Facebook knows more about you than you ever will.

First though, I freely admit that I'm not a machine learning or social
network expert. I know a little bit from what I've read online and a
few books I've picked up, but I would have to spend a fair amount of
time brushing up before I felt comfortable implementing even naive
methods. However, unless noted otherwise, I think everything I list
here is well within the capability of the
[talented team at Facebook](http://www.technologyreview.com/featuredstory/428150/what-facebook-knows/).

So, without further ado: You there! Yes, you! Step right up and play
**"What could Facebook possibly know about a user?"**

{% tweet https://twitter.com/ZackMaril/status/284115670814314496 %}

If you are a woman, then you probably know the pains of the menstrual
cycle. I don't have firsthand experience personally but I've heard
through the grapevine that it sucks. **Have you ever seen a woman post a
status update like "Omg, I hate my body, does anybody have any
chocolate"?** It is reasonable to assume that the user was on their
period when that update was made. 

Here's how Facebook could use status updates like this one and other
ones to calculate when a woman was on her menstrual cycle.
Specifically, what they would be looking for would be the length and
offset of the cycle (when does the cycle start and how long does it
last?). They could construct a
[bag of words](http://en.wikipedia.org/wiki/Bag-of-words_model) model
based on the set of words like
"period","blood","midol","tampon","hurts", etc. They could then create
a function that takes in a status update and uses the presence of the
words in the bag to give the most probably stage of her menstrual
cycle that a woman was on when she made that status update. Then, they
could run that function across every status update that a woman has
made and get back a time series giving the stages of a woman's cycle.
From there, a
[measure of autocorrelation](http://en.wikipedia.org/wiki/Autocorrelation)
could be applied to find out the length of the cycle. The offset could
then be found shortly afterwards through some straightforward methods.

This is a simple model of course and only works if a woman posts
somewhat directly about her period. But bag of words can be extremely
versatile; the model could be refined to figure out what words like
"chocolate", "stay home", "uggghhhhhhhh", "boyssssss" and others would mean.
Instead of each status update considered individually, all the status
updates for one day could be lumped together which, I believe, would
help reduce noise in the data and give more precise results in terms
of confidence with less precision in time. There are many ways to
refine this model without much hassle. 

{% tweet https://twitter.com/ZackMaril/status/284116240304312320 %}

If a user is sending messages about "blacking out" or asking "what
happened last night" then they might have an alcohol problem. Using
computer vision, you could count the number of
[red cups that appear in photos](http://www.veerina.com/2012/Classyfying-Red-Cups.html)
that a user is tagged in. The more cups there are in a user's photos,
the more likely a user might have a problem. **Take the number of
occurances of certain words and the number of red cups, run it through
one of
[the dozens of classification algorithms](http://en.wikipedia.org/wiki/Category:Classification_algorithms)
[with a decent training set](http://en.wikipedia.org/wiki/Training_set), and you have a system that can
predict the whether a user has alcoholism based on their profile**.

{% tweet https://twitter.com/ZackMaril/status/284117064799617024 %}

Have you been looking at somebody's profile a ton lately? Have they
been looking at yours? Do you attend the same events as them? Have you
been sending a bunch of messages back and forth lately with someone?
**Do any of your messages contain something along the lines of "Last
night was amazing ;)"?** All of that information can be used to
predict whether two people have had sex. Using that same method on
every person a user has interacted with and you have the expected
value of the number of sexual partners and information with which you
can construct sexual orientation.

{% tweet https://twitter.com/ZackMaril/status/284117443293609984 %}
Checking the phone less often from the gym? Checking into Facebook
late at night, disrupting your sleep schedule? Status updates about
how stressed out you are? In a week or two, you will probably be sick
and Facebook will have known about it before you even had the first
symptom.

{% tweet https://twitter.com/ZackMaril/status/284119586666864640 %}

Facebook has all of the information needed to construct a highly
accurate [life table](http://en.wikipedia.org/wiki/Life_table). They
know everything about the lives of roughly a billion people across the
globe. They have systems in place for finding out when a person is
dead and can use that information to start constructing massive life
tables based on user's age, location, gender, sexual orientation, what
they liked on facebook, and who they were friends with. While it might
be a stretch to say that Facebook can predict cause of death, time of
death is well within the realm of possibility.

So. **Facebook probably knows more about your life than you ever will
know.**  Why does that matter? 

{% tweet https://twitter.com/ZackMaril/status/284120780323827712 %}

Facebook needs to make money. Under the stated assumption, advertising
isn't going to cut it. ** My main fear is that Facebook would soon be selling
information about me that even I don't know.** 

Who would want to buy detailed information about you, you ask? 

* College admissions: How often does this person study, are
  their parents wealthy?
* Insurance companies: What are the health risks of insuring this
  person, does this person's family have a history of depression,
  how often do users who like 'Texting at Red Lights' get into car
  accidents, what is the chance that this user will get an STD in
  the future?
* Employers: Does this person complain about work often, Does this
  person work late at night, does this person have friends who we
  can recruit later, has this person ever slept with someone from
  work?
* Identity thieves: Soooooo, how much do I need to pay to know **everything**
  about a person?
* Banks: What is the credit score for people who like 'Student
  loans suck', what is the credit score for user based on who his
  friends are?
* The IRS: What is the difference between how much this person
   reported on their taxes and users like this person?
* Oppressive governments: Where is this user, who are this user's
  friends and families?
   
So, I think it will soon be in Facebook's best interest to start
selling users' information to parties who will use this information in
ways that are not in users' best interest. Your life will be moving
more towards a completely asymmetrical model of knowledge: parties who
you don't know exist will know more about your life than you do. As
soon as companies figure out they can use this information to their
advantage, they will throw as many resources at it as they can. I can
imagine far more negative consequences of greater magnitude of this
knowledge difference than I can of positive consequences. Bluntly, **I
think you are screwed if you have a Facebook account**. Which,
incidentally, is why I don't have an account.

I really hope I am wrong though. It would be nice to say this is just
some eggnog induced paranoia and that the folks at Facebook would
never do something like this. I have friends and family who all use
Facebook and I fear that they will get very hurt because of it and not
understand why. I wish I could have a Facebook account without
worrying that it will come back to haunt me. 

------------

** Bonus ** 
{% tweet https://twitter.com/ZackMaril/status/284121414401933312 %} 

If this were implemented at Facebook, whoever did it will probably
take that secret to her gold-lined grave. Facebook would probably have her
killed if she tried to talk (half joking here). 

------------

** Double Bounus **

You might be able to delete your profile ([it takes two weeks](http://www.wikihow.com/Permanently-Delete-a-Facebook-Account)), but there is no
way you can get Facebook to throw out your data. If you want to mess
up their systems, you really only have one option that I can think of:
start throwing in random noise into your profile for a few weeks or
months before you wipe your profile and then delete it. Tag yourself
in pictures as people who you obviously are not. Change your birthday
often. Like things that you don't like. Message people you wouldn't
normally message. Defriend a ton of people and add in some random
people of various types (local and global). Change your name. Do
whatever you can think of that you wouldn't normally do.

And then at the very end of it all, remove all of your information
from Facebook. Some crazy unicode name, no friends, no pictures, no
likes, all of your settings changed to strictest privacy possible.
They will have a record of everything you did, but they will have to
be very, very careful about how they use your data from now on. If an
intern messes up and only uses dead profiles as they last appeared,
then you will be a ghost. If an engineer messes up and doesn't account
for the random noise at the end, then your profile will be worthless
to them. Beyond that, that is really all you can do. They already know
everything about you; all you can do is help them make mistakes. 
