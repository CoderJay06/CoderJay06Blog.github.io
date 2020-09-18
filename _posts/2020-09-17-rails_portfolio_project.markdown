---
layout: post
title:      "Rails Portfolio Project "
date:       2020-09-18 00:35:43 +0000
permalink:  rails_portfolio_project
---



After lots of challenges and bugs, I'm coming towards the end of my rails project with the requirements done and my MVP up and running. In the beginning, it took me a while to figure out what exactly I wanted to build. I did not want to make something too common such as another todo app but I didn't have many ideas. After searching around the web a bit I came across this site which listed [simple web app ideas ](https://flaviocopes.com/sample-app-ideas/#a-book-database) and it helped give me an idea of what I'd like to build. My final decision was to build a library app for Software Development books. 


**Planning**
<iframe src="https://giphy.com/embed/ggX0rPlSMJZIQYHon6" width="400" height="280" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/memecandy-ggX0rPlSMJZIQYHon6"></a></p>
For the planning part of my project, I started with a word doc to jot down all the requirements and what my models would be and their associations. I then filled out the project planning resources and followed the steps that the curriculum suggests. I gave wireframing a shot to end with, drawing out my templates in a notebook and using this really cool site for wireframing [Wireframe.cc](https://wireframe.cc/) which I found simpler to use compared to Figma.

**Coding**
<iframe src="https://giphy.com/embed/3oKIPnAiaMCws8nOsE" width="280" height="300" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/cat-kitten-computer-3oKIPnAiaMCws8nOsE"></a></p>
After setting up my project repository and jotting down my plans in a .md file it was time to start coding. For my first steps I followed the usual flow of generating my models and controllers then migrating the database. Then came the part of building out my model associations. The associations I came up with were the following:

User:<br> has_many :reviews<br>
  has_many :downloads<br>
  has_many :books, through: :downloads<br>
	
Book:<br>
   belongs_to :author<br>
   belongs_to :category<br>
   has_many :reviews<br>
   has_many :downloads<br>
   has_many :users, through: :downloads<br>
	 
Category:<br>
  has_many :books<br>
	
Review:<br>
  belongs_to :user<br>
  belongs_to :book<br>
	
Download:<br>
  belongs_to :user<br>
  belongs_to :book<br>
	
Author:<br>
  has_many :books<br>
	

Once my model associations were how I wanted them I was able to move on to the next task. I included some basic validations and some more specific validations such as `URI::MailTo::EMAIL_REGEXP ` for my user's email. You can read more about the `URI::MailTo` ruby method  [here](https://ruby-doc.org/stdlib-2.5.3/libdoc/uri/rdoc/URI/MailTo.html).  Including a class level ActiveRecord scope method was next. I decided to make a scope method for recently added books, so the url looked like: `books/recently_added` and my scope method which I added to my Book model: `scope :recently_added, -> { order("books.updated_at DESC LIMIT 10") }`. Moving along the requirements spec I built out my forms for signing up, logging in, creating, and editing. Another step was to add Omniauth functionality to the application. I decided to add Google Omniauth, this turned out to be a bit challenging but using the following videos really helped me figure things out: [TodoMVC - Implementing Omniauth](https://www.youtube.com/watch?v=UAvuo-EbTFY&feature=emb_title) & [Rails - MyBlog Project Build Pt 4](https://www.youtube.com/watch?v=n8ZIzH5Ol-Q&t=1124s). My next requirement was to include nested resources for the show or index page. I added these for my book reviews by using the following code in my routes file:
```
  resources :books do 
    resources :reviews
  end
```
Some of the routes this generated are `books/:book_id/reviews` for a book's reviews & `books/:book_id/reviews/new` for creating a new review. The next requirement was to Include form display of validation errors. This was fairly simple, after reading through the [Active Record Validations](https://guides.rubyonrails.org/active_record_validations.html#displaying-validation-errors-in-views) docs in the 'Displaying Validation Errors in Views' section I added the code for displaying errors to each of my forms. 


**Refactoring**
<iframe src="https://giphy.com/embed/Lntt6Vee77UeiLf4aD" width="280" height="300" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/Veeam-code-refactoring-veeam-Lntt6Vee77UeiLf4aD"></a></p>
After finishing the basic requirements from the project specification the last but not least requirements were:
 .The application is pretty DRY
 .Limited logic in controllers
 .Views use helper methods if appropriate
 .Views use partials if appropriate
This called for some refactoring. Although refactoring can be challenging I find it to be one of my favorite parts of coding. 
I started by moving most logic I had in my controllers into their associated models then moving repetitive forms and error messages into partials with locals to make my code much more dry and then modified my routes file to use more resources for my routes instead of hard coding them. I would suggest following the [Rails style guide](https://github.com/rubocop-hq/rails-style-guide) as it helped me a bit with this process.

**Designing**

I do not have much to add here because I'm still in the process of designing the front end of my app but I decided to use Bootstrap for this part which was pretty simple to set up with Rails if you just follow along with the video I used [How to use Bootstrap with Webpack & Rails](https://www.youtube.com/watch?v=bn9arlhfaXc) and also Avi's video was a great resource for this [Find a Pair 6 - Adding a Frontend](https://www.youtube.com/watch?time_continue=3009&v=Vsr3wWoxUrQ&feature=emb_title).



**Things I've learned**

Some things I've learned from this project are: 
- Make sure to put enough time into planning before coding, I feel like I could've done a bit better with this and would've gone through the requirements faster if I did better planning. 
- Utilizing Flatiron's resources such as the videos can really help when you are stuck.
- Last but not least, make sure to attend project meetups (even if you don't think you need help with anything it can be very helpful to see what other students are struggling with and it's good for communicating with other students who are in the same part of the curriculum as you're).
