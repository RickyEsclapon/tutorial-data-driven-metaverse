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


### GraphQL query:
```graphql
{
  delegators(where:{id:"0x994d6ea5a9ccb836d1354947d4697ed3157e48fd"}){
    id
    currentDelegation
  }
}
```


### Pull data in Cryptovoxels from The Graph:
```js
let text_sign = parcel.getFeatureById('welcome')
let delegation = parcel.getFeatureById('delegation')

parcel.on('playerenter',e=>{
  
  console.log(e.player.name)
  
  text_sign.set({text: 'welcome ' + e.player.name + ' !'})
  
  fetch('https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-analytics', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    query: `
        query {
  delegators(where:{id:"0x994d6ea5a9ccb836d1354947d4697ed3157e48fd"}){
    id
    currentDelegation
		totalUnrealizedRewards
  }
}
      `,
  }),
})
  .then((res) => res.json())
  .then((result) => {
    
    
    // do stuff here
    
    console.log(result)  
    
    console.log(result.data.delegators[0].currentDelegation/10^18)    
    
        
    delegation.set({text: result.data.delegators[0].currentDelegation/10^18})    
  
  }) 
  
})
```



... finish adding in code!


