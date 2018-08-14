# ReactNative Styleguide

Wether you use plain `javascript` or `typescript` following guide is equally applicable except specified otherwise.

## Table of content

### Naming Convention and Structure

Use following naming convention and structure

- Files related to main feature/module should all be within a folder. Name the folder the same as feature. ex: `Auth` folder for any files related with authentication
- Includes a suffix on file name for API, Redux/MobX, Screen
- Function for API should follow REST naming, prefix it with REST method. Ex: getOrders, postComment, deleteItem
- Function on API files should minimise any data transformation, let Redux/Mobx handle it.
- Function that call API, should have use `fetch` prefix
- Function that load data from local storage or database should use `load` prefix
- Prefer to use PureComponent instead of functional stateless component

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
