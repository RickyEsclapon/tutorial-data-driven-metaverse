# Data-driven tools and experiences in the metaverse



## Completed code reference

### First example button:
```js
i = 1

feature.on('click',e=>{
  
  console.log('hello')
  
  i++
  console.log(i)
})
```


### Get player info:
```js
feature.on('click',e=>{
  
  console.log(e.player)
  
  console.log(e.player.wallet)
  
  console.log(e.player.name)
  
})
```


### Update text sign:
```js
let text_sign = parcel.getFeatureById('welcome')

parcel.on('playerenter',e=>{
  
  console.log(e.player.name)
  
  element.set({text: 'welcome ' + e.player.name + '!'})
})
```


## Part 2: https://youtu.be/veJj-Q3W84I

### POAP example

Show the user their most recent POAPs.

#### GraphQL data from The Graph

Subgraph: https://thegraph.com/legacy-explorer/subgraph/poap-xyz/poap-xdai

GraphQL Request Template:
```js
  fetch('[ENDPOINT LINK HERE]', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    query: `
        query [YOUR QUERY HERE]
      `,
  }),
})
  .then((res) => res.json())
  .then((result) => {
    
    // do stuff here
    console.log(result)
  
  }) 
```

GraphQL Request Example:
```{js}
  fetch('https://api.thegraph.com/subgraphs/name/poap-xyz/poap-xdai', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    query: `
        query {
  accounts(where: {id: "0x8115afd8dffce5579381ad27524b6feeae917bef"}) {
    id
    tokens {
      id
    }
    tokensOwned
  }
}
      `,
  }),
})
  .then((res) => res.json())
  .then((result) => {
    
    // do stuff here
    console.log(result)
  
  }) 
```

Refresh result for user visiting the parcel:
```js
feature.on('click',e=>{
  console.log(e.player)
  
    fetch('https://api.thegraph.com/subgraphs/name/poap-xyz/poap-xdai', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    query: `
        query {
  accounts(where: {id: "`+e.player.wallet +`"}) {
    id
    tokens {
      id
    }
    tokensOwned
  }
}
      `,
  }),
})
  .then((res) => res.json())
  .then((result) => {
    
    // do stuff here
    console.log(result)
  
  }) 
  
})
```



#### API data example from POAP


Example API request:
```js
    fetch('[API ENDPOINT LINK HERE]').then(function (response) {
	return response.json();
}).then(function (data) {
	// This is the JSON from our response
	console.log(data);
})
```


#### Final Script in Video

```js
let element = parcel.getFeatureById('poap_image')


parcel.on('playerenter',e=>{
    fetch('https://api.thegraph.com/subgraphs/name/poap-xyz/poap-xdai', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    query: `
        query {
  accounts(where:{id:"`+e.player.wallet+`"}) {
    id
    tokens {
      id
    }
    tokensOwned
  }
}
      `,
  }),
})
  .then((res) => res.json())
  .then((result) => {
    
    // do stuff here
    console.log(result)
  
    console.log(result.data.accounts[0].tokens[0].id)
    
        fetch('https://api.poap.xyz/token/'+result.data.accounts[0].tokens[0].id).then(function (response) {
	return response.json();
}).then(function (data) {
	// This is the JSON from our response
	console.log(data.event.image_url);
      
      element.set({url: data.event.image_url})    
              
})

          
        
  }) 

})
```


