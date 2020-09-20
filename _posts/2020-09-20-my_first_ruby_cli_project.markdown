---
layout: post
title:      "My First Ruby CLI Project!"
date:       2020-09-20 05:55:56 +0000
permalink:  my_first_ruby_cli_project
---

So, for my first Ruby CLI project, I decided to scrape a website for information about travel destinations around the world. It was fun and exciting but definitely challenging as well! The requirements for the project was to use an API or scraping to get data from a public website and to create a Command Line interface where users can interact with the data. 

**1. Getting started**
To start off, I had to come up with an idea, which should have been the easiest part! But it actually took me a while to find an idea I loved. Initially I started with the idea of scraping a website for information for career changers like myself! I was going to scrape data about 2020's top tech careers and display information about those careers as per the user's choice that would allow them to learn about tech career options, salaries, job descriptions, typical education entry requirement, etc. And I even found a website that displayed exactly the information I wanted to scrape. But I started with first coding the CLI before checking if the site was actually scrapable! Mistake #1. After working on it for days, and designing the interface with hard coded data, I was unable to scrape the site and so was on the search again for another site. After going through a few and even looking through API's, I decided to switch tracks. I went with the next best thing. 

I love to travel so I decided to go with my World Traveller ruby gem, which scrapes Lonely Planet for top travel highlights in each destination. This time, I made sure to check if I can scrape the information I need first before starting to code! A great way to do so was using [this](https://repl.it/repls/OccasionalCourteousViruses#main.rb)

Next, I watched a ton of videos! Avi's walkthrough of the CLI project on learn.co as well the live build [here](http://https://rb.gy/sxs1ge) were incredibly useful resources.

**2. What the Gem Does**
World Traveller gem displays a list of continents to users, asking them where they would like to explore. It then displays travel highlights for the user's continent of choice. Next, it prompts users to choose a highlight they would like to learn more about and displays details for that highlight. 

**3. Planning!**
It helped to think though the relationships I wanted my classes to have and planning before starting to code. I knew I wanted a scraper class and a CLI class and I knew I wanted to scrape a list of continents and highlights of each continent. So, the continents would have a name, a url and highlights. The highlights would also have a name, a url, details and also belong to a continent. Once I had this idea in mind, I was ready to begin. 


**4. Bundler**
Before scraping, I had to set up the structure of the gem. First thing was to run **bundle gem world_traveler** to create the gem. This was really neat as it stubbed out the structure of the gem and gave me most of the files and directories i needed, including a Readme file. But to make this work, I had to first install bundler using **gem install bundler**

**5. Coding my classes!**
I started with coding the scraper class. Unlike my initial tech career project, thankfully Lonely Planet did not put data in tables! After playing around with scraper to make sure I was getting the intended data, I was ready to start! Using **Nokogiri** I was able to successfully scrape continents and highlights.

Next i worked on my Continents class, responsible for instantiating new instances of continents once scraped when the gem runs. I then worked on a Highlights class reponsible for initializing new instances of highlights. But I didn't want all the highlights being scraped at once like the continents. That would be a whole lot of data! I had to set up the class to acess the scraper only when the user choses a highlight to look into. In order to do so, I had to link the classes by passing the return values of one class as an argument into another class.

I also had to set up the classes to check if user input was valid i.e. it was an integer and within the choices given. 

After alot of work tweeking and re-tweeking the code, it was finally working! I was able to design the user interface that I wanted. I still had a day or two before the deadline, so I decided to have a bit more fun with it and add some art and color. I used a cool gem called **[colorize](https://rubygems.org/gems/colorize/versions/0.8.1)** to get color. I also learned that you can add some ASCII art to make it add a bit of art. A google search for *"ASCII art generator"* helped me find one that worked for me.

Lastly, I wanted to publish the gem so I spend some time reading up on how to do so and created an account on rubygems.org. I had to run gem command and use **gem push** to publish.

In short, this project was not as easy as this blog makes it sound. But I definitely learned alot about using github, visual code, scraping, how gems work......the list goes on. I look forward to doing a follow up blog with more specific details!

