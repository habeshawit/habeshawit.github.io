---
layout: post
title:      "My Sinatra Project"
date:       2020-11-16 03:42:13 +0000
permalink:  my_sinatra_project
---


For my second project, I build a sinatra app called EduTasks, an app students can use to keep track of upcoming assignments, tasks, and reminders related to courses they are enrolled in. I chose this idea because I'm a student myself and with all classes being virtual at the moment, having a place to track all tasks, classes and due dates collectively would be beneficial to me and I assume to others as well. 

The app is a CRUD, MVC app using Sinatra and a simple Content Management System (CMS) using the tools we have learned in Module 2. It uses four basic types of functionality: Create, Read, Update, and Delete.  It also uses a Model-View-Controller design pattern that divides the logic of the program into 3 section and each section of the code has its own distinct purpose. So, I set up the following:

1. A user can create an account and can create courses
2. A user can view his/her account information and can view courses they are enrolled in
2. A user can edit his/her own account as well as courses they are enrolled in
3. A user can delete his/her account as well as delete any courses

To set this up, I set up the following association:

```
class User < ActiveRecord::Base
    has_secure_password
    has_many :courses
end

class Course < ActiveRecord::Base
    belongs_to :user
end
```
Some gems and resources I found to be useful are:

1. [Corneal Gem ](https://github.com/thebrianemory/corneal) - I used this gem to set up the scaffolding for the project. 
2. [Sintra-Flash:](https://github.com/SFEley/sinatra-flash) - I used this gem to set alerts and notices to the user. (eg. incorrect password, account doesn't exist, password too short, etc)
3.  [Sass](https://github.com/sass/sass) - I found this to be useful for styling css.
4. [Boostrap](https://github.com/twbs/bootstrap) - I actually ended up not using this since I watching [this tutorial](https://www.youtube.com/watch?v=QoadrtxvvAY&list=PLNUiyK37z4zHyIuQjCJt-gPjBzbMb5k1Q&index=10&t=4984s) and ended up using sass instead, but it's a great resource for styling.  
5. [bcrypt](https://github.com/codahale/bcrypt-ruby) - this was useful for encrypting passwords

Overall, this was a fun project and one I hope to expand with additional features! 

My walkthrough video of the current status of the project can be found [here](https://drive.google.com/file/d/1ieuj8XJfbyZDpQJk3Gs1Dug1ZIVyq_eB/view?usp=sharing).







