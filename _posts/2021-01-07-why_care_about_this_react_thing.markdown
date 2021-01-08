---
layout: post
title:      "Why care about this “React” thing?"
date:       2021-01-07 19:16:31 -0500
permalink:  why_care_about_this_react_thing
---


As people, or programmers, we tend to get lazy and look for shortcuts. From the time perspective, why take an hour to make something from scratch when you could be done in half the time with something partially made. In some areas, such as cooking, this makes a huge difference in quality, although code can have identical quality with different amounts of time spent. This is where React comes in, why build the same library of code every time one starts a new project when it’s faster, and more likely polished code, to use an existing one. React is a Javascript library whose goal is to create an application with complex user interfaces as well as reusable, isolated pieces of code.

Components

The pieces of code that React uses are called “components” and they are what allows us to structure our app. We’re able to relegate certain parts of our app to certain places. Using Youtube as an example, there’s a place for navigation buttons, for subscribed channels, videos, and more. Instead of figuring out how to present that information at the same time, we use components to compartmentalize certain roles for our app. In the case of navigation buttons, we’d regulate the role of presenting and applying logic for those buttons to one piece of code, often called “containers”.

The container for these buttons would present other components that represent the buttons themselves. The goal here is to have 2 or 3 pieces of code represent one section as opposed to having all of the code in one place. The benefit is that the simple pieces of code we write can be used in other applications, given they aren’t written in a very individualized way. These types of components are known as presentational and container components.

Presentational vs Container

The difference between them is relatively simple, container components handle the logic and pass down relevant information while presentational components take that information and present that information in the same fashion as it would appear normally or in the elements section of developer tools. Of course, we can have one piece of code handle both the logic and information but in the end it comes down to writing clean code that has a specific purpose. 

The following pieces of code will help illustrate the idea. Credit to @chantastic for the code examples.

```
// CommentList.js
import React from "react";

class CommentList extends React.Component {
  constructor() {
    super();
    this.state = { comments: [] }
  }
  
  componentDidMount() {
    fetch("/my-comments.json")
      .then(res => res.json())
      .then(comments => this.setState({ comments }))
  }
  
  render() {
    return (
      <ul>
        {this.state.comments.map(({ body, author }) =>
          <li>{body}-{author}</li>
        )}
      </ul>
    );
  }
}
```

Assuming there is a basic understanding of React, `componentDidMount()` is responsible for receiving information to be presented and `render()` returns something to be presented, which in this case is comments. While the amount of information being presented is currently small and easy to handle, that will soon become harder to handle as the size of the app increases with more information being processed. The next two pieces of code will show how one could separate CommentList into a presentational and a container component.

Container
```
// CommentListContainer.js
import React from "react";
import CommentList from "./CommentList";

class CommentListContainer extends React.Component {
  constructor() {
    super();
    this.state = { comments: [] }
  }
  
  componentDidMount() {
    fetch("/my-comments.json")
      .then(res => res.json())
      .then(comments => this.setState({ comments }))
  }
  
  render() {
    return <CommentList comments={this.state.comments} />;
  }
}
```

Presentational
```
// CommentList.js
import React from "react";

const Commentlist = comments => (
  <ul>
    {comments.map(({ body, author }) =>
      <li>{body}-{author}</li>
    )}
  </ul>
)
```

While these two pieces of code are different from the first `CommentList`, they are identical in what they do and present. The other important idea is we have a reusable piece of code in the form of the second `CommentList` that can be used with other apps upon changing a few values. This allows for code that has a specific purpose and can be easily organized.

State

Another feature of React is "state", which in other words can be categorized as a convenient location for information that can/tends to change. It's the storage for information that we may want to present to the user and one use is storing the information we receive from fetch as used in `CommentListContainer`.

```
constructor() {
    super();
    this.state = { comments: [] }
  }
  
  componentDidMount() {
    fetch("/my-comments.json")
      .then(res => res.json())
      .then(comments => this.setState({ comments }))
  }
```

We can think of state as one big binder and in this case comments are a folder while the comments themselves are pages within the comments folder. We can add as many folders as we want to this metaphorical binder, being state, and store information that we want to keep track of. This convention is just another one of the features that React brings along with its library. 

Coding something from scratch is great and something to be proud of although we don't have to "reinvent the wheel" everytime we start working on a new project. React helps us get off of the ground and have something functional as well as presentable with minimal effort. If this happens to be your first time hearing about React, consider doing some research to see if this is something you may want to use.

