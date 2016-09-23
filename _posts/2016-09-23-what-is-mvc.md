---
layout: post
title: What is MVC? 
---
 

What is MVC?

The MVC framework stands for Models - Views - Controllers and is the basic structure of any Rails application (although not used exclusively in Rails).

How does MVC work?

For a web application to be more than a static website, it needs a few components: the browser for user interaction, a database to store information, and a way to communicate browser actions to the database.

MODEL

The model represents the database – the data stored and the actions you can perform to manipulate the data. Rails’ models are based on ActiveRecord (docs here). An app can have any number of models based on the groups of items that an app needs.

For example, for a simple blog application, you may have a User model to store user information, a Post model to store posts that a user creates, and a Comment model to store comments made on each post. Each model will also contain attributes, or characteristics of the data.

User may have username, email, password attributes.

Post may have title and body.

Comment may have body.

Models are generally related to each other – they are the building blocks of your application. For the example above, a User has many Posts and has many Comments; a Post belongs to a User and has many Comments, and a Comment belongs to both a User and a Post.

VIEW

The view represents what you see on a browser page – data from the database is displayed to a user. This is where the front-end magic comes to life, mixing HTML/CSS with Ruby and Javascript, jQuery and more!

View files in a Rails application are saved as name.html.erb – .erb stands for Embedded Ruby and allows us to mix Ruby syntax with HTML.

In the example blog application, you may have a Post#Show view that displays a single post or a Post#Index view that displays a list of posts. The Post#Show view could also include a section that displays comments for that post. You could also have a User#Show view to display a list of all posts by that user.

Each view has a name that corresponds to a controller action – make sure the view name and the controller name matches, including any namespaces, to ensure that they communicate properly.

CONTROLLER

So what is a controller?

The controller handles all interactions between a user from the view and the data in the models. This is where all the action happens, from creating/deleting new objects to displaying objects. When a user clicks a button on a view, some kind of corresponding action is taking place behind the scenes in the controller, and this action is generally manipulating model data.

Let’s take a Post Create action: when a user has finished writing the blog post in the browser and clicks “Publish”, the Post Controller will look for the create method that might include code similar to the following:

{% highlight ruby %} 
   def create
     @post = Post.new
     @post.title = params[:post][:title]
     @post.body = params[:post][:body]

     if @post.save
       flash[:notice] = "Post was saved successfully."
       redirect_to @post
     else
       flash.now[:alert] = "There was an error saving the post. Please try again."
       render :new
     end
   end
   {% endhighlight %}
   
   
A new instance variable @post is created as Post.new. Then, the method sets the @post.title and @post.body equal to the content that the user has inputted via the view. If the @post.save goes through without errors, the page will direct to display the @post in a view.

 

When I first started learning the MVC framework, I found Rails for Zombies to be the most helpful in wrapping my mind around how the different components work together. Playing around with basic apps such as a blog apps can also help visualize the basic functions in the MVC framework.

 

