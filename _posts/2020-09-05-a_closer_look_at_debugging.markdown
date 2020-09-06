---
layout: post
title:      "A Closer Look At Debugging"
date:       2020-09-06 00:44:04 +0000
permalink:  a_closer_look_at_debugging
---


The content of this blog post is [here](https://medium.com/@jackrrye/everyone-has-their-own-method-of-debugging-though-youll-find-there-s-great-overlap-cf86b1952a0f).

Everyone has their own method of debugging, though you’ll find there’s great overlap. Approaching any big project, debugging is most of what you do. Encountering problems in your code or encountering broken code is just part of being a developer.

When I debug I start by searching for the relevant file. You always start by looking at the lines of code the error is coming from. Syntax errors are always the easiest to fix.

The line throwing the error isn’t always the source, though. Sometimes a person has to dig deeper. One example would be a `Uncaught TypeError: Cannot read property ‘map’ of undefined` error. The reason for this error is usually improperly passed data. Finding where the data gets lost goes something like this:

I would start in the file throwing the error. Then, I would use debugger and console.log() to find what value the data has in that file and what it looks like when I pass it around.

If the data is undefined or empty everywhere in the file throwing the error, I go backwards to where the data is being passed from. In my Random Character Generator (RCG) project, this often led me to the ApiCalls.js file where I had all my fetch calls. I keep following the trail of where I passed my data until I find the file where the data is as I want it to be. Then, I know the error is somewhere between that file where it’s the correct type and has all the attributes I need, and the previous file where it isn’t.

The process to debugging data that is incorrectly defined is similar. I work my way backward until I find where the data is the correct type and has all the attributes I need.

Once I find where the passing of data messes up, I analyze.

Maybe I forgot to initialize the variable properly in my reducer. Maybe the way that I’m trying to retrieve the data from the API is inconsistent with how the backend is structured. Maybe I forgot to add the connect function or forgot to pass props to a child component. (All things that I did, in fact, do at one point during my RCG project.)
I was throwing an `Unhandled Rejection (TypeError): Cannot read property 'background_title' of undefined` error at one point in my RCG project. The line it pointed me to read:

`<ListGroup.Item><h5>Background: {props.backgroundInfo.background_title}</h5></ListGroup.Item>`

When I used console.log() to see what my props looked like, I found that {backgroundInfo: undefined. I looked to see where the data was being passed from. My background component was getting props from my CharacterPage.js I was passing d.background as my props in my CharacterPage file. I console logged that and found that d.background was undefined. I console logged my variable d next. That gave me:

[image]

Alas! No background! When I hit this I was thoroughly confounded. Why did I have a full set of data but was missing one piece? That made less sense than having not acquired any data at all. After maybe an hour of bang my head against my wall, I remembered one of the golden rules of code:

**Never sit down and code for too long in one sitting.**

Remember to take a break! Grab a snack, drink some water, etc. So, I took a break. I texted some friends and made lunch. When I got back, it took me five minutes to realize what was wrong.

Was my problem fixed? Unfortunately, not yet! My API looked good, but my console.log(props.backgroundInfo) in my Background.js file still turned up undefined. I backtracked to my CharcterPage.js file where I passed d.background as props to Background.js. I found that when I console.log-ed d.background it came up as an empty object. Why would this be?

The next question is where does d (or this.props.character) get defined?

It comes from the Redux state and is defined in my reducer. I first looked at my GET_CHARACTER case. There, I saw that my character object was populated and had all the attributes I needed. It was another head-scratcher, and, I have to admit, I once again made the mistake of being in the coding zone too long. I spent a good while agonizing over what was causing my error. Another break and another snack later I realized that it was coming from where I was initializing my object. My line initializing my reducer looked like this:

`export default function reducer(state= { players: [], character: {}, player: {characters:[]} }, action) {`

I needed to initialize background! I was trying to access the background attribute of character when a background attribute wasn’t there yet (because the fetch call hadn’t been run yet). I changed my code to:
`export default function reducer(state= { players: [], character: { background: {} }, player: {characters:[]} }, action) {`

and my code was finally working!

Often there is more than one thing causing an error. Maybe you fix one error but your code still isn’t working. Don’t be discouraged! This is a normal part of the coding process. Just take things one error at a time, and keep going (whilst taking breaks when appropriate)!
