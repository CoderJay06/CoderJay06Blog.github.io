---
layout: post
title:      "Sinatra Portfolio Project Journey"
date:       2020-05-04 06:11:14 +0000
permalink:  sinatra_portfolio_project_journey
---

My journey through building the Sinatra portfolio project is just about finished (just need to get started on my stretch goals!). With all requirements met I've come towards the end of this section. It has definitely been a challenging experience but well worth it! Overall the Sinatra section specifically the Activerecord with Sinatra part was pretty difficult to get a grasp on but after many small struggles, screen shares and questions asked I've made it through to my final project. The specification for this project's requirements were as follows:


 .Use Sinatra to build the app
 
 .Use ActiveRecord for storing information in a database
 
 .Include more than one model class (e.g. User, Post, Category)
 
 .Include at least one has_many relationship on your User model (e.g. User has_many Posts)
 
 .Include at least one belongs_to relationship on another model (e.g. Post belongs_to User)
 
 .Include user accounts with unique login attribute (username or email)
 
 .Ensure that the belongs_to resource has routes for Creating, Reading, Updating and Destroying
 
 .Ensure that users can't modify content created by other users
 
 .Include user input validations
 
 .BONUS - not required - Display validation failures to user with error message (example form URL e.g. /posts/new)
 
 .Your README.md includes a short description, install instructions, a contributors guide and a link to the license for your code

 Going through most of these requirements was a fairly simple and smooth process, *untill things started breaking as they always do! :)*  
 
 
 **Coming up with my Project Idea**
 
 Often this can prove to be one of the most challenging parts of the process for me as I'm not the best at coming up with project ideas. Although this time around wasn't too bad. I just thought of something familiar and relevant to me as the Sinatra project planning resources suggests:
- Choose a domain you're familiar with!

- Choose a domain you care about

- Choose a domain that fits the project specs

Following this advice I chose to build a simple CRUD(Create, Read, Update, Delete) application that's for security guard reporting where security guards can conveniently create and organize their reports. I'm currently employed in security and have experience in this area so I figured this would be a good choice.
 
 
 **Planning out the Project**
 
 I first described to myself how a user would use my app. *As a user I can make a new account, delete an existing account, log in, and log out. I can Create, Read, Update, Delete daily activity reports, incident reports, etc.* I decided on a name for my project naming it [Guard Reports](https://github.com/CoderJay06/guard_reports). I named my models and their relationships, typed everything out in a Microsoft word doc, and sketched out a flowchart using [drawio](https://drawio-app.com/).
 
 
 **Building out the Project**
 
 After creating a new repo, building out my file structure following the MVC(Model View Controller) design pattern, and implementing much planning it was finally time to start coding!
 
 ![](https://media.giphy.com/media/LmNwrBhejkK9EFP504/giphy.gif)
 
 Starting from the backend I first built out my tables and migrated my database using ActiveRecord. Then created my models and their relationships.
 
 ```
class Guard < ActiveRecord::Base
   has_secure_password
   has_many :reports
 end
```

```
class Report < ActiveRecord::Base
  belongs_to :guard
end 
```
 
 I used bcrypt for securing my users passwords, hence the has_secure_password on my Guard model.
 After this process which went suprisingly smooth, I built out my routes and my views frequently testing 
 the behavior of my app and how all its components were interacting with each other by using shotgun, pry, raise and inspect. Once I had my MVP(Minimum Viable Product) up and running it was on to the bonus task which is to display validation errors for invalid input. Sounded pretty simple but turned out to be a challenge for me. I did eventually figure out how to implement this feature with my app using Activerecord and [ActiveModel Validations](https://api.rubyonrails.org/classes/ActiveModel/Validations.html) then inserting the below code into my signup view:
 
```
 <h2>Signup Here</h2>
<form action="/signup" method="POST">
   <% if @guard && @guard.errors.full_messages.any? %>
      <% @guard.errors.full_messages.each do |error_message| %>
         <p style="color:red"><%= error_message  %></p>
      <% end%>
   <% end %>
   <br>
```
 
 After all the ups and downs through my Sinatra journey I feel like I've gotten a lot out of it. I'm happy with how my project has come out thus far though I do plan to add to it and make it look prettier :).
 
 
 
 
