# ReactNative Styleguide

Wether you use plain `javascript` or `typescript` following guide is equally applicable except specified otherwise.

## Table of content

### null / undefined

#### Don't

**Don't** pass **null / undefined** into function parameter

```js
function one(){
    let params;
    callParams(params)
}
...

const callParams = (params) => {
    // do something here
}
```

#### Do

**Do** give default value to function parameters or check for **null / undefined**

```js
function one(){
    let params;
    callParams(params)
    // OR check for value
    if (params){
        callParams(params)
    }
}

...

const callParams = (params = {}) => { // add default value as well
    // do something here
}
```

### Lambda

#### Don't

**Don't** declare _lambda_ within **JSX**.

This affect performance in terms of rendering

```js
render(){
    return {
        <TouchableOpacity onPress={()=>this.callFunction()} > // don't do this
        ...
        </TouchableOpacity>
    }
}
```

#### Do

**Do** separate the call from _user action_ such as **onPress** into it's own function

```js
buttonPressed = () => {
    this.callFunction()
}

render(){
    return {
        <TouchableOpacity onPress={this.buttonPressed}>
        ...
        </TouchableOpacity>
    }
}
```

```js
buttonPressed = () => {
    const { params } = this.props
    if (params){
        this.callFunctionWithParameters(params)
    }
}

render(){
    return {
        <TouchableOpacity onPress={this.buttonPressed}>
        ...
        </TouchableOpacity>
    }
}
```
