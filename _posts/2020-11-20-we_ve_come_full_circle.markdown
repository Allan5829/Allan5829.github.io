---
layout: post
title:      "We’ve come full circle"
date:       2020-11-20 14:38:08 +0000
permalink:  we_ve_come_full_circle
---


Initial Thoughts

We spent so much time learning rails and now having learned JavaScript, we can combine those skills together to create applications we’d use on a daily basis. We may not be able to recreate Twitter from scratch but we can definitely come close with the skills we have now. This blog will be talking about my experience working on my Mod 4 project. 

The Project... 

The goal of this project is to make an application so as when a user interacts with the app, the app will update visually (frontend) and in the app’s database (backend). We previously used Rails to act as both the front and backend but now with JavaScript taking the role of the frontend, Rails only needs to worry about the backend. Thus a powerful combination is now in our hands. 

My project is a card collection tracker with some basic actions such as: adding a new card to a collection, deleting a card from a collection, and viewing all of your collections with their respective cards. When a user clicks “Add card”, they expect to see their card appear on the page in the right place. That’s the user’s job. The developer’s job is to add that new card to the database with the rest of the cards and make that card appear visually to the user. 

How to? (Part 1)

The magic begins with a method, called ```fetch()```, working in conjunction with Rails. We use ```fetch()``` to send an HTTP request and, if the promise is resolved, we get an object that’s received from the HTTP request we just made using fetch. 

```
fetch(`${BACKEND_URL}/cards`, configObj)
        .then(response => response.json())
        .then(card => Card.addCardToTable(card, table))
```

In order to understand the object we received, we need to understand what we send to that HTTP request and what rails does with it. For reference my "BACKEND_URL" is ```http://localhost:3000``` and the "configObj" looks like so. 

```
let configObj = {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Accept": "application/json"
      },
      body: JSON.stringify(newCard)
    };
```

The role of "configObj" is to specify what request we are making, Get vs Post, and the option to include information of a new object in the body, which in this example we do include. This specific config data tells Rails we are making a POST request to ``` http://localhost:3000/cards``` and sending this object along with it. Given everything is typed correctly and enabled we meet in Rails. 

```
def create
        card = Card.new(name: params[:name], collection_id: params[:collection_id])
        if card.save
            render json: card.to_json
        end 
    end 
```

We continue in the Create action of Cards Controller. Given our new card object saved and is stored in our database, we render our newly created card in JavaScript Object Notation aka json, and ```fetch()``` returns that displayed object for us to use however we like. 

How to? (Part 2)

We finished the backend of things and now it’s time to show the user the card they created. There’s more than one way to display something on the DOM although this is the route I went with. 

```
let table = document.getElementById(collectionOptions.value);

table.innerHTML += `<tr id="card-row-${card.name}"> <td> <button id="${card.id}">X</button> ${card.name} </td> </tr>`
```

I first find the table element that has an id that matches the name of the collection this new card is a part of. I then update it’s ```innerHTML``` with appropriate element tags and information. This is a simplification  of what happens when you click New Card/New Post/etc, however the basic principles are the same.

Wrap Up Thoughts

While I did meet some bumps in the road, I’m happy with how this project turned out. The biggest motivator while coding is seeing some visual results from it. We can work on the backend as much as we want but we don’t know if it works until we do x amount of steps. While coding with JavaScript you could say I got instant gratification from seeing something I typed show up on screen. I think the biggest takeaway from this module is that now we can create the types of websites we’d use in our daily lives. 
