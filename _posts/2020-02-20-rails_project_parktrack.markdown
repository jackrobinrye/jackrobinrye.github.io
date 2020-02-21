---
layout: post
title:      "Rails Project: ParkTrack"
date:       2020-02-20 18:19:47 -0500
permalink:  rails_project_parktrack
---


For my Rails Project I built an app, ParkTrack that kept track of 3 object classes: parks, species, and, most importantly, sightings. It was through sightings that new parks or species could be made and that the relationship between parks and species could be tracked. I picked this subject because I have spent a lot of time visiting national parks growing up and they bring back good memories. 

I started my project by mapping out my relationships. Using an online program I mapped out how my relationships should look: 
![(https://66.media.tumblr.com/3e27748aa885b98c38f14d3eac78c4f3/8f322dca3f5136fb-6b/s1280x1920/4ff1e4be2dddd4c753803db74b9835fede4e6519.png)]

That done, I used the rails model generator to create my models and migrations. I find that easier to do than using the migration generator and manually creating models. I went into my model files to set up my object relationships and then the real work could begin. 

I focused then on routes. With the help of my professor, Jake, I stubbed out some ideas for routes: 
```
    # show/update/destroy
    # sighting/1

    # edit
    # sighting/1/edit

    # new -- this is where new parks or new species would be created
    # parks/1/sightings/new
    # sightings/new

    # index
    # sightings/
    # parks/1/sightings

    # species/

    # parks/

```
Those are straight from my notes created while working with Jake. From those notes I made my routes.
```
    resources :parks, only: [:index, :show] do
      resources :sightings, only: [:index, :new]
    end 
    resources :sightings
    resources :species, only: [:index, :show]
    get '/dashboard', to: 'users#show' 
    root 'application#hello'

```
Routes in place, I was ready to start building controllers and views. 
I started with Parks. I created the view pages for Parks and implemented a few simple validations. I needed some data to toy with to see my views so I took a quick trip to seeds.rb and created seed data.
Once Parks#show was up and running, I took a detour to get my login/logout functions going. I would have done so before I started on parks but I needed to wait until Jake did a demonstration to help me flesh out my functionality with Devise. I used devise to get both my custom login and my omniauth login working. 
That done, I moved back to my own models and views. I made the Species#show page and got ready to build index partials. Deciding the best way to set up my partials took some time. I felt like the best course of action would be to have one partial for both the index of parks and the index of species, but I wanted to sort species out by kingdom so, ultimately, that would not work. I created index partials for both species and parks separately. I'd need these partials for their index pages, for the home page, and for the Users#show page. 
I went on and built my home page. To do this all I needed were the index partials for species. I jumped to my application layout page real quick. I dabbled in some css I borrowed online to change font and create a header and footer formated how I wanted, then I used conditionals and added a login button, a logout button, and a dashboard button. 
With show pages and index pages done for Parks and Species, I needed to move on to the hard bit, the form for Sightings. I started in the sightings#new view but later moved and reformatted my code to make a form partial. 
The hardes part of my project was getting my forms to work. I have trouble understanding how to handle fields_for and nested attributes so that took some help from Jake. Eventually, though, I wound up with a form that accepted date, name and kingdom of a species, and had the option to either pick an existing park or create a new one. Then, I needed to figure out how to format the partial so it worked for both the /sightings/new and the parks/:park_id/sightings/new path. I needed a conditional and a working hidden field (the hidden field was tricky). 
Once my forms were working, I just needed to get my Sightings#show and Users#show (or /dashboard) views like I wanted them. The Sightings#show page was pretty straightforward. The Users#show required the index for species and parks, as well as a new partial I'd have to build for sightings index. I wanted my sightings listed in date order with dates as headings. This took some scope methods in my classes and helper methods to get everything organized like I wanted, but in the end I'm pretty content with how it works. 
That in place, I was pretty much done. I just needed to test different iterations of creating new sightings and look at all my pages to clean things up and format my views how I wanted. 
