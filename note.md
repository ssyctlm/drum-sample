# 1 how Array.map method works on complex Obj (2020-02-04)
  ```javascript
    this.props.power?
    padBank = this.props.currentPadBank.map((drumObj,i,padBankArr)=>{
      return (
        <DrumKeys
        clipId = {drumObj.id}
        clip =  {drumObj.url}
        keyTrigger={drumObj.keyTrigger}
				keyCode={drumObj.keyCode} 
        updateDisplay = {this.props.updateDisplay}
        power = {this.props.power} />
      )
    }):
    padBank = this.props.currentPadBank.map((drumObj,i,padBankArr)=>{
      return (
        <DrumKeys
        clipId = {padBankArr[i].id}
        clip = "#"
        keyTrigger = {padBankArr[i].keyTrigger}
        keyCode = {padBankArr[i].keyCode}
        updateDisplay = { this.props.updateDisplay}
        power= {this.props.power} />
      )
    });
```




Turns out, this method has nothing to do with Object, **`map` method is an Array method**!
3 parameters of Array.map method are `EachArrayElement`, `indexOfEachElement`,`TheArrayItSelf`. And as above snippet of code show, two different way to quote the item will have a identical outcome



# 2. `Array.prototype.slice.call(argument)` 

## Explain call : `Function.prototype.call()`

 sample sinppet:
 ``` javaScript

    function Product(name,price){
      this.name = name;
      this.price = price;
    }

    function Food(name,price){
      Product.call(this,name,price);
      this.category = 'food'
    }

    console.log(new Food('cheese',5).name)

 ```
 The `call()` method calls a function with a given `this` value and arguments provided individually.
 The syntax is `function.call(obj[this.item],argument)`.

## Explain `[].slice.call()`
 `Array.prototype.slice()` method also is a function which allows it to use `call()` method.
 ``` javascript
    // below wuold return True
    [].slice === Array.prototype.slice

 ```
 It means in the snippet `Array.prototype.slice.call(argument,0)`, `argument` is seen as current Object which has a slice method too, So , actually above snippet exercute like as follow:
 ```javascript
  var argument = [...argus]
  var [] = argument.slice(0)

 ```

----------------
- **Reference**
  - [Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
  - [你遇到过[ ].slice.call()吗？](https://www.jianshu.com/p/ae57baecc57d)