---
layout: post
title:      "35mm app Search function"
date:       2021-01-11 21:47:14 -0500
permalink:  35mm_app_search_function
---


My assignment was to implement a search function within my application; where a user would be able to search their collection of film by name. 

In order to do this I created this method within the Film model:
```
class Film < ApplicationRecord
...
  def self.search(search)
    where("name LIKE ?", "%#{search}%")
  end
end
```
This creates the method which takes in the argument of the word we will be searching for.

Next, in the controller, we needed to accept the params that the user would be giving to us to start their search.
```
class FilmsController < ApplicationController
...
  def index
	   if params[:search]
			@films = Film.search(params[:search])
		else
			@films = current_user.films.all
		end
   end
end
```
This is saying, if params[:search] has something submitted by the user, we want to run Film.search with an argument of whatever the user submitted. This is coming from the method that we made in the Film model. else, just display all of the current users films. (This is also what loads if the user presses submit on the blank search bar.)

Finally our form:
in view/films/index.html.erb
```
...
<%= form_tag films_path, method: :get do %>
     <%= label_tag :search, "Search By Name:" %>
		 <%= text_field_tag :search, params[:search] %>
		 <%= submit_tag "Search", :name => nil %>
<% end %>
```
This is the form we set up to accept the :search param that we use in the model, to find what the user is searching for.

![https://hnet.com/video-to-gif/viewimage/20210111-13-TjdVUcW9bzUkVqCL-5ytaou-HNET](http://)
