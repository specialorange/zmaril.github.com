---
layout: post
title: "Ideas about the future of d3 and related technologies" 
date: 2012-07-10 23:31
comments: true
categories: 
---

[d3]: http://d3js.org/
[boilerplate]:https://github.com/zmaril/d3.js-boilerplate
[plugins]:https://github.com/zmaril/d3-bootstrap-plugins
[mail]:https://groups.google.com/forum/?fromgroups#!searchin/d3-js/zack$20maril
[odesk-blog]: https://www.odesk.com/blog/2012/07/visualizations-of-odesk-oconomy/
[dashboard]: http://research.odesk.com/visualizations/country-dashboard/

Lately, I've been working with [d3.js][d3] a good deal. I've created
several [open source][boilerplate] [d3.js projects][plugins],
participated in the [d3.js mailing list][mail], and
[successfully released][odesk-blog] a rather large
[d3.js project][dashboard]. I have at least as much perspective as a
self taught college kid can have at this point. Here are some ideas
that I've had about moving d3.js and related technologies
forward. They've been broken into the more general ideas first and the
backbone related ideas last. My hope is that this will cause one of
three things to happen: 

* I'll get motivated and make some of this happen.
* Somebody else will get motivated and make some of this happen.
* Somebody will point out that these things have been done and
  everyone can be lazy.

# General Ideas

## Encourage and use coffeescript

The function syntax, fat arrow, and object creation sugar are the
features that saved me the most time in aggregate. With d3.js you are
writing a lot of functions that are just object property retrievers,
so the terse syntax comes in handy (`(ob)-> ob.x`). Debugging is a
slight pain in that line numbers don't typically match up. For me, it
has been a net win. As I get better with coffeescript and d3.js,
debugging time will hopefully go down while I learn more useful
features.

## Use grunt

