---
layout: post
title:  Building a Rails app using Devise, Omniauth, Pundit and Nested forms
date:   2017-05-11 01:18:40 -0400
---


For the third assessment project at the Flatiron Learn Verified Online Program, I was required to build a Rails (MVC architecture) application. I built a simple online store application using authentication gems like Devise and Omniauth, and also the Pundit gem for authorization. Here is the [link](https://youtu.be/czgv3gm85zk) to my walkthrough video of this app.


 
**Conceptualization**
 
 
One of my friends has been thinking about selling stuff online. Ever since she heard that I've been learning web developing, she has asked me several times to help her build a ecommerce website. No matter she is joking or not, I thought why not? So I decided to create a Rails app that display merchadise and has simple functions that are similar to all the ecommerce sites out there, like a user can sign in and add things they want to buy in the cart, and when the users check out, the admins can view all the orders for them to process.


 
**How it works:**
 
 
Only the users that sign in as a admin are provided full CRUD capabilities (Create, Read, Update, Destroy) in creating new items for sale. Normal users can only browse through all the items and add items to their cart, and checkout when they are ready. When a user checkout, a new order is created. Only admins can see all the orders.

-Controllers: 

I have users, categories, items, carts, line-items, and orders controllers. All of them are inherit from the application controller.

-Models: 

I built user, item, category, cart, line-items, and order models. I build the associations like this: 

![](https://www.dropbox.com/s/xnwzvt6sakkhuoe/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-08%20%E4%B8%8B%E5%8D%884.50.19.png?raw=1)

It took me some time and googling to figure out how to make a user belong to a "current-cart" (which is just a cart, no difference from others) while a user has many carts.

-Views:

Start from the layout, I created a layout template with messages and navbar partials, to avoid copying over basic HTML in every erb file. In the navbar, there is a dropdown that contains links for users to access all the category pages; and of course there are also the sign in, sign up or sign out link.

There would have to be views for all the actions about items – show, index, new, edit page and a form partial for create or update a item. Same goes to carts (only show page, for users to see what's in their cart) and orders (show and index page for admins to check out).  

 
**Authentication–Devise and Omniauth**

Devise and Omniauth are two of the big topics in the curriculum, to properly intergrate these two tools into the app is challenging, but the instructions in the lessons and the [Devise documentation](https://github.com/plataformatec/devise) help me implement them in my app successfully.

Devise is a somehow complicated tool that has several features to help dealing with authentication, I only used the **database_authenticatable**, **registerable**, and **omniauthable** features. Set it up properly and it gave me all the default views and routes I can implement right away for users to sign up, in or out.

One of the requirements for this project is to give users an option to sign up with other authentication providers, such as Facebook, Twitter and Github, just like what we encounter everyday on many sites. I picked Facebook for my app. By following the procedure of setting up Omniauth from previous Learn lessons, I was able to implement it successfully in my app through Devise's **omniauthable** feature. One of the steps includes adding the following method shown below in the User model:

![](https://www.dropbox.com/s/uljy0sfx9w6upak/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-08%20%E4%B8%8B%E5%8D%8810.59.00.png?raw=1)

 
 
**Authorization–Pundit**

 
In order to restrict some users to access certain functions, we have to deal with authorization, and Pundit is a gem that take cares of this. 

First, I separate all the users into two group: normal users and administrators. Use the Rails' enum attribute by adding `enum role: [:normal, :admin]` in the user model, now all the User instances have the `#normal?` and `#admin?` methods to check their role.

Next, Pundit requires us to write **policy** for relevant models. For instance, to limit only admins and the owner of a order to access it, and only the admins can see the index of all the orders, I wrote this policy file: 

![](https://www.dropbox.com/s/xlvyi6l23zl8dh9/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-09%20%E4%B8%8A%E5%8D%8812.05.30.png?raw=1)

And in the show and index method in orders controller, we can now use the `authorize` keyword to check whether the current user is authorize to access the order it requests.

 

**Nested Form**
 
Using nested form is another requirment of this project. I wrote a **collection select** field in the item's form, so when the admins want to create a new item, they can select which category does this item belongs to in the same time. Rails make this very easy by providing the `accepts_nested_attributes_for` method. I added `accepts_nested_attributes_for :category` in the item model, and of course **permit** the categories_attributes to pass the strong params. Now when a new item is created, it is already associate with a category!
 

![](https://media.giphy.com/media/l3V0dy1zzyjbYTQQM/giphy.gif)

Overall, building this app was an amazing learning experience. Portfolio projects like this are encouraging when I see how I am now able to combine all the things I've learned so far in the curriculum and put them together. I have become more comfortable with building a Rails app from scratch and am now looking forward to implement some JavaScript to make it more dynamic in the near future.



Check out the rest of my code [here](https://github.com/johnsont426/online-store).
