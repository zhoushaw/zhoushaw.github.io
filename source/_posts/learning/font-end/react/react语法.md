---
title: react语法
date: 2018-07-9 7:52:35
tags: react
categories: js
---


<div><!-- more--></div>

##  起步


>  依赖

```
    <script src="react.js"></script>
    <script src="react-dom.js"></script>
    <script src="babel.min.js"></script>
    
    <body>
        <div id="example"></div>
    </body>
```

> 初始化

```
    <script type="text/babel">
        ReactDOM.render(
          <span>Hello World!</span>,
          document.getElementById('example')
        );
    </script>
```

## 组件化

> 组件注入

```
    <script type="text/babel">
    class MyTitle extends React.Component {
      render() {
        return <h1>Hello World</h1>;
      }
    };

    ReactDOM.render(
      <MyTitle/>,
      document.getElementById('example')
    );
    </script>
```

> 组件传参


```
<script type="text/babel">
      class MyTitle extends React.Component {
        render() {
          return <h1 style={{color: this.props.color}}>Hello World</h1>;
        }
      };
    
      ReactDOM.render(
        <MyTitle color="red" />,
        document.getElementById('example')
      );
</script>
```


定义接口规范:

```

class Counter extends Component {

}

Counter.propTypes = {
  caption: PropTypes.string.isRequired,
  initValue: PropTypes.number
};

Counter.defaultProps = {
  initValue: 0
};

```

> 事件绑定

```
 <script type="text/babel">
  class MyTitle extends React.Component {
    constructor(...args) {
      super(...args);
      this.state = {
        name: '访问者'
      };
    }

    handleChange(e) {
      let name = e.target.value;
      this.setState({
        name: name
      });
    }

    render() {
      return <div>
        <input type="text" onChange={this.handleChange.bind(this)} />
        <p>你好，{this.state.name}</p>
      </div>;
    }
  };

  ReactDOM.render(
    <MyTitle/>,
    document.getElementById('example')
  );
    </script>
```
类中的每个成员在执行时的this并不是和类实例自动绑定的，而在构造函数中，this就是当前组件实例，往往在构造函数中将这个实例的特定函数绑定他this为当前实例

另一种bind函数的方式，类似下面的语句: this.foo = ::this.foo;
等同于下面的语句:
this.foo = this.foo.bind(this);


> 异步渲染

引入了jquery，state值变化时会触发render函数，

```
head:
<script src="jquery.js"></script>

body:
<script type="text/babel">
        class MyList extends React.Component {
            constructor(...args) {
                super(...args);
                this.state = {
                    loading: true,
                    error: null,
                    data: null
                };
            }

            componentDidMount() {
                const url = 'https://api.github.com/search/repositories?q=javascript&sort=stars';
                $.getJSON(url)
                    .done(
                        (value) => this.setState({
                            loading: false,
                            data: value
                        })
                    ).fail(
                    (jqXHR, textStatus) => this.setState({
                        loading: false,
                        error: jqXHR.status
                    })
                );
            }

            render() {
                if (this.state.loading) {
                    return <span>Loading...</span>;
                } else if (this.state.error !== null) {
                    return <span>Error: {this.state.error}</span>;
                } else {
                    /* 你的代码填入这里 */
                    return (
                        <div>
                            <p>API 数据获取成功</p>
                            <p>改写代码，将结果显示在这里</p>
                        </div>
                    );
                }
            }
        };

        ReactDOM.render(
            <MyList/>,
            document.getElementById('example')
        );
    </script>
```

> 列表渲染

```
<script type="text/babel">
        class MyList extends React.Component {
            constructor(...args) {
                super(...args);
                this.state = {
                    items: [
                    {id:0},
                    {id:1},
                    {id:2}
                    ]
                };
            }
            
            render() {
                    const listItems = this.state.items.map((value,index) =>{
                            return <li key={index}>{value.id}</li>
                        }
                    );
                    return (
                        <div>
                            <p>
                                {listItems}
                            </p>
                        </div>
                    );
                }
            }
        };

        ReactDOM.render(
            <MyList/>,
            document.getElementById('example')
        );
    </script>
```

> 组件样式

```
render() {
    const counterStyle = {
      margin: '16px'
    }
    return (
      <div style={counterStyle}>
        <button onClick={this.onClickButton}>Click Me</button>
        <div>
          Click Count: <span id="clickCount">{this.state.count}</span>
        </div>
      </div>
    );
  }
```

