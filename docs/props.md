---
title: 组件化 & Props
---

组件可以将UI切分成一些的独立的、可复用的部件，这样你就只需专注于构建每一个单独的部件。

组件从概念上看就像是函数，它可以接收任意的输入值（称之为“props”），并返回一个需要在页面上展示的 Taro 元素。

你也可以使用 ES6 class 来定义一个组件:

```javascript
class Welcome extends Component {
  render () {
    return <View>Hello, {this.props.name}</View>
  }
}
```

## 组件渲染

在前面，我们遇到的 Taro 元素都是内置组件：

```javascript
const element = <View />
```

然而，Taro 元素也可以是用户自定义的组件：

```javascript
const element = <Welcome name="Wallace" />
```

当React遇到的元素是用户自定义的组件，它会将JSX属性作为单个对象传递给该组件，这个对象称之为“props”。

例如,这段代码会在页面上渲染出”Hello, Wallace”:

```javascript
// welcome.js
class Welcome extends Component {
  render () {
    return <View>Hello, {this.props.name}</View>
  }
}

// app.js
class App extends Component {
  render () {
    return <Welcome name="Wallace" />
  }
}
```

### Props的只读性

一个声明的组件决不能修改它自己的 `props`。来看这个`sum`函数：

```javascript
function sum (a, b) {
  return a + b
}
```

类似于上面的这种函数称为「纯函数」，它没有改变它自己的输入值，当传入的值相同时，总是会返回相同的结果。

与之相对的是非纯函数，它会改变它自身的输入值：

```javascript
function withdraw (account, amount) {
  account.total -= amount
}
```

Taro 和 React 一样，也有一个严格的规则：

所有的 Taro 组件必须像纯函数那样使用它们的props。

当然，应用的界面是随时间动态变化的，我们将在下一节介绍一种称为`state`的新概念，State可以在不违反上述规则的情况下，根据用户操作、网络响应、或者其他状态变化，使组件动态的响应并改变组件的输出。

### 使用 PropTypes 检查类型

随着应用日渐庞大，你可以通过类型检查捕获大量错误。要检查组件的属性，你需要配置特殊的 `propTypes` 属性：
```javascript
import PropTypes from 'prop-types';

class Greeting extends Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

如上例，Taro与React一样，也支持`PropTypes` 检查类型，*目前在小程序端还有些问题*，但在 H5 端可以使用，用法和在 React 里一样。
更多可参照[React的相关文档](https://reactjs.org.cn/doc/typechecking-with-proptypes.html)。


