---
layout: post
title:      "CLI Portfolio Project "
date:       2020-02-02 21:41:07 +0000
permalink:  cli_portfolio_project
---


I'm writing this blog after completing my very first portfolio project here at Flatiron. This process has taken me a bit longer than expected but I believe I did a pretty good job with it in the end and checked off all requirements. At first it felt intimidating to have to start this from scratch being that up until this point I've only been completing lessons and labs with prewritten tests, but I knew I just have to beleive in the curriculum and what I've learned thus far. I first watched some of Avi's CLI prep videos to give me an idea on how to get started which helped a lot . The first task is to find a website to scrape data from or to use an API. So I started searching for a scrapeable website which proved to be fairly difficult for what I was looking for. My project idea was to make something that had to do with boxing since boxing has been a big part of my life over the years, having been doing it since childhood and always watching the fights on tv. So I decided my plan would be to make a CLI Ruby gem that scrapes all the data on upcoming fights. Once I found a scrapeable site which I had tested with the Scraper Checker provided in the instructions, I began the process of planning out what my app will do, what the user experience will be, what to do with the data once I have collected it, what classes need to be built and how the data will be displayed to the user. I started with making a flow chart as suggested on the project planning form. 

![](https://lh3.google.com/u/0/d/1bGSTsyyrLcugxnTiVBlx5bOdTCDDSm9_=w1280-h671-iv201)

Before getting to the actual coding I decided to type out the classes I would need to make, their responsibilities and all other ideas  into a project notes file. My three classes I named are Fight, Scraper and CLI class. I found all the data I would need using Nokogiri and CSS selectors so I wouldn't have to worry about that once I started coding. After building out my classes and  typing out the user interface , the challenge of building the right methods in each class was the next step. My first would be my scraper method which would scrape all the data needed, make a new object from my Fight class and assign everything to Fight object attributes. 

```
def self.scrape_scheduled_fights
    content = self.open_scheduled_fights.css("div.schedules") 
    number_of_fights = open_scheduled_fights.css(".vs").size
    i = 0
    while i <  number_of_fights
      fight = BoxingSchedules::Fight.new
      fight.channel_location = content.css("p.fight-channels")[i].text.split.join(" ")
      fight.fighter_names = content.css(".schedule-details-block div div")[i].text.split.join(" ").strip
      fight.fight_time = content.css(".schedule-time-block")[i].text.split.join(" ")
      fight.fight_details = content.css(".schedule-details-block")[i].text.split.join(" ")
      fight.fight_url = "https://schedule.boxingscene.com/" +  content.css("a")[i].attr("href")
      fight.save
      i += 1
    end
  end
	
```

With some help I eventually got the above method working and displaying the data I needed it to. This method  uses css selectors to open the part of the webpage I need and get the number of upcoming fights to loop through, assigning both to variables. It's then making new Fight class objects and assigning all details needed as the object attributes before saving it all to the Fight class. The next challenge is having it all get displayed to the user in a clean and structured look. Using the CLI class to call on the Scraper method and iterate over all objects saved to Fight class I eventually had it displaying everything how I wanted. The only problem was making my CLI class mored DRY(Don't Repeat Yourself) but metaprogramming proved to be very useful here by using `.send()` I was able to make my application more flexible and dry. In the end I feel like I learned a lot and had an overall good experience with this project.













