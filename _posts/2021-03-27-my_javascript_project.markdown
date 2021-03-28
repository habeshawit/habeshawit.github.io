---
layout: post
title:      "My Javascript Project"
date:       2021-03-28 03:40:00 +0000
permalink:  my_javascript_project
---


For my Javascript Project, I initially worked on an app that allows users to buy and sell books from one another at discount prices. I, being a student, know how expensive books can be, particularly those you use for just a semester! So, that was my initial inspiration for the project. After building the MVP for this project, however, I realized that for the app to be used as intended, a user model was crucial. Given the time constraint to finish the project, I decided not to work on the additional user model and authentications as my intention was to build a simple app with relatively simple functionalities. So, I did what I would never advise anyone to do and switched project ideas! 

I decided to create an app called My Devotional, which is an app that allows users to create and save their daily Bible devotions or reflections on scripture that they read that day. As it uses a very similar structure and premise as my initial idea, making the switch was not difficult. I set up the project into two repositories: a backend repo (using rails) and a frontend (using html, css, and javascript)

I set up my rails backend api by first running:

```
rails new <my_app_name> --database=postgresql --api
```

For this app, I only had two models: a category model and a devotion model:

```
class Category < ApplicationRecord
    has_many :devotions, dependent: :destroy
end

class Devotion < ApplicationRecord
   belongs_to :category 
   validates :title, presence: true
end

```

Each model had the attributes as shown in the db schema below:

```
create_table "categories", force: :cascade do |t|
    t.string "name"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

  create_table "devotions", force: :cascade do |t|
    t.string "title"
    t.string "date"
    t.string "verse"
    t.string "content"
    t.string "image_url"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.bigint "category_id", null: false
    t.index ["category_id"], name: "index_devotions_on_category_id"
  end
	
	add_foreign_key "devotions", "categories"
```

I set up the routes as follows, using namespacing to organize the controllers and allow for version control:

```
Rails.application.routes.draw do
  namespace :api do
    namespace :v1 do
      resources :devotions
      resources :categories
    end
  end

end

```

Once the backend was complete, I linked to to the front end by setting the fetch endpoint to "http://localhost:3000/api/v1/devotions" so that the front end can communicate with the backend. 

Overall, although I stuck to just the mvp for this project, I felt like I learned alot. I look forward to expanding on it further in the future
