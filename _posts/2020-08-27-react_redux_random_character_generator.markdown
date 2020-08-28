---
layout: post
title:      "React/Redux Random Character Generator"
date:       2020-08-28 00:09:47 +0000
permalink:  react_redux_random_character_generator
---


The beginning of every coding project is always the file structure and setting up the GitHub repo. As such, my first steps to this project were 1) creating the backend with the $rails new APP NAME --api command 2) creating the front end with $npx create-react-app app-name 3) backing the entire project folder containing the front and back ends up to github. 

I then began in the backend. I used $rails generate to create models for my players and characters. I created validations as necessary and made sure that a character belongs_to a player and a player has_many characters (Note: I added the backgrounds model later on in my project). Next up was building my make_new method in my character model which was easy at first, but later, when I added backgrounds, became more difficult. With the make_new method in place I could create the seed data I needed. I couldn’t move to the front end until I had seed data and routes set up in my front end. I needed an API to work with in order to mess around in the front end. 

When I moved from the back end to the front end, I started off in the most basic of places: my home page. The home page is a container, and like most of my front end, I used Bootstrap-React to create it. I knew I wanted a header for all pages, a home page, a player page, a character page, and a new player page. Originally, when I built the home page I had a fetch call to the player’s page directly in it. Later, I made an ApiCalls file that handled all my API calls and was imported into the necessary file. Redux state is present in my Home component, hence the mapStateToProps, mapDispatchToProps, and connect functions. My mapDispatchToProps is giving me proper access to the fetchPlayers and createCharacter functions. In my code I call those functions which update my local state. My mapStateToProps function then uploads the local state (containing an array of my players as obtained by my fetchPlayers function) to the Redux state. The connect function makes my redux state available in this file through props. 

Next, I needed to actually set up my routes in the front end. In my App file (another container) I have React-Router. It has the routes for my home page, my player pages, my character pages (there is a fetch function in this file for that), and my new player page. The only other thing that is really in my App.js is the div with the class “bg” which, paired with some css, allowed me to have a background image for my website (though it is not used on the home page). 

The other containers in my project are my character pages, player pages, and new player page. 

The new player page uses Bootstrap to create a working form. It uses fetchPlayers (as all the containers do) and createPlayer from my ApiCalls file. Each field has its own ------Change method to save changes in its value to state. There is a handleSubmit function for the form that uses the createPlayer function and the field values to send data to the backend and create a new player in my database.

All the containers (except App.js) use the Redux state. The player page uses three components: Header, CharacterBrief, and the AddCharacterButton. The character page uses four components: Background, Stats, CharacterBrief, and Header.

My AddCharacterButton component contains a fully functional button that uses local state. Depending on whether or not the showForm value in state was true or false, it gives you an input box to type in the campaign name for your random character. The Background component is passed down props from its parent component. It creates a simple list group with all the attributes from the background model. The CharacterBrief component portrays a table with the main character attributes to give you a gist of what that character is like. The Header component contains all the necessary code (with the help of bootstrap) to create a header with links to all the relevant pages. The Player component creates a div with a link to the player’s PlayerPage and a CharacterBrief for each character that the player has. The Stats component contains a table with the stats for a character. 