## 生命周期

> 三个过程

react严格定义了组件的**生命周期**

* 装载过程( Mount)，也就是把组件第一次在 DOM 树中渲染的过程;
* 更新过程( Update)，当组件被重新渲染的过程;
* 卸载过程( Unmount)，组件从 DOM 中删除的过程 。

三种不同的过程， React库会依次调用组件的一些成员函数，这些函数称为生命周期
函数 。 所以，要定制一个 React 组件，实际上就是定制这些生命周期函数 。


> 装载过程

依次调用:

* constructor
* getlnitialState
* getDefaultProps
* componentWillMount
* render
* componentDidMount

createReactClass初始化

```
var Sample = createReactClass({
    // 初始值
    getInitialState: function() {
        return {count: this.props.initialCount};
      },
    // 默认传参
      getDefaultProps: function() {
        return {
          sampleProp: 0
        };
      }
});
```

ES6初始化传参和初始值
```
// 初始值
class Sample extends React.Component { 
    constructor(props) {
        super(props);
        this.state = {foo: ’ bar ’};
    } 
}
// 传参
Sample.defaultProps = {
    return { sampleProp: 0}
}
```
componentDidMount 只能在浏览器端被调用，在服务器端使用 React 的时候不会被调用 


> 生命周期函数

* componentWillMount 在渲染前调用,在客户端也在服务端。
* componentDidMount : 在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()来进行访问。 如果你想和其他JavaScript框架一起使用，可以在这个方法中调用setTimeout, setInterval或者发送AJAX请求等操作(防止异部操作阻塞UI)。
* componentWillReceiveProps 在组件接收到一个新的 prop (更新后)时被调用。这个方法在初始化render时不会被调用。
* shouldComponentUpdate 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。 
* 可以在你确认不需要更新组件时使用。
* componentWillUpdate在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。
* componentDidUpdate 在组件完成更新后立即调用。在初始化时不会被调用。
* componentWillUnmount在组件从 DOM 中移除的时候立刻被调用。

## 引用第三方组件

rechart为例


```
<head>
    <meta charset="utf-8">
    <script src="react-with-addons.min.js"></script>
    <script src="react-dom.js"></script>
    <script src="react-dom-server.min.js"></script>
    <script src="Recharts.min.js"></script>
    <script src="babel.min.js"></script>
  </head>
  <body>
    <div id="example" style="width: 1000px;height: 800px;"></div>
    <script type="text/babel">
      const {LineChart, Line, XAxis, YAxis, CartesianGrid} = Recharts;
      const data = [
            {name: 'Page A', uv: 4000, pv: 2400, amt: 2400},
            {name: 'Page B', uv: 3000, pv: 1398, amt: 2210},
            {name: 'Page C', uv: 2000, pv: 9800, amt: 2290},
            {name: 'Page D', uv: 2780, pv: 3908, amt: 2000},
            {name: 'Page E', uv: 1890, pv: 4800, amt: 2181},
            {name: 'Page F', uv: 2390, pv: 3800, amt: 2500},
            {name: 'Page G', uv: 3490, pv: 4300, amt: 2100},
      ];

      const TinyLineChart = React.createClass({
          render () {
          return (
        <LineChart width={1000} height={400} data={data}>
          <XAxis dataKey="name"/>
          <YAxis/>
          <CartesianGrid stroke="#eee" strokeDasharray="5 5"/>
          <Line type="monotone" dataKey="uv" stroke="#8884d8" />
          <Line type="monotone" dataKey="pv" stroke="#82ca9d" />
        </LineChart>
          );
        }
      })

      ReactDOM.render(
        <TinyLineChart />,
        document.getElementById('example')
      );
    </script>
  </body>
```

## prop 和 state 的对比

* prop 用于定义外部接口， state 用于记录内部状态;
* prop 的赋值在外部世界使用组件时， state 的赋值在组件内部; 
* 组件不应该改变 prop 的值，而 state存在的目的就是让组件来改变的 。

组件的 state，就相当于组件的记忆，其存在意义就是被修改，每一次通过 this. setState 函数修改 state 就改变了组件的状态，然后通过渲染过程把这种变化体现出来 。

## setState改变复杂对象赋值


```
let targetTopic = this.state.dynamicList[0].topic
this.setState(Object.assign(
  targetTopic,
  {
      topicLikeCounts: dotCounts
  }
))
```



