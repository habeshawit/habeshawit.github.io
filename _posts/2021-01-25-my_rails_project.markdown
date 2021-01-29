---
layout: post
title:      "My Rails Project"
date:       2021-01-25 03:10:37 -0500
permalink:  my_rails_project
---


For my Rails project, I decided to work on a recipe managment app with a bit of a social aspect to it. I created an app where users can create and save some of their favorite recipes and share them with others. Users can also browse through other users' profiles and recipes. They can add other chefs to their friends and gain inspiration from others. This was my favorite project so far because I had a great time exploring different aspects of the project such as adding recipes to favorites, making friend, using various useful gems....etc.


These are the associations I set up for my two main models:


User:
```
  has_many :recipes, dependent: :destroy
  has_many :comments, :dependent => :destroy
  has_many :commented_recipes, through: :comments, source: :recipe
  has_many :friendships, :dependent => :destroy
  has_many :friends, through: :friendships
  has_many :user_recipes, :dependent => :destroy
  has_many :added_recipes, through: :user_recipes, source: :recipe 
  has_one_attached :avatar

  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable

  devise :omniauthable, :omniauth_providers => [:facebook]
 
```
 Recipe:
```
 belongs_to :user
  belongs_to :category
  has_many :comments, :dependent => :destroy
  has_many :commented_users, through: :comments, source: :user
  has_many :user_recipes, :dependent => :destroy
  has_many :added_users, through: :user_recipes, source: :user

  has_many :ingredients, dependent: :destroy
  accepts_nested_attributes_for :ingredients, reject_if: :all_blank, allow_destroy: true

  has_many :steps, dependent: :destroy
  accepts_nested_attributes_for :steps, allow_destroy: true

  validates :name, :ingredients, :steps, :category_name, presence: true

  scope :most_commented, -> {left_joins(:comments).group('recipes.id').order('count(recipes.id) desc')}

  has_many_attached :images
```
  
 
I also had a few other models, namely:
* Comment
* Categorie
* Ingredient
* Step
* Friendship
* User_Recipe


Some of the gems I found to be great were:
1. Devise - The first model I set up was my user model. Devise worked great for setting up user authentication. After adding the devise gem to my gemfile and running bundle install, I used $ rails generate devise:install to install devise. Next, I generated the user model by using $ rails generate devise MODEL and ran rails db:migrate to set up the user table
2. Facebook omniauth - I also integrated devise with facebook omniauth to give users the option to sign in using their facebook account. I found [this resource](http://https://medium.com/@trydelight/facebook-authentication-with-devise-5b53d2f664ed) to be quite useful in setting up the integration
 
2. Bootstrap - Bootstrap was great for styling the page. In fact, I used [boostrap](http://https://github.com/hisea/devise-bootstrap-views) to create styled views for the user instead of using devise:views

3. Cocoon - I used [gem cocoon](http://https://github.com/nathanvda/cocoon) to set up my nested forms.  Ingredients and instructions were nested into the new recipe creation form.

4. Font-awesome-rails - I also used this gem to add some icons for styling purposes.

Overall, this was a fun project and I hope to expand on it in the future!
