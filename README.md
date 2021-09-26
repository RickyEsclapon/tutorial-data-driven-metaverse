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
