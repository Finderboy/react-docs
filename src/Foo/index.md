# React

### 简介

- 用于构建 Web 和原生交互界面的库
- React 用组件创建用户界面
- 通俗来讲：是一个将数据渲染为HTML视图的开源JS库

### 为什么使用React?

- 原生JS使用DOM-API修改UI代码很繁琐，效率低下，React可以解决这种问题
- 原生JS直接操作DOM，浏览器会大量重绘重排，React可以解决这种问题
- 原生JS没有组件化方案好用，代码复用率很低，
- React 采用组件化模式，React 让你可以通过组件来构建用户界面
- React 使用声明式编码
- React 使用虚拟DOM，将数据映射成虚拟DOM,再生成真实DOM,当数据变化的时候，会对原有的虚拟DOM和新的虚拟DOM进行比较,再生成真实DOM。
- React 使用DOM diffing 算法，最小化页面重绘

### 特点

声明式设计 −为你应用的每一个状态设计简洁的视图，当数据改变时 React 能有效地更新并正确地渲染组件。

- 高效 −React采用Virtual DOM(虚拟DOM), 极大的提升了UI渲染(更新)效率。

- 灵活 −React 允许你结合其他框架或库一起使用。

- JSX − JSX 是 JavaScript 语法的扩展。JSX 可以很好地描述 UI 应该呈现出它应有交互的本质形式。

- 组件 − 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。

- 单向响应的数据流 − React 采用了单向响应的数据流，使组件状态更容易维护, 组件模块化更易于快速开发。

  

### 文档、工具