[Irene Ros](http://ireneros.com/) pointed out
[grunt](https://github.com/cowboy/grunt) to me and it was love at
first sight. I've been using it with the
[d3-bootstrap-plugin](https://github.com/zmaril/d3-bootstrap-plugins)
project and it has
[helped immensely](https://github.com/zmaril/d3-bootstrap-plugins)
with development. It's really amazing how freeing `grunt` and `grunt
build` can be. I am looking to learn more about the system. If I could
automatically run `python -m SimpleHTTPServer` when I do `grunt
watch`, I would be way happy. I'll try and do a post on using grunt
and d3, but it isn't too hard to [figure out in an afternoon](http://net.tutsplus.com/tutorials/javascript-ajax/meeting-grunt-the-build-tool-for-javascript/).

## Testing visualizations with saved images

A problem I've had is that I really want to start writing tests for my
visualizations. They have started to get sufficiently complex in some
cases and things have broken down for several hours/days before I was
able to notice them again. Stressful.There aren't too many solutions
to this that I know of. You can test the DOM pretty easily with the
various testing libraries out there. But that's almost a direct test
of d3.js itself in most cases. Not incredibly useful given that d3.js
already has
[pretty good test coverage](https://github.com/mbostock/d3/tree/master/test).

A possible solution for this is to create a collection of saved images
that represent what the visualization should look like. You could pair
[the selenium webdriver](http://seleniumhq.org/) with a framework like
[qunit](http://docs.jquery.com/QUnit) or
[jasmine](http://pivotal.github.com/jasmine/) to create a image driven
test suite. You would have a program that walks you through the tests
one by one, displays the image, and asks "Is this what you expected?"
It then saves all of the reference images. Each time you run the
tests, it would go back through and recapture all of the pictures. A
test would fail if the picture wasn't within a set threshold for
deviation of pixels. You could get really fancy with this and take
snapshots of images as things get interacted with randomly, as well as
have UI exploration based on the state of the javascript
environment (Clojure/script would probably be a pretty good tool for
this sort of thing). The main point is that I want to write tests that
use saved images as the method for evaluating whether or not the test
passes. No speculation on difficulty, prior art, implementation, and
performance from me at this point. I currently don't have plans to do
anything related to this.

# Combining d3.js and backbone

Let's get some context for the upcoming ideas. From what I can tell,
the two major frameworks for d3.js right now are
[nvd3](http://nvd3.com/) and
[dance.js](https://github.com/michael/dance). 

nvd3 is a general charting library that has gotten a fair bit of press
lately. I watch it on github and I've seen a marked increase in terms
of rate of commits and issues added to the project day after
day. People are excited about the idea of a general framework with
d3. nvd3 is a good idea with a smart/motivated developer behind it and
could end up displacing highcharts.

dance.js is a project that I have admired from afar at this point. I
view it as one of those projects that is fun and will teach the
developer a ton. It might not ever end up use in production, but it
doesn't matter. The developer will write better code all around
because of it. Really, go take a look a look at it. It's fun to read
through and think about the abstractions that are being created. It's
got some obscure libraries as dependencies and purposefully
reimplements half of backbone.

So, as far as I know, that is the current state of the major open source d3
frameworks. There is
[Rickshaw](https://github.com/shutterstock/rickshaw) for time series,
but it isn't
[actively being developed further beyond maintenance](https://github.com/shutterstock/rickshaw/commits/master)
as far as I can tell. There has been some excellent talk about
[combining ember.js and d3](http://corner.squareup.com/2012/04/building-analytics.html),
but not much open source has come out of it. This is the most active
[ember+d3](http://cmeiklejohn.github.com/ember-visualizations/) work
I've been able to find. As far as backbone and d3 goes, there is [a
project](http://drsm79.github.com/Backbone-d3/) silently gathering
dust on github and [graphene](https://github.com/jondot/graphene),
which is [semiactive](https://github.com/jondot/graphene). 

__tl;dr Try to use nvd3 if you want free/pretty d3 charts now.__

(Note: As of December 2012, much of this information is no longer
correct. Rickshaw is getting love, ember and d3 are being combined
together well, and, well, open source is moving forward.)

## Eidetic backbone

Moving towards new ideas, a month or so back, I noticed that backbone
and ember allowed you to manage the URL in neat ways with
[javascript based routers](http://backbonetutorials.com/what-is-a-router/). At
the time, backbone had better documentation about getting started, so
I choose backbone and got started using the routes to encode the state
of the interface of the oDesk country dashboard. This meant I could
link directly to the project bubbles of
[Russia](http://research.odesk.com/visualizations/country-dashboard/#/bubble/Russia)
and
[Canada](http://research.odesk.com/visualizations/country-dashboard/#/bubble/Canada)
with very little effort.  This was way cool and set me down the path
of thinking through how to combine backbone and d3.js to produce
excellent visualizations with very little developer effort.

The basic abstraction was encoding the state of an interface within
the URL. This allowed people to directly link to pieces of a
visualization as well as making the backbone much more useful (trying
messing around with the oDesk visualization and then hitting the back
button). I
[implemented this in a messy way](https://github.com/johnjosephhorton/gg2d3/blob/master/country-dashboard/js/index.coffee),
with a ton of calls to router.navigate littered throughout the
code. It got the job done.

Generalizing away from this, we can start thinking in terms of the
state of the interface. For the oDesk visualization, the state of the
interface depended on the section being displayed. For the
[compare section](http://research.odesk.com/visualizations/country-dashboard/#/compare),
we encoded the selected countries within the URL as well as whether
the top graph was being displayed in absolute or log scale. For the
[watch section](http://research.odesk.com/visualizations/country-dashboard/#/watch/false/42),
we encoded the hour being displayed as well as whether we are using a
relative or absolute scale. The
[bubble section](http://research.odesk.com/visualizations/country-dashboard/#/bubble)
recorded only the country within the URL. If you crawl through the
github repo hard enough, you can probably find all the instances
across the multiple files where I reference variables like
selectedCountries and what not. 

Here's what I wish I could have written (in coffeescript):

``` coffeescript
CompareState = Backbone.Model
    countries: ["India","Denial","`Murica"]
    log: true

WatchState = Backbone.Model
    time: 42
    log: true

BubbleState = Backbone.Model
    country: "Canananada"

Eidetic.Router.extend
    routes:
        compare:
            model: CompareState
        
            toUrl: ()->
                countries = encodeURI(@countries.join["/"])
                "/#{@log}/#{countries}"
                
            fromURL: (url)->
               sections = url.split('/')
               log = sections[0] is "true"
               countries = (decodeURI(c) for c in sections[1..])
               @model.set
                   log: log
                   countries: countries
                   
            callback: "compare"

        watch:
            model: WatchState
        
            toUrl: ()-> "/#{@attributes.log}/#{@attributes.time}"
                
            fromURL: (url)->
               sections = url.split('/')
               log = sections[0] is "true"
               time = +sections[1]
               @model.set
                   log: log
                   time: time
                   
           callback: "watch"

        bubble:
            model: BubbleState
        
            toUrl: (model)-> "/#{model.country}"
                
            fromURL: (url)->
               @model.set
                   country: url.replace('/',"")
                   
            callback: "watch"

    compare: ()-> #display compare html. No updating of url's here.
        compareView.update()
    watch: ()-> #display watch html. No updating of url's here either.
        watchView.update()
    bubble: ()-> #You know what is up by now.
        bubbleView.update()
```

What would ideally happen is that the
[Eidetic](http://en.wikipedia.org/wiki/Eidetic_memory) router would
hook up the model such that whenever the model changed the router
would change as well. In addition, the Eidetic router would take the
inbound url and set up the State model correctly. The design behind
the API is still pretty rough honestly. I've spent most of my time so
far just playing around with how to structure this idea of storing the
state of the interface within the URL. I have a
[repo set up for development](https://github.com/zmaril/Eidetic), but
only within the past few days have I gotten an idea about where to
take the design of the API. I suspect within the next month I will
have something usable up there.

Why does this matter for d3.js though? This would be developed purely
as an extension of backbone. As I got better with d3.js, my sights
start to soar. I wanted to create the next big dashboard. And
"Wouldn't it be cool if state crossed over between those two charts?
Woah! That's awesome! Let's do it again! Three charts! Four charts and
legend! Wait. Why is it broken? Where is my state?"  It's part of
solution to the puzzle of managing a complex interface that has
multiple interactive and connected charts.

I want to put all of my important state in one place and I want the
URL to denote and remember the state of the interface. I don't want to
have to design a complex framework each time I set out to design a
complex dashboard. backbone would handle the state abstractions and d3
handles the svg. The Eidetic router is not a hard hack to do, but I
really want to nail the API design from the get go. Looking at it now,
I will probably move the callbacks straight into the route
definition. Maybe.

## d3.js charts as backbone views

Now that we have gotten into the spirit of thinking with backbone,
let's start thinking about collections and reusable charts. Here's an
example of what I mean:

``` coffeescript
Book = Backbone.Model

Books = Backbone.Collection.extend
    model: Book

Books.add({pages: Math.round(Math.random()*250)} for i in [0..100])

Histogram = Backbone.view.extend
    initialize: ()->
        @svg = {}
        @svg.svg = d3.select(@el).apppend("svg")
            .attr("height",@options.height)
            .attr("width",@options.width)
            .classed("histogram")
            
        @svg.bars = @svg.svg.append("g").attr("id","bars")
        @svg.axis = @svg.svg.append("g").attr("id","axis")

        @d3 = {}
        @d3.hist =  d3.layout.histogram()
            .value(@options.value)

    render: ()->
        bins = @d3.hist(@collection)
        #Make all of this actually work
        @d3.x = d3.scale().range
        @svg.bars.selectAll("rect").data(bins).enter()
            .append("rect")
            .scale
        #If I wasn't lazy, code for the axis would be here

    remove: ()-> 
        @svg.svg.remove()

BooksHistogram = Histogram
    collection: Books
    element: document.getElementById("#booksHistogram")
    value: (d)-> d.get("pages")
    height: 200
    width: 200
```    

And bam! You have a histogram of the books! That updates dynamically
as your backbone data does! And the implementation is reusable for other
models. This is what I see coming from combining backbone and d3
together. 

That is most of what I was thinking about while working on the oDesk project. 