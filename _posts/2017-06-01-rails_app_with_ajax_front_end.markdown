---
layout: post
title:  Rails App with Ajax Front End
date:   2017-06-01 21:57:23 +0000
---


Finally, I have learned enough to intergrate some more matured front end techniques in my HomeDec ecommerce site. I decided to use Ajax on the item's show page to make my site look nicer and enhence user's experience. It seems daunting at first and I had encountered some problems, but it turns out to be another fruitful learning experience. 

**Ajax Get request**

First, I want the users to be able to switch between the product's description and the product's reviews by clicking the tabs. I use the pattern that I learned on [Flatiron School's online web developer program](https://flatironschool.com/campuses/online/), which is to bind the links with event handlers that will ask the server for more instruction (javascript), instead of writting all the codes on the client side. So the only code on client side will be fairly simple such like this:

![](https://www.dropbox.com/s/mhe8sjdoyuzldzu/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-01%20%E4%B8%8B%E5%8D%882.07.00.png?raw=1)

Once the link is clicked, a ajax request will be fired to the server (though the url provided) to ask for a javascript. The controller will respond with `show.js.erb` instead of `show.html.erb`, for the browser to execute. This is what's in `show.js.erb`:

![show.js.erb](https://www.dropbox.com/s/gow72zvzoa46ktq/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-01%20%E4%B8%8B%E5%8D%881.53.43.png?raw=1)

It ask the browser to swap the content in the item-info div. And that's it, the content in item-info div can now be changed without firing a http request!

**Ajax Post request**

Now that we can view all the reviews, of course we will have to be able to post one too. Refreshing the entire page after posting a review will be kind of annoying, so I also make the posting process more smoother using ajax.

To do this, similar to the get request, we have to bind the form with the event handler that will post the form through ajax, like this: 

![](https://www.dropbox.com/s/qx4ebkmc5dmacrb/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-01%20%E4%B8%8B%E5%8D%882.23.27.png?raw=1)

So the data from the form will first be serialized and then send to the server via ajax. After the review is created, I make the controller render the review's show page without the layout:

![](https://www.dropbox.com/s/2rgs1mf3ezl53re/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-01%20%E4%B8%8B%E5%8D%882.34.42.png?raw=1)

Then the ajax action will deal with this respond—prepend it on the top of the reviews div. Yay! my app is now more dynamic!

![](https://media.giphy.com/media/1mtIX6fY83Hji/giphy.gif)

