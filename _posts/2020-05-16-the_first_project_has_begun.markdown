---
layout: post
title:      "The first project has begun... "
date:       2020-05-16 05:37:29 -0400
permalink:  the_first_project_has_begun
---


Completed Project Retrospective 

In terms of projects, I think this is a good level of difficulty as the first project for software engineering. In the beginning, the project seemed more difficult than it really is but after I watched the CLI Gem Walkthrough, it looked like a combination of the Music Library CLI and the Student Scraper. There wasn't anything we hadn't learned before that we had to implement and it felt familiar to me, other than creating, mostly, everything from scratch. 

The theme around my project was manga because I enjoy reading them and there was a convenient page that had a list of every manga on that specific website with a link to get more information for each manga. For those of you who have no idea what manga is, think of it as a Japanese version of a comic book. It met the criteria for the project needs, it was something I'm interested in, and I could personalize it to make it unique to myself.

Things I Struggled With

Out of everything, the part I struggled with the most was getting the project created, in terms of files and such. It sounds funny but using github to create a repository, constantly updating the "master" repository, and having to save my project in a specific way was all new to me. I have no doubt it knowing this will help me in the future but it was still hard to get a grasp as well as frustrating because we were spoiled by the browser Learn IDE since it conveniently saved everything for us. I slowly got used to it but the biggest hurdle was definitely first creating it.

Ah scraping, I sure love how one-dimensional it is, right. Okay sarcasm out of the way, I expected scraping to give me trouble purely for the fact that I'm not used to it nor have I done it enough to feel super comfortable. I probably have to give some credit to the website I used because each manga has a unique url with information formatted in the same way as the rest of the manga urls. That made it very convenient for scraping the same type of data for every manga in one fell swoop. To my surprise, the scraping process as a whole wasn't as hard as I expected, except one part with getting certain urls. This issue was I either scraped one specific url that I didn’t intend to or I scraped each one into one object and that caused other issues. With some help, I was able to access each url individually by using `.search` on the appropriate class/selectors and going through every url with `.each`. 
```
doc.search("div.g-3.g-3--md.mar-b-lg a").each do |div| #searches through every url
            if div.attributes["href"].value.include?(MangaScraper.change_into_href(manga_name)) 
```                                                                                  ^ above method changes a name like One Piece into one-piece

Last Thoughts

I really liked the process I used which was working from the top down. I used “fake data” to first implement the CLI and once it had the intended use, I focused on scraping. It helped set up a list of instructions in my head of what to do next and that was really helpful. 

I’m glad I refactored the way I scraped the information needed because now if I want to add another manga to be a part of the CLI, all I have to do is add it as a string in an array. Given that the name is formatted the same way on the first url I scrape with every manga listed. For me, it’s really satisfying when I simply type “Black Clover” in the array needed and my code will scrape everything needed to make a new object as if the manga was always going to be used in the first place. It makes it really easy to customize it and that’s really satisfying from a developer standpoint. 

This project went pretty smooth, beside for the few issues, and hopefully future projects follow suit. 
