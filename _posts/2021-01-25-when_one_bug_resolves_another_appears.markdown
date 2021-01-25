---
layout: post
title:      "When One Bug Resolves Another Appears"
date:       2021-01-25 05:36:57 +0000
permalink:  when_one_bug_resolves_another_appears
---


The title is a reference to the classic metaphor of “When one door closes another opens.” It’s fitting in several ways because my journey as a Flatiron student will soon end and my door as a Flatiron graduate will open. The title also references the struggles of a programmer which are all too relatable. 

The post will be discussing my react redux project, mock-store. If the name was misleading in any way, my project is a recreation/clone of an ecommerce website. The goal is to recreate the same functionality as the one I’m using as reference, in this case being the American Eagle website. This project being a Single Page Application provides its own challenges due to the limitation and nature of an ecommerce website. The first obstacle wasn’t one of great progress but one of functionality.

Category Selection

Most ecommerce websites have various buttons at the top of the page that allow the user to look at items categorized based on the selected button. The challenge was using one group of code, or React Component, to show several different views. The roadblock I hit was once I viewed one type of product, Men’s for example, and clicked on another type, Women’s, the page wouldn’t be updated with different products. The key component I was missing was using `shouldComponentUpdate`. 

Before using `shouldComponentUpdate`, some routes I tested became infinite loops or React hooks that couldn’t be used in that setting. I’d spent too much time on this small piece of functionality but there was a great sense of satisfaction from successfully implementing what I had envisioned.

The last piece of code needed to achieve this is as follows.
```
shouldComponentUpdate(nextProps) {
        if (this.props.filterTerm !== nextProps.filterTerm) {
            this.props.getAllProducts(nextProps.filterTerm)
        }
        return true
    }

```

I pass down a `filterTerm` prop instead of updating the Redux Store’s state because state wouldn’t be updated at the point in time `shouldComponentUpdate` is triggered, while a passed down prop is instantly available. If I used state then the page would render with the same `filterTerm` and would appear that a button that should show Women’s products is showing Men’s products. 

The following code is the respective action used and reducer case for `getAllProducts`.
```
export const getAllProducts = (filterTerm) => {
    return (dispatch) => {
      dispatch({ type: 'LOADING_DID_MOUNT'})
      fetch(URL + '/products')
      .then(response => response.json())
      .then(p => dispatch({ type: 'INDEX_PRODUCTS', payload: p, filterBy: filterTerm }))
    }
  }
```

This is a standard action whose role is to get data to display and it’s possible with redux-thunk, allowing us to return a dispatch to the reducer.

```
case('INDEX_PRODUCTS'):
            switch(action.filterBy) {
                case('Men'):
                    return {...state, loading: false, sliceStart: 0, sliceEnd: 8, 
                        products: action.payload.filter(p => p.gender === "Men")}
                case('Women'):
                    return {...state, loading: false, sliceStart: 0, sliceEnd: 8, 
                        products: action.payload.filter(p => p.gender === "Women")}
	    ...
                default:
                    return {...state, loading: false, sliceStart: 0, sliceEnd: 8, 
                        products: action.payload}
            } 

```
By including `filterTerm` in the dispatch, I’m able to control what data is saved to the state by filtering out data that I don’t need at that point.

Page Numbers

A different feature that granted, didn’t have me attempting different solutions for hours, still gave me satisfaction upon achieving it. This feature is having page numbers/buttons that display different products based on the page. If you look at the previous code snippet, there’s some values `sliceStart` and `sliceEnd` whose purpose is to be used to see which set of products should be displayed. Those values are stored and updated in the Redux Store’s state.

The reducer case that updates those values is like so. 
```
case ('UPDATE_PAGE'):
            return {...state, sliceStart: ((action.payload - 1) * 8), sliceEnd: (action.payload * 8)}
```

It’s simple and efficient, simply needs an integer value which in this case is the page number the user clicks.

The piece of code that uses those slice values is the same code that iterates through all the products received from `getAllProducts`.

```
const allProducts = this.props.products.slice(this.props.sliceStart, this.props.sliceEnd).map( p => {
            return < ProductComponent key={p.id} product={p}/>
        })

```

This non-destructively copies the data we want and ignores the rest which allows the user to click the next page with the following products loading quickly.

Wrap Up Thoughts

While I’m proud of what I made, I didn’t satisfy my personal goals for this project within the timeframe allotted. The plan is to continue working on this application to make it a more finished project with the ideas I still have in mind. 

The journey after this will involve learning more, perfecting my craft, and selling myself to potential employers. Here’s to what the future has in store (hopefully better than 2020 overall).

