---
layout: post
title:      "We have so much power now…"
date:       2020-07-13 03:13:28 +0000
permalink:  we_have_so_much_power_now
---


Initial Thoughts

We have learned how to create and use databases. Just knowing that gives us the power to create more objects than we know what to do with. It’s kinda amazing that we can create thousands of objects and they’re all there in our database. Of course, that's how so many websites operate but it doesn’t make it any less powerful.

Going into the project, the requirements felt like an appropriate challenge. There’s room to make it more challenging and there’s limitless freedom with the html to make it look as you like, compared to the CLI project where output came out in a very specific way. 

Things I Struggled With

In general, I didn’t have any difficulties that stopped me from progressing further. I had issues where I didn’t figure out the problem initially but thanks to the resources I had available, I ironed those out eventually. The biggest struggle associated with my project was having to deal with life while having this on the back of my mind. I don’t think that impacted the final state of my project too much but with more time I may have added a feature or two.

One of the features I struggled implementing at first was only viewing public reviews and not private reviews. I thought it was most appropriate to have a boolean value for users to determine whether or not every review by that user was public or private vs a boolean value that had to be selected every time a review was made. What I struggled with was displaying every review by public users because I couldn’t join the two tables and get the result I wanted. The solution I came up with may not be the best but it certainly works the way I intended it to.

```
get "/" do
    @users = User.where(public: true)
    erb :'/reviews/index'
  end
```

Inside /review/index.erb
```
<h2>List of Reviews</h2>
    <% @users.each do |user| %>
        <% @reviews = user.reviews %>

        <% @reviews.each do |review| %>
```

Final Thoughts

I know this is the stepping stone to begin working with rails but this part of the journey is important because if we know what our program is doing it gives us more power to add the features we want and so on. Of course we don’t know everything about the gems we use but it would be inefficient if we don’t have one common resource we can all contribute to. There were days I wasn’t interested in the lessons throughout the mod but it’s all about pushing forward for the long run.

