---
layout: post
title:  My First Published Ruby Gem From Scratch
date:   2017-03-10 22:34:51 -0500
---


It has been three weeks since I started learning at [Learn.co online web developer bootcamp](https://www.flatironschool.com/programs/online-community-bootcamp/), and I am now at the end of the OO Ruby curriculum and just published an CLI data gem, which makes me feel a bit of sense of accomplishment.  Thanks to the wonderful and rigorous curriculums Learn offers, I am able to finish this final project smoothly. [Here](https://youtu.be/VdcfJd15u8M) is the walkthrough video of this project and the following is my programming process.

**Plan It Out**

I decided to build a gem that can take in a zip code and list the movie times that's available in the theaters around the area. So I first look for a website that I can scrap my data from. I found the website "Fandango", which serves the similar purpose to the gem I want to build. And now I have the website I can scrap and I have an idea what kind of info can I get from it, I can start thinking about what objects should I create to make this program work. I learned it from the lessons that it's better for a class to only know one other class, so I made a simple relationship diagram:


```
-CLI   
  -Scraper   #scrap theaters' name and all the attributes I want to create Movie
    -Theater   #has many Movie
      -Movie   #has attributes: title, genre, times available
```


Next, I wanted to have a better idea of how my gem will interact with the users, I typed out some pseudocodes like this:


```
1. Welcome Banner
2. Ask for zipcode
3. List the theaters around the area and ask the user to choose one
4. List all the movies in that theater and ask the user to choose one
5. Display the showtimes available for that movie in that theater.
6. Ask if the user wants to pick another theater or exit.
```

**Start Building–One By One**

Now I can start turn these pseudocodes into real codes. I started from the template directory from `$ bundle gem` . First I create the file `cli.rb` and start building a CLI class. According to my plan, I build some methods in my CLI class— `#get_zip` , to get zipcode from user;  `#zip_to_url` , turn the zipcode into a url that links to the Fandango website and can be fed to the scraper;  `#make_theater` , uses the data from the scraper to create instances of Theater;  `#add_movies_to_theater` ,  add the instances of Movie into the Theater instances...,etc. Some of the methods is still empty since the other classes are not complete yet so I am still not sure how my CLI should collaborate with them, but it's ok, I can move on to build the other classes.

Coming next is the Scraper class in the  `scraper.rb` file. I build two methods in this class— `#theater_scraper` that takes a url argument and return a array of theater's name; and `#movies_scraper` that also takes a url argument and return a array of movie hashes that contain attributes of the movies. It took me a while to figure out how to use the **Nokigiri** gem properly to get the data I want.

Lastly, the Theater class and Movie class.  The Movie class has the title, genre, and times available attributes, and the Theater
class has title and has many Movie instances.

**Using Console, "Pry", and "Raise" to Debug**

In this project, I started to get used to debug using these tools. Bugs appeared all the time, especially when I was scrapping. Learned to use "**raise**" keyword right saves me a lot of time. I can "raise" the return value of a scrapping and see its content which is very handy. Pry is useful as always, just put binding.pry at any point and I can poke around. 

**Finally...**

After all the trial and error, and all the refactoring to make sure my classes do serve their purpose and all my objects collaborate with each other, my program finally started to work! After some tests to make sure it works properly, I published it to RubyGems.org. 

This is it, my first [published gem](https://rubygems.org/gems/movies_around_you)!

**View rest of my codes [here](https://github.com/johnsont426/movies-around-you-cli-gem).**
