---
layout: post
title:      "Javascript Random D&D Character Generator"
date:       2020-06-09 21:28:08 -0400
permalink:  javascript_random_d_and_d_character_generator
---


Javascript is a bit step after so much time in the back end! Learning it involved a lot of stress and practicing deep breathing, but now here we are!

For my Javascript Project I made a Random D&D Character Generator. 

For those who know nothing about DND, each character is given 6 primary number stats: strength, dexterity, constitution, intelligence, wisdom, charisma. There are 2 main ways to assign these stats: point buy, or by using what's called the standard set. For this project, I used the standard set. The standard set is a pre-determined list of numbers you can pull from to assign values to each of these 6 stats. The set is [8, 10, 12, 13, 14, 15]. My character maker randomly assigns these values to the 6 character stats. Characters have aditional stats (name, race, class, gender, background, alignment, and age). All but the last are generated using the Faker gem. The last is generated with a plain ol' number generator. Age is generated to be a value between 10 and 200. 

My backend makes use of a make_new method in my Character class to make these randomly generated characters.

Then comes the front end, the part where Javascript comes in! I've got two class files: character.js and player.js. Both create objects and have self explanatory instructors. In my index.js file I have the bulk of my code. 

The structure of my file is this:

I start with creating the head of my page: the title and the create new player button. The create new button is, of course, a button, so it requires an eventListener. The event listener calls for a function (summonForm) which can be found at the bottom of the index.js file. It creates a small, 4 part form for creating a new character. It has inputs for name, gender, age, and a submit button. When you hit the submit button on a new player, the form disappears. You can summon a new form if needed.

The head of the page handled, nest up is all the various things to iterate through. I needed to iterate through 3 things: players, their characters, and each character's attrubutes. To do this, I needed to start at the top and go down. 

A promise is a conditional statement that will produce a value at some time in the future. It either returns resolved or rejected after a conclusion about the running code has been made. 

Javascript has built in asynchronous capabilities which allows the client to be updated without reloading the page. Fetch is the primary use of asynchronous methods in this project. The way it works is it's based off of promises. Fetch will return a promise every time it requests data from it's given URL. Then, using the .then() on the returned promise will ensure that code that depends on that data that is recieved will only run if the promise returns as resolved. There is also a .catch() that will run if the promise returns rejected instead of resolved. 

Ahead of all other code, I wrote a fetch call to my API (in my backend) that holds my player information. This fetch will wait until a response has been recieved. After it has been recieved, I then used the JSON data in the response to initialize the app and display all players and characters.

The other two fetch calls I used in my app were to create new players and create new characters in the back end. For new players, you fill out a form of information for your new player. When the form is submitted, that data is transfered through the backend via fetch and then comes back in the form of JSON data to be rendered on the site. 

The create new characters fetch is triggered by pressing the add new character button. The character is generated on the backend then transfered to the front end via fetch. 

My iteration process is as follows: iterate through the json data of all my players (renderPlayers function which is fed my fetched json data). The renderPlayers method calls takes each piece of player data from the json and creates a player object with it. Creating this player object creates all it's character objects, too, because of how a player is set up in player.js. We then iterate over this player object's characters. And for each player we iterate through it's attributes to display them in a table on the DOM.

It basically goes:
DOMContentLoaded -> fetch call to /players to get json to feed to -> renderPlayers -> renderPlayer -> renderCharacters -> renderCharacter

The purpose of this app is to allow any person who plays D&D to be able to keep track of random characters. With some later polishing, this app could fully create a character (class/racial bonuses and all) and save D&D players everywehre a lot of hastle!
