---
layout: post
title:  "Using Handlebars Template In My Rails App"
date:   2017-06-04 04:32:15 -0400
---


Now that know how to use [Handlebars](http://handlebarsjs.com) template, I want to use it in my HomeDec app and refactor some of my codes. **(Go to my last three posts to read more about this app! And click [here](https://youtu.be/CJ8D2alZJOk) to watch a quick walkthrough video of this app)**

The part I wanted to change is the process of posting new review. In order to use Handlebars, I need the server to respond the Ajax post request with the json of the newly created review. To do so, simply ask the controller to render json:

![](https://www.dropbox.com/s/l7jrosq8j483efd/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-03%20%E4%B8%8B%E5%8D%8811.26.30.png?raw=1)

Now in our success function, we can feed this json to the Handlebar template. The template I attached at the bottom the show page is this:

![](https://www.dropbox.com/s/sj43ctnjrhg61j6/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-03%20%E4%B8%8B%E5%8D%8811.42.23.png?raw=1)

Here I use a custom helper `times`, which I registered by adding this in the script:

![](https://www.dropbox.com/s/3t72gmmax4rt1sr/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-03%20%E4%B8%8B%E5%8D%8811.58.58.png?raw=1)

this helper allow the template to loop as many times as the number of the stars, to show the right amount of the stars. 

In addition, I created a Review class so all the functions can be stored as class methods, and can be passed around. At the end, my codes in `new.js.erb` look like this:

![](https://www.dropbox.com/s/kmhddoj6agmaqst/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-04%20%E4%B8%8A%E5%8D%881.20.22.png?raw=1)
![](https://www.dropbox.com/s/itvrbljljstxp8q/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-06-04%20%E4%B8%8A%E5%8D%881.20.37.png?raw=1)

Nice! By refactoring my codes this way, now they looked more mature and easy to follow. 

**See rest of my codes [here](https://github.com/johnsont426/online-store).**
