---
title: new title
tags: d3, data binding, hack reactor, game, javascript
published: true
---

###What's this D3 thing, anyway?
D3 stands for Data Driven Documents. It's a javascript library usually used for data visualization.

###Have you written anything with D3?
Yup! During a recent 2-day solo project at Hack Reactor, I made a silly little game. You can play it here:
>http://m-arnold.github.io/

I wrote it in two days. Be gentle.

###Pretty cool! How do I do that?
Explaining the whole thing would require a lot more space then I've got here, but let's start with **data binding**.

###What's that?
**Data binding** is the process of creating a link between a given DOM node and some set of data. Here's a sample:
```
var data = [1,2,3];
d3.select('.numbers')
    .data(data)
    .enter()
    .append("div")
    .text(function(d) { return d; });
```
####Uh...what?
Fair enough. Let's talk about what's happening above.
 
* "d3.select" is  just like a jQuery selector. So `d3.select('.numbers')` is selecting all DOM elements with class 'numbers'. "But wait!" You ask, "how does it select DOM elements I haven't made yet?" Hold on to that thought, young grasshopper. 

* Using the magic of method chaining, we associate `var data` with that selection using the `data()` method.

* `enter()` *sub-selects* any elements that don't already have data associated with them. If there are less elements than data, then it creates new elements to hold that data! Pretty great, huh? 

* `append()` attaches new divs to the selection based on the `enter()` sub-selection.

* `text()` fills in the above divs with, well, text. `function(d) { return d; }` tells d3 to attach one piece of data to each sub-selected element.

Now, you've got a set of DOM elements that you've programmatically filled with data, appended to your page. Yay!
