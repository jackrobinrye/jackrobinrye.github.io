---
layout: post
title:      "A Good Coder's Mentality"
date:       2020-09-06 00:39:50 +0000
permalink:  a_good_coders_mentality
---


The content of this blog post is [here](https://medium.com/@jackrrye/a-good-coders-mentality-1b4a6d3b778b).

As I near graduation from Flatiron School, I can confidently claim that I have a better grasp on the mentality of a good coder.

Name your variables and files informatively. Learning this ended up changing how I interacted with code significantly. Each variable or file name should be informative and specific. In my most recent project, repeatedly I’d find myself naming a hash data and then being mystified by what type of information it contained when I reviewed it. I should have made sure everything was named playerData/player_data or characterData/character_data (snake vs camel case depending on whether in the front or back end). Methods should have clear names as well to clarify what they are meant to do too.

Next, as you hear time and time again, is to make your code as DRY (Don’t Repeat Yourself) as possible! Be modular! Make code that you can use in many places. Instead of copy and pasting the same code over and over again, make a method that does that work for you! When working on my React/Redux Random Character Generator, I tried to make dozens of if statements in the backend in my make_new_background method. I needed to create character alignments based on the randomly generated character ideals. For example:

[image]

This is the ideal table for an Outlander. Each option gives you a value for either “goodness” (good, neutral, evil) or “lawfulness” (lawful, neutral, chaotic). Initially, I began to create if statements for each value of each background and randomly assign it an alignment that way. I was maybe two dozen if/elsif statements in, when a friend pointed out I should just make a method for it.

At the time, I felt like banging my head against the wall. All I needed was a method that parsed a string for the last word in it and assigned values that way. In the end, my method looked like this:

[image]

The method has an informative title, assign_alignment. It finds the half of alignment (half_alignment) based on the final word in the ideal argument and assigns the other half randomly. Or, in the case of “any,” assigns both randomly.

The whole issue was something I should have realized sooner. Sometimes, as a coder, you get lost in what you’re doing without realizing you should clean up your process. I should not have gotten two dozen lines of copy-pasting ideals to create if-then statements in only to then realize I should make a helper method. It seems obviously in retrospect that I should have created a method first instead of going through to dozen lines of copy-pasting ideals to create if-then statements. That would have led to a smoother more efficient process

This leads me to my next lesson: don’t be afraid to break things! Once I was two dozens of if-then statements in I became afraid to go back and have the code function through a method instead. So I nearly kept plowing forward with the same if-then statements until a friend challenged me on allowing fear to dictate how I handled the code. My fear of breaking my code almost kept me from changing things for the better.

**It’s important to remember that breaking code is a part of making code.**

It’s unavoidable. Should things go horribly wrong, you can always fall back on your github repo. (Always remember to keep your github repo up to date!)

Finally, don’t get stuck in the “Well, It Works!” mentality! This is one I still struggle with. Good enough isn’t good enough. Aim higher! Work harder! Making something just to pass the minimum requirements or requires the least amount of effort shows people where your values lie. When you first finish working code for a project, consider your initial code as a first draft instead of a finished product. Make sure you go back and clean up redundant code. Ask yourself if your work flow maximizes efficiency. Moving forward, I plan to take a second look at some of my projects to see if there is anything I can do better.
