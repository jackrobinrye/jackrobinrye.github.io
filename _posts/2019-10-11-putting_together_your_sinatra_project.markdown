---
layout: post
title:      "Putting together your Sinatra Project:"
date:       2019-10-11 17:35:01 +0000
permalink:  putting_together_your_sinatra_project
---


First thing you will need to do in order to set up your Sinatra Project is to install the corneal gem. Just go into your command line and type `gem install corneal`. Next, run `corneal new NAME` (putting the name of your project where  NAME is) and finally run `bundle`. If you run `shotgun` you should now see that the skeletal structure of your app has been set up. 

How I approached my project once I had used the corneal gem was to create the migrations and seeds for my database first. So use `rake db:create_migration NAME=name_here` to create a migration for each table you are using in your project. I had 2 tables for my project. A books table and a users table. Don't forget to give users a *password_digest*. 

Once your migrations are set up, create your models. I had a model for books and for users. They looked like this: 

```
class User < ActiveRecord::Base

    has_many :books
    has_secure_password

    validates :name, :email, presence: true

end
```


```
class Book < ActiveRecord::Base
    
    belongs_to :user
    validates :title, :author, :genre, presence: true

end
```

I then created files for all my views and simply filled them in with a line of text saying what file they were. So a *show* view would say "show" in it. This functions to let me set up my first routes and test that they are working before I move on to add more functionality to the web page. Once all your files are there, make your most basic routes. Just the *get* routes. Index, show, edit, new, etc. Open Shotgun and test to see that they all are working. 

If your basic *get* routes are working, its time to start building forms. Your *new* and *edit* pages need to be filled out with all the necessary prompts for information. Set those up with names to secure their proper places in params. Don't forget your submit button for both pages and `<input type="hidden" id="hidden" name="_method" value="PATCH">` for your *edit* page. 

From here, you've got the bulk of your project done! Just keep working at it and you'll get the rest knocked out in no time!











