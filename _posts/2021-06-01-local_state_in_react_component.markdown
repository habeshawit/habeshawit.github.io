---
layout: post
title:      "Local State in React Component"
date:       2021-06-01 19:50:48 -0400
permalink:  local_state_in_react_component
---


For my final project, I worked on a React app that allows users to sell to and buy items from one another. In order to display existing items to the user, I created an 'ItemsList' component, using useEffect hook to dispatch my "getItems" action that fetched all existing items from my Rails backend API as below.

```
useEffect(() => {
	  props.getItems();
  },[]);
```

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
```

One of the functionalities I tried to add was an option for users to 'UpVote' an item. Initally, I tried to accomplish this by creating a local state (using a useState hook) that keep track of the number of times an item has been updated. I also wrote a "handleVote" function that would increment the count of UpVotes when the user clicks on it. 

```
const [count, setCount] = useState(0);

const handleVote = () =>{
    setCount(
      count +1 
 )
```

I added a button on the page, so that each item would have the UpVote option as below:

![Item List View](https://drive.google.com/file/d/10PjR-dT9RyaLDPhiMn_3siTE6BlmsU0e/view?usp=sharing)


## The Problem
Although this seemed like a quick, simple way to add this functionality, I ran into a problem. Everytime a user clicks on the upvote button, the upvote count of ALL items were incremented! Definitely NOT the user experience I was looking for. But it made sense why. I had set the state for the entire ItemsList component. So when I incremented the upvote count in the local state by clicking on "Upvote" on any item, that state was shared by all the items.

## The Solution
What I really needed was for each item on the page to have its own upvote count. What I needed was for each item to be its own component and keep track of its own upvote count. This was accomplished by creating an Item component and placing it within my ItemsList component. (Alternatively, it could also be put in its own component file and imported into my ItemList component). 

The Item component could then be created as below:

```
const Item = ({user, id, image_url, name, price, userId, handleDelete}) => {
  const [count, setCount] = useState(0);
  
  const handleVote = () =>{
    setCount(
      count +1 
    )
  }

  return <div className = "col-sm-3">
										
    {user ? 
    <div className="item-box">
        <Link to={`/items/${id}`}><img src={image_url} className="item-img"></img ></Link>
       ** <button onClick={handleVote}>Upvote</button> {count}**
        <p>{name}</p>
        <b>${price}</b>
    </div>
    : null}  
  </div>  
}
```


This would allow me to iterate through Items array and for each item, render an Item component, passing into it the properties it would need (the item's attributes, the userId, and handleDelete method) from the ItemsList parent component:

```
<div className= "row">
				{props.items.map(item => 
							<Item {...item} userId={props.user.id} handleDelete={handleDelete} key={`item${item.id}`}/>
				)}
</div>
```

What this accomplishes is that now each item is its own component and could keep track of its own local state (i.e. upvote count). The handleVote method will then update the local state by incrementing the vote count just for that item. Thus, when a user click on 'Upvote' for one item, only that item's upvote count increments. Success!

![Item List](https://drive.google.com/file/d/1qJpFhSIPecAaqdVt631QCd3PLgn5637y/view?usp=sharing)






