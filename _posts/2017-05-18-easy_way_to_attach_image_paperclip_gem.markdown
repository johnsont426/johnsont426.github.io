---
layout: post
title:  Easy Way to Attach Image—Paperclip Gem
date:   2017-05-18 04:51:48 -0400
---


Still working on my HomeDec Rails app and try to make it better. Today I learned about a wonderful tool to attach images to a model: the Paperclip gem. In the previous version of this app, I provided a field for an admin to type in the url of the image when they want to create a new item. Now with Paperclip, instead of just key in the url string, we can select a image file from our local device and attach it directly. Here is how:

**Adding a image to a item**


Before everything, of course, is to include `gem 'paperclip'` in the gemfile and run `bundle install`. 

First thing to do, is to wire up the model to use Paperclip's `has_attached_file` method, and tell it what attribute name we want to use to access the attached file. I simply just use image. And we also need to include the `validates_attachment_content_type` validator that is provided by Paperclip in the model too, to make sure we get an image file when we expect one.

![](https://www.dropbox.com/s/63d9gcp325lbbti/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-18%20%E4%B8%8A%E5%8D%881.04.59.png?raw=1)

Next, I add the `image` field in my items table by running

    `rails g paperclip item image`

which is provided by Paperclip, to generate a migration. Then, of course, run `rake db:migrate`.

Now to the form, we need to give the users a way to upload the image by adding the file_field helper to generate the appropriate input and "choose" button to attach the file:

![](https://www.dropbox.com/s/bntugbadye1edfm/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-18%20%E4%B8%8A%E5%8D%881.17.55.png?raw=1)

Finally, we need to update our strong params in the controller to allow the new image field to be used for mass assignment.



**Displaying the image**


To display the images, simply use the url method provided by Paperclip in the views so that no matter where the images are stored, we can always use them in an image_tag:

![](https://www.dropbox.com/s/bup85si8qi9otz8/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-18%20%E4%B8%8A%E5%8D%881.35.12.png?raw=1)

How convenient! Now I don't have to do any copy and paste job and let the Paperclip take care of all the image-attaching work for me. Another beautiful day of learning new stuff!

![](https://media.giphy.com/media/94OPiy03NXCiQ/giphy.gif?response_id=591d6045423427cae1a04b05)


Paperclip also come with other handy features, such as setting default image and generating thumbnails. To learn more, go to [Paperclip's documentation](https://github.com/thoughtbot/paperclip). 



