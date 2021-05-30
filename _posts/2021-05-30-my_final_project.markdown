---
layout: post
title:      "My Final Project"
date:       2021-05-30 06:54:33 +0000
permalink:  my_final_project
---


For my final project, I worked on a React App with a Rails API backend. Initially, the project started out with a simple inventory system for a small store but as I worked on the project, I wanted to expand on the idea as I thought it would be a great way to learn more about react. So, I decided to expand it to be a simple app where users can buy and sell items, making sure the project lined up with the expectations below:

* Use the create-react-app generator to start your project.
* Your app should have one HTML page to render your react-redux application
* There should be 5 stateless components
* There should be 3 routes
* The Application must make use of react-router and proper RESTful routing
* Use Redux middleware to respond to and modify state change
* Make use of async actions and redux-thunk middleware to send data to and receive data from a server
* Your Rails API should handle the data persistence with a database. You should be using fetch() within your actions to GET and POST data from your API - do not use jQuery methods.
* Your client-side application should handle the display of data with minimal data manipulation
* Your application should have some minimal styling

## Backend

To set up the backend, I set up the following associations:

```
class Category < ApplicationRecord
    has_many :items
    validates :name, presence: true
end


class Item < ApplicationRecord
    belongs_to :category
    belongs_to :user
    validates :name, presence: true
end

class User < ApplicationRecord
    has_many :items
    has_secure_password
    validates :username, presence: true
    validates :email, uniqueness: true
end

```

I set up the files to include respective controllers and serializers as below:

![](https://drive.google.com/file/d/1DzpewCSWZ3_I_FTq4VOP7iAErN7-LNgl/view?usp=sharinghttp://)

To set up the database, I ran the following commands:
```
rake db:migrate
rake db: seed
```

## Frontend

To create the react app, I ran create-react-app, following the instructions at [this repo](http://https://github.com/facebook/create-react-app)

I started out with setting up redux to manage the app's state, such as user, item, and category states. In the redux directory, I set up actions and reducers. Whereas the actions are responsible for running actions such as fetch to get and post data from the backend, reducers determine the changes made to the app's states. For my particular project, for instance, my item actions and reducer look like this: 

ItemActions.js
```
export const getItems = () => {
    return (dispatch) =>{
        fetch('http://localhost:3001/api/v1/items')
            .then((res) => res.json())
            .then((items) => 
                dispatch({
                    type: 'FETCH_ITEMS',
                    payload: items
                })
        )
    }   
}

export const createItem = (newItemData, history) =>{    
    return(dispatch) => {        
        fetch('http://localhost:3001/api/v1/items', {
            headers: {
                'Content-Type': 'application/json',
                'Accept': 'application/json'
            },
            method: 'POST',
            body: JSON.stringify({item: newItemData})
        })
        .then((response) => {
            if(response.ok){
                return response.json();
            } else {
                throw new Error(response.statusText);                
            }
        })
        .then((item) => 
            (dispatch({type: 'CREATE_ITEM', payload: item}),
            history.push('/items'))
        )
        .catch((err) => 
            dispatch({
                type: 'ERROR', 
                payload: "Error creating item. Please enter a name"}))
    }
}

export const deleteItem = (itemId, history) => {
    return(dispatch) => {        
        fetch(`http://localhost:3001/api/v1/items/${itemId}`, {
            method: 'DELETE'
        })
        .then((res) => res.json())
        .then((item) => 
            (dispatch({type: 'DELETE_ITEM', payload: item}),
            history.push('/items'))
        )
    }
}
```

ItemReducer.js
```
export default (state = [], action) => {
    switch(action.type){
        case 'FETCH_ITEMS':
            return action.payload
        case 'CREATE_ITEM':
            {
                alert(action.payload.message)
                return [...state, action.payload]
            }           
        case 'DELETE_ITEM':                   
            {alert(action.payload.message)
            return [...state, action.payload]}
        case 'ERROR':
            {
            alert(action.payload)
            return  [...state, action.payload]
            }
        default:
            return state;
    }
}
```

With Redux setup, I could map the states to props and pass those props on to different components. Although this was only the beginning, I felt like it was a good place to start before. 

Overall, it was a fun project to work on and look forward to writing a more detailed blog about the experience.