- [中文文档](https://react.docschina.org/)
- [英文文档]( https://react.dev/learn)
- [HTML 转 JSX 工具](https://transform.tools/html-to-jsx)

## 快速入门

![image-20240604091939784](/Users/gxn/Library/Application Support/typora-user-images/image-20240604091939784.png)

## 1、JSX简介（★★★）

#### 1.1、**JSX简介**

- 1、全称：JavaScript XML
- 2、react定义的一种类似于XML的JS扩展语法：JS + XML本质是React.createElement(component, props, ...children)方法的语法糖
- 3、作用：用来简化创建虚拟DOM
- 4、写法：

```css
var ele = <h1>Hello JSX!</h1>
```

#### 1.2、**基本语法规则**

- 1、定义虚拟DOM时，不要写引号；
- 2、标签中混入**JS表达式时**要用 `{ }`。
- 3、样式的类名指定不要用 class，要用 `className`。（因为class是ES6中类的关键字，所以不让用）
- 4、内联样式，要用 `style={{ key:value }}` 的形式去写。
- 5、只有一个根标签；
- 6、如果没有子节点的React元素可以用 `/>` 来结束
- 7、React元素的属性名使用驼峰命名法

#### 1.3、嵌入JS表达式

###### 语法：{JavaScritp表达式}

```css
/*let content = '插入的内容'*/
/*let h1 = <h1>我是通过JSX创建的元素+ {content}</h1>*/
```

###### 注意点

- 只要是合法的js表达式都可以进行嵌入
- JSX自身也是js表达式
- 注意：js中的对象是一个例外，一般只会出现在style属性中
- 注意：在{}中不能出现语句

#### 1.4、条件渲染

###### 根据不同的条件来渲染不同的JSX结构

```jsx
import React from 'react';
let isLoading = true
function loading(isLoading) {
  if(isLoading){
    return <div>Loading...</div>
  }
  return <div>加载完成</div>
}
export default loading;
```

可以发现，写JSX的条件渲染与我们之前编写代码的逻辑是差不多的，根据不同的判断逻辑，返回不同的 JSX结构，然后渲染到页面中

```css
/*var ele = <h1>Hello JSX!</h1>*/
```

#### 1.5、列表渲染

- 如果需要渲染一组数据，我们应该使用数组的 map () 方法
- 注意：渲染列表的时候需要添加key属性，key属性的值要保证唯一
- 原则：map()遍历谁，就给谁添加key属性
- 注意：尽量避免使用索引号作为key

```jsx
import React from 'react';
let arr = [
  { id: 1, name: '三国演义' },
  { id: 2, name: '水浒传' },
  { id: 3, name: '西游记' },
  { id: 4, name: '红楼梦' }
];
function ShowUrl() {
  return (
    <ul>
      {arr.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  )
}
export default ShowUrl;
// ReactDOM.render(ul, document.getElementById('root'));
```

#### 1.5、样式处理

###### 行内样式 -style

在style里面我们通过对象的方式传递数据

```css
/*<li key={item.id} style={{'color': 'red',"backgroundColor": 'pink'}}>{item.name}</li>*/
```

###### 类名 -className

```css

/*<li className='container' key={item.id} style={{'color': 'red',"backgroundColor": 'pink'}}>{item.name}</li>*/
/*import './css/index.css'*/
/*.container {*/
/*    text-align: center*/
/*}*/
```

小结

- JSX是React的核心内容
- JSX表示在JS代码中写HTML结构，是React声明式的体现
- 使用JSX配合嵌入的JS表达式、条件渲染、列表渲染、可以描述任意UI结构
- 推荐使用className的方式给JSX添加样式
- React完全利用JS语言自身的能力来编写UI，而不是造轮子增强HTML功能



## ﻿﻿2、元素渲染（★★★）

#### 2.1、 基本概念

* React 元素与 DOM 元素不同。React 元素是不可变对象，一旦创建就不能更改其内容或属性。更新界面的唯一方法是创建一个新的元素，并将其传递给 ReactDOM.render() 方法。

#### 2.2、渲染元素

假设我们有一个简单的 `div` 容器：

```html
<div id="root"></div>
```

我们可以使用 React 渲染一个元素到这个容器中：

```javascript
import React from 'react';
const element = <h1>Hello, world!</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

#### 2.3、 更新渲染
* React 元素是不可变的。要更新显示的内容，我们需要创建新的元素并再次调用 ReactDOM.render()。例如：
```javascript
// function tick() {
//   const element = (
//     <div>
//       <h1>Hello, world!</h1>
//       <h2>It is {new Date().toLocaleTimeString()}.</h2>
//     </div>
//   );
//   ReactDOM.render(element, document.getElementById('root'));
// }
//
// setInterval(tick, 1000);
```

上面的代码每秒钟都会创建一个新的 React 元素并将其渲染到 DOM 中。

#### 2.4、元素的更新

###### React 只更新实际需要更新的部分。通过比较新旧元素的不同，React 能够高效地更新 DOM。

```javascript
// const element = <h1>Goodbye, world!</h1>;
// ReactDOM.render(element, document.getElementById('root'));
//
// 如果我们将上面的元素更新为:
//
// const element = <h1>Hello, world!</h1>;
// ReactDOM.render(element, document.getElementById('root'));
```

> [!IMPORTANT]
>
> React 只会更新文本内容，而不是重新构建整个 DOM 节点。

## 3、组件&Props（★★★）

###### React 是一个基于组件的库，组件是构建 React 应用程序的基础单元。每个组件都可以看作是一个独立的、可复用的 UI 模块。

#### 3.1、什么是组件

组件可以是类组件或函数组件：

- **类组件** 使用 ES6 类语法创建，包含更多功能和生命周期方法。
- **函数组件** 使用函数语法创建，更加简洁，并且从 React 16.8 版本开始，可以使用 Hooks 使其具备状态和其他特性。

##### 1.1 类组件

```javascript
import React from 'react';

class Welcome extends React.Component {
  constructor(props) {
    super();
  }

  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

export default Welcome;
```

##### 1.2 函数组件

```javascript
import React from 'react';
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
export default Welcome;
```

#### 3.2、 使用组件

###### 组件可以像 HTML 标签一样使用。组件可以通过 props 接收参数，并且 props 是只读的。

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}
export default App;

```

#### 3.3、 Props

###### `props`（属性）是组件的输入参数。它们是从父组件传递给子组件的数据。

##### 3.1 传递 Props

###### Props 可以是任意类型的 JavaScript 值，包括对象、数组和函数。

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
```

##### 3.2 默认 Props

###### 可以使用 `defaultProps` 为组件定义默认的 props 值。

```javascript
class Welcome extends React.Component {
  static defaultProps = {
    name: 'Stranger'
  };

  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

函数组件也可以使用 `defaultProps`：

```javascript 
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

Welcome.defaultProps = {
  name: 'Stranger'
};
```

## ﻿﻿4、State &生命周期（★★★）

在 React 中，状态（state）和生命周期（lifecycle）是组件的重要概念。状态允许组件动态地响应用户输入和数据变化，而生命周期方法则允许开发者在组件的不同阶段执行特定的代码。

#### 4.1、State 简介

###### State 是组件内部管理的数据。与 props 不同，state 是私有的，完全由组件自身控制。

##### 1.1 定义 State

###### 类组件中通过 `this.state` 定义 state，函数组件中通过 `useState` Hook 定义 state。

```javascript
// 类组件
class ClockDemo extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
// 函数组件
function Clock() {
  const [date, setDate] = React.useState(new Date());

  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {date.toLocaleTimeString()}.</h2>
    </div>
  );
}
```

##### 1.2 更新 State

```javascript
// 类组件
class ClockDemo2 extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

// 函数组件
function ClockDemo3() {
  const [date, setDate] = React.useState(new Date());

  React.useEffect(() => {
    const timerID = setInterval(() => setDate(new Date()), 1000);
    return () => clearInterval(timerID);
  }, []);

  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {date.toLocaleTimeString()}.</h2>
    </div>
  );
}

```

#### 4.2、生命周期方法

###### 生命周期方法是类组件特有的，用于在组件的不同阶段执行代码。函数组件则通过 Hooks 实现类似的效果。

##### 2.1 类组件的生命周期方法

1. **挂载（Mounting）**: 当组件实例被创建并插入 DOM 中时调用的生命周期方法。

   - `constructor()`构造函数，最先被执行，用于初始化state等数据 
   - `static getDerivedStateFromProps() `静态方法，会在组件实例化和更新时被调用，用于处理props。
   - `render()`必须的方法，创建虚拟DOM，返回JSX模板
   - `componentDidMount()` 组件挂载后执行，可以进行异步操作，如获取数据等。

2. **更新（Updating）**: 当组件的 props 或 state 发生变化时调用的生命周期方法。

   - `static getDerivedStateFromProps() `：静态方法，在更新props时被调用
   - `shouldComponentUpdate() `返回Boolean值，表示是否需要更新组件，默认返回true。
   - `render()` 必须的方法，创建虚拟DOM，返回JSX模板
   - `componentDidUpdate()` 组件更新后执行，可以进行DOM操作等

3. **卸载（Unmounting）**: 当组件从 DOM 中移除时调用的生命周期方法。

   - `componentWillUnmount()`

4. **错误处理（Error Handling）**: 在其子组件树中的任何位置捕获 JavaScript 错误并打印这些错误。

   - `static getDerivedStateFromError()`
   - `componentDidCatch()`

   

## 5、﻿﻿事件处理（★★★）

###### 事件处理是 React 应用中的重要组成部分，用于响应用户的交互操作。React 的事件处理与传统的 HTML 事件处理有一些不同之处，包括语法和机制。

#### 5.1、 基本事件处理

###### 在 React 中，事件处理器是以 camelCase 命名的属性，而不是小写。并且在 JSX 中，你需要传入一个函数作为事件处理器，而不是一个字符串。

```jsx
import React from 'react';
function ActionLink() {
  const activateLasers = () => {
    // todo
  }
  return (
    <button onClick={activateLasers}>点击</button>
  )
}
export default ActionLink;

```

#### 5.2、 事件对象

###### 在事件处理函数中，React 会自动传递一个合成事件对象（SyntheticEvent），它是 React 包装的原生事件对象。这个合成事件对象可以跨浏览器正常工作。

```javascript
function handleClick(e) {
  e.preventDefault();
  console.log('The link was clicked.');
}

<a href="#" onClick={handleClick}>Click me</a>
```

#### 5.3、 向事件处理器传递参数

###### 在 React 中，你可以通过箭头函数或 bind 方法向事件处理器传递参数。

```javascript
import React from 'react';
class Greeting1 extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: 'World' };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick(name, e) {
    console.log('Hello, ' + name);
  }

  render() {
    // 使用 bind 方法
    return (
      <button onClick={this.handleClick.bind(this, 'React')}>
        Greet React
      </button>
    );
  }
}
// 函数组件中通过箭头函数传递参数
function Greeting2() {
  const [name, setName] = React.useState('World');

  function handleClick(name, e) {
    console.log('Hello, ' + name);
  }

  return (
    <button onClick={(e) => handleClick('React', e)}>
      Greet React
    </button>
  );
}

```



## 6、﻿﻿条件渲染（★★★）

条件渲染是 React 中的重要概念，它允许你根据不同的条件动态地渲染组件或元素。React 的条件渲染与 JavaScript 的条件语句（如 `if` 或三元运算符）相似。以下是一些常用的条件渲染方法。

#### 6.1、 使用 `if` 语句

###### 最直接的方法是使用 `if` 语句来控制渲染的内容。

```javascript

function UserGreeting() {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting() {
  return <h1>Please sign up.</h1>;
}

function Greeting3(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}
```

#### 6.2、使用三元运算符

###### 三元运算符可以在 JSX 内部使用，是一种简洁的条件渲染方法。

```javascript
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? <UserGreeting /> : <GuestGreeting />}
    </div>
  );
}

```

#### 6.3、 使用逻辑与（`&&`）运算符

###### 可以使用逻辑与（`&&`）运算符来执行短路操作，如果条件为真，则渲染某个元素，否则不渲染。

```javascript
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

// 使用组件
const messages = ['React', 'Re: React', 'Re:Re: React'];
```

#### 6.4、使用立即调用函数表达式（IIFE）

###### 立即调用函数表达式（IIFE）可以在 JSX 中执行更复杂的条件逻辑。

```jsx
import React from 'react';
function UserGreeting() {
  return <h1>Welcome back!</h1>;
}
function GuestGreeting() {
  return <h1>Please sign up.</h1>;
}
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  return (
    <div>
      {(() => {
        if (isLoggedIn) {
          return <UserGreeting />;
        } else {
          return <GuestGreeting />;
        }
      })()}
    </div>
  );
}
export default Greeting;

// 使用组件
// ReactDOM.render(
//   <Greeting isLoggedIn={true} />,
//   document.getElementById('root')
// );
```

### 总结

- **`if` 语句**: 最直接的条件渲染方法，适合在渲染逻辑较为复杂时使用。
- **三元运算符**: 在 JSX 内部使用，适合简洁的条件渲染。
- **逻辑与（`&&`）运算符**: 执行短路操作，在条件为真时渲染内容。
- **立即调用函数表达式（IIFE）**: 在 JSX 中执行复杂的条件逻辑。

## 7、﻿列表&Key（★★★）

#### **为什么要给每一个元素添加key属性？**

> 官方描述：key 帮助 React 识别哪些元素改变了，比如被添加或删除。 **解读**

React是在更新DOM的时候，是使用Diffing算法进行比较，只有发生了变化的元素才会更新DOM，如果通过key属性可以让React知道哪个li元素发生了变化。

> [!IMPORTANT]
>
> 一个元素的 key 最好是这个元素在列表中拥有的一个独一无二的字符串。通常，我们使用数据中的 id 来作为元素的 key。
```jsx
import React, { useState } from 'react';
const todos = [{
  id: 1,
  text: '学习React'
},{
  id: 2,
  text: '理解React'
},{
  id: 3,
  text: '使用React'
}]
function todoItems() {
 return (
   todos.map((todo) =>
     <li key={todo.id}>
       {todo.text}
     </li>
   )
 ) 
}
export default todoItems;
```

> [!IMPORTANT]
>
> 当元素没有确定 id 的时候，**万不得已你可以使用元素索引 index 作为 key**

```jsx
import React from 'react';
const todos = [{
  id: 1,
  text: '学习React'
},{
  id: 2,
  text: '理解React'
},{
  id: 3,
  text: '使用React'
}]
function todoItems1() {
  return (
    todos.map((todo, index) =>
      // Only do this if items have no stable IDs
      <li key={index}>
        {todo.text}
      </li>)
  )
}
export default todoItems1;
```

#### **为什么不建议通过索引来作为key属性**？

> 官方描述：如果列表项目的顺序可能会变化，我们不建议使用索引来用作 key 值，因为这样做会导致性能变差，还可能引起组件状态的问题。可以看看 Robin Pokorny 的深度解析使用索引作为 key 的负面影响这一篇文章。如果你选择不指定显式的 key 值，那么 React 将默认使用索引用作为列表项目的 key 值。

使用索引作为key属性，一旦数组元素的顺序发生了变化，就可能带来意想不到的错误，所以React官方不推荐。



## 8、表单（★★★）

####  8.1、简介

React 表单处理是一个重要的概念，涉及到用户输入、表单提交和表单验证。React 的设计理念强调组件化和单向数据流，表单处理也是基于这些原则。React 通过受控组件和非受控组件两种方式来处理表单数据。

#### 8.2、 受控组件

###### 受控组件指的是表单元素的值由 React 组件的 state 管理。每当表单元素发生变化时，都会触发一个事件处理函数来更新 state，这样表单元素的值就始终与 state 同步。

###### 示例：受控组件

```jsx
import React, { useState } from 'react';

function ControlledForm() {
  const [inputValue, setInputValue] = useState('');

  const handleChange = (event) => {
    setInputValue(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert('提交的值是: ' + inputValue);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        输入:
        <input type="text" value={inputValue} onChange={handleChange} />
      </label>
      <button type="submit">提交</button>
    </form>
  );
}

export default ControlledForm;
```

#### 8.3、 非受控组件

###### 非受控组件指的是表单元素的值不受 React 组件的 state 管理，而是通过 `ref` 来直接访问 DOM 元素。这样，表单元素的值是由 DOM 自己管理的。

###### 示例：非受控组件

```jsx
import React, { useRef } from 'react';

function UncontrolledForm() {
  const inputRef = useRef(null);

  const handleSubmit = (event) => {
    event.preventDefault();
    alert('提交的值是: ' + inputRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        输入:
        <input type="text" ref={inputRef} />
      </label>
      <button type="submit">提交</button>
    </form>
  );
}

export default UncontrolledForm;
```

#### 8.4、 表单元素

###### React 支持各种表单元素，包括输入框、文本域、选择框、单选框和复选框等。以下是如何处理不同类型的表单元素的示例。

##### 输入框

```jsx
import React, { useState } from 'react';

function InputExample() {
  const [name, setName] = useState('');

  const handleChange = (event) => {
    setName(event.target.value);
  };

  return (
    <div>
      <label>
        名字:
        <input type="text" value={name} onChange={handleChange} />
      </label>
      <p>输入的名字是: {name}</p>
    </div>
  );
}

export default InputExample;
```

##### 文本域

```jsx
import React, { useState } from 'react';

function TextAreaExample() {
  const [description, setDescription] = useState('');

  const handleChange = (event) => {
    setDescription(event.target.value);
  };

  return (
    <div>
      <label>
        描述:
        <textarea value={description} onChange={handleChange} />
      </label>
      <p>输入的描述是: {description}</p>
    </div>
  );
}

export default TextAreaExample;
```

##### 选择框

```jsx
import React, { useState } from 'react';

function SelectExample() {
  const [fruit, setFruit] = useState('apple');

  const handleChange = (event) => {
    setFruit(event.target.value);
  };

  return (
    <div>
      <label>
        选择水果:
        <select value={fruit} onChange={handleChange}>
          <option value="apple">苹果</option>
          <option value="banana">香蕉</option>
          <option value="cherry">樱桃</option>
        </select>
      </label>
      <p>选择的水果是: {fruit}</p>
    </div>
  );
}

export default SelectExample;
```

##### 单选框

```jsx
import React, { useState } from 'react';

function RadioExample() {
  const [gender, setGender] = useState('male');

  const handleChange = (event) => {
    setGender(event.target.value);
  };

  return (
    <div>
      <label>
        <input type="radio" value="male" checked={gender === 'male'} onChange={handleChange} />
        男
      </label>
      <label>
        <input type="radio" value="female" checked={gender === 'female'} onChange={handleChange} />
        女
      </label>
      <p>选择的性别是: {gender}</p>
    </div>
  );
}

export default RadioExample;
```

##### 复选框

```jsx
import React, { useState } from 'react';

function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChange = (event) => {
    setIsChecked(event.target.checked);
  };

  return (
    <div>
      <label>
        <input type="checkbox" checked={isChecked} onChange={handleChange} />
        同意条款
      </label>
      <p>是否同意: {isChecked ? '是' : '否'}</p>
    </div>
  );
}

export default CheckboxExample;
```

#### 8.5、 表单验证

###### 表单验证是表单处理中的一个重要环节。React 可以通过在事件处理函数中添加逻辑来实现表单验证。

##### 示例：表单验证

```jsx
import React, { useState } from 'react';

function ValidationForm() {
  const [email, setEmail] = useState('');
  const [error, setError] = useState('');

  const handleChange = (event) => {
    setEmail(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    if (!/\S+@\S+\.\S+/.test(email)) {
      setError('请输入有效的邮箱地址');
    } else {
      setError('');
      alert('提交的邮箱是: ' + email);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        邮箱:
        <input type="email" value={email} onChange={handleChange} />
      </label>
      {error && <p style={{ color: 'red' }}>{error}</p>}
      <button type="submit">提交</button>
    </form>
  );
}

export default ValidationForm;
```

#### 8.6、 总结

React 提供了灵活的表单处理方式，通过受控组件和非受控组件两种方式管理表单数据。受控组件使得表单元素的值与组件的 state 同步，而非受控组件则直接操作 DOM 元素。React 支持各种表单元素，并且可以方便地实现条件渲染和表单验证



#### 今天就学到到这里啦~

- 小伙伴们，(￣ω￣(￣ω￣〃 (￣ω￣〃)ゝ
  - ​		大家要天天开心哦 
