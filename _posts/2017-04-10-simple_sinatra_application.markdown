---
layout: post
title:  Simple Sinatra Application
date:   2017-04-10 04:04:37 -0400
---


I have dived into Sinatra curriculum for about two weeks, and finally it's time for the final project. Here is the [link](https://youtu.be/KYlVWLj640Q) to the walkthrough video of this project. Sinatra is just another Ruby library that helps us build a web application faster—well, not fast enough, since the point of learning Sinatra is to warm up for the real deal—Rails. But through learning Sinatra, I started getting the hang of the idea of MVC (model-view-controller) framework, and the RESTful architectural style.

In this project, I built a small application that can help me organize my camera bags. I love photography, like every other photographers, I have several cameras and quite a few lenses. I love to take my gears with me when I  go to a trip and take beautiful pictures, but at the same time I don't want my bag to be too cumbersome, so I always want to know how heavy will my camera bag be so I can decide what to bring and what not to.

**Model**

To start, I know there will be four models in this domain, which are user, bag, camera, and lens. So I went on and create four migration file for each of the four tables. Next, I build the model files for each of them, now we have the M part and the database ready. 

**Controller**

Then here comes the C part. The controllers is like waiters in a restaurant, who are in the middle of the patrons and the chefs, to tell the chef what to cook for the patrons and serve the courses that are prepared by the chefs to the patrons. And in this metaphor, the chefs are the models on the server side, and the patrons are the views that the clients will see when they send the request to the server.

In the controllers, we defined each of the http actions following the REST convention to allow us to CRUD(create, retrieve, update, and delete)  the data. For example, for the bag model, the actions are:

```
get '/bags'              #render the index page

get '/bags/new'       #render the form for creating a new bag

get '/bags/:id'          #render the show page to display the info about the specific bag

post '/bags'             #create a new bag using the data from the form

get '/bags/:id/edit'   #render the form for editing an already existed bag

patch '/bags/:id'      #update the bag using the data from the form

delete '/bags/:id'     #delete a bag
```

These are the seven conventional restful routes.

**View**

Finally, we have to build the index, show, new and edit pages for the clients to display. Each of them are written in erb, the embedded Ruby code, which is basically blending Ruby code in html. It is very interesting to learn that the data from a form will be passed to the post action through the `params` hash and also that we can pass the data from a controller to a view using instance variable.

After some time figuring out all the tricky part of the interaction between M, V and C, I finally got [my application](https://github.com/johnsont426/camera-bag-organizer) running! While everything started to work and make sense, when I was writing this project, I felt that there are many repetitive codes and I have to hard code many things. I know that Sinatra is just a light weight framework, so I can't wait to learn the more sophisticating Rails library.

**View the rest of my codes [here](https://github.com/johnsont426/camera-bag-organizer).**
