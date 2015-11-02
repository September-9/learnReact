<h1>React的知识点整理</h1>
<h3>一、React是什么？</h3>
React是Facebook开源的用于构建用户界面的javascript库。
<h3>二、React的特点即它与其他js库相比好在哪里？</h3>
1、专注MVC架构中的V（view），使React很容易和开发者已有的开发栈进行融合<br>
2、组件化，React顺应了web开发组件化趋势，从UI抽象出不同的组件，方便多次使用<br>
3、提高造作性能，React抛弃html而应用JSX语法，因为DOM操作非常慢，所以引入虚拟DOM的概念














<h3>三、React精髓</h3>
在虚拟DOM上创建元素，然后将它们渲染到真实DOM上。
<h3>四、创建React对象</h3>
<h4>1、createElement(type,[props],[children..])</h4>
  <p>type指要创建的元素类型，可以是标准的HTML标签名称或一个React组件名称。
  props,可选，用来指定元素的附加属性，比如样式、css类等等。
  children，参数，被认为是这个元素的子参数。</p>
<h4>2、createClass创建一个component</h4>



























<h3>四、components</h3>
 <p>React app通常由用户定义的component组合而成，通常结果是一个主要是很多div组成的树</p>











































<h3>五、React动态交互</h3>

组件其实是状态机（State Machines）React 把用户界面当作简单状态机。把用户界面想像成拥有不同状态然后渲染这些状态，可以轻松让用户界面和数据保持一致。<br>


React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。React 来决定如何最高效地更新 DOM。<br>


常用的通知 React 数据变化的方法是调用 setState(data, callback)。这个方法会合并（merge） data 到this.state，并重新渲染组件。渲染完成后，调用可选的 callback 回调。大部分情况下不需要提供 callback，因为 React 会负责把界面更新到最新状态。





















<h3>六、动态子集</h3>
 <p>如果子级要在多个渲染阶段保持自己的特征和状态，在这种情况下，你可以通过给子级设置惟一标识的 key 来区分。</p>
 <p>当 React 校正带有 key 的子级时，它会确保它们被重新排序（而不是破坏）或者删除（而不是重用）。 务必 把 key添加到子级数组里组件本身上，而不是每个子级内部最外层 HTML 上：</p>
如果 result.id 看起来是一个数字（比如短哈希），那么 // 对象字面量的顺序就得不到保证。这种情况下，需要添加前缀 // 来确保 key 是字符串。
<h3>七、关于render（）方法</h3>
render() 函数应该是纯粹的，也就是说该函数不修改组件 state，每次调用都返回相同的结果，不读写 DOM 信息，也不和浏览器交互（例如通过使用 setTimeout）。
<h3>八、表单组件</h3>
交互属性：
value，用于`<input>` `<textarea>`组件<br>
checked，用于`<checkbox>` `<radio>`<br>
selected,用于`<option>`组件<br>
表单组件可以通过 onChange 回调函数来监听组件变化。当用户做出以下交互时，onChange 执行并通过浏览器做出响应：

	* <input> 或 <textarea> 的 value 发生变化时。
	* <input> 的 checked 状态改变时。
	* <option> 的 selected 状态改变时。

类型为 radio、checkbox 的`<input>` 支持 defaultChecked 属性， `<select>` 支持 defaultValue 属性。

<h3>九、生命周期方法</h3>
很多方法在组件生命周期中的某个确定的时间点执行<br>
<h4>挂载：</h4>
<h5>1)、componentWillMount()</h5>
 <p>服务器端和客户端都只调用一次，在初始化渲染执行之前立刻调用。如果在这个方法内调用setState，render()将会感知到更新后的state，将会执行近义词，尽管state改变了。</p>
<h5>2）、componentDidMount()</h5>
 <p>在初始化渲染执行之后立刻调用一次，仅客户端有效（服务器端不会调用）。在生命周期中的这个时间点，组件拥有一个 DOM 展现，你可以通过 this.getDOMNode() 来获取相应 DOM 节点。</p>
 <>p如果想和其它 JavaScript 框架集成，使用 setTimeout 或者 setInterval 来设置定时器，或者发送 AJAX 请求，可以在该方法中执行这些操作。</p>
<h4>更新：</h4>
<h5>1)、componentWillReceiveProps(object nextProps)</h5>
 在组件接收到新的 props 的时候调用。在初始化渲染的时候，该方法不会调用。<br>
用此函数可以作为 react 在 prop 传入之后， render() 渲染之前更新 state 的机会。老的 props 可以通过this.props 获取到。在该函数中调用 this.setState() 将不会引起第二次渲染。<br>
<h5>2)、shouldComponentUpdate(object nextProps,object nextState)</h5>
在接收到新的 props 或者 state，将要渲染之前调用。该方法在初始化渲染的时候不会调用，在使用 forceUpdate 方法的时候也不会。
如果确定新的 props 和 state 不会导致组件更新，则此处应该 返回 false。
<h5>3)、componentWillUpdate(object prevProps,object prevState)</h5>
 在组件的更新已经同步到 DOM 中之后立刻被调用。该方法不会在初始化渲染的时候调用。<br>
使用该方法可以在组件更新之后操作 DOM 元素。
<h4>移除</h4>
<h5>1）、componentWillUnmount（）</h5>
在组件从 DOM 中移除的时候立刻被调用。<br><br>
在该方法中执行任何必要的清理，比如无效的定时器，或者清除在 componentDidMount 中创建的 DOM 元素。
<h3>十、JSX中的 if-else</h3>
 jsx中不可以用if-else来写判断，应该用三目运算符
 不过当三目运算符不够强健时，可以使用 if 来判断应该渲染哪个组件.<br>
   例如：
>			 var loginButton;
>			 if(LogedIn){
>			     loginButton=<LogoutButton />;
>			 }else{
>			      loginButton = <LoginButton />;
>			 }
>			 return (
>			   <nav><Home /> {loginButton} </nav>);
<h3>十一、自闭合标签</h3>

在 JSX 中， <MyComponent /> 是合法的，而 <MyComponent> 就不合法。 所有的标签都必须闭合，可以是自闭和的形式，也可以是常规的闭合。
注意：
所有 React component 都可以采用自闭和的形式：<div />. <div></div> 它们是等价的。
<h3>十二、与其他类库并行使用 React</h3>
你不用非得全部采用 React。组件的生命周期事件，特别是componentDidMount 和 componentDidUpdate，非常适合放置其他类库的逻辑代码。

<h3>十三、基于ES6的React</h3>
	class TodoApp extends React.Component {
	    constructor(props){
	        super(props); // 需要在第一行
	       
	        this.state = {};
	
	        // unwork，官网说不支持
	        //this.mixins = [xxx];
	    }
	
	    render() {
	        return (
	            <div>
	                <button type="button" onClick={this.handleAdd.bind(this)}>add</button>
	                <div>
	                    {this.props.todos}
	                </div>
	            </div>
	        );
	    }
	
	    handleAdd() {
	        // something
	    }
	}
	
	TodoApp.propTypes = {
	    todos: React.PropTypes.array.isRequire
	};
	//TodoApp.defaultProps = { xxx };
<h3>十四、React中需要注意的地方</h3>
<h4>1）行内样式</h4>
 在React中，行内样式不再是个简单的字符串。它是一个{ }对象，对象里的key是样式名称的驼峰命名显示，而value则是你想要的样式值（通常是字符串）。<br>
例：
>      var divStyle={
 >        color : 'white' ,
 >        backgroundImage : ' url ( ' + imgUrl + ' ) '
 >     }
 >      React.render(<div style={divStyle}>Hello World!</          
 >      div>,mountNode);
 
如果不单独写样式，也可以采用{{ }} 来表示：
如：					
>	     React.render(<div style={{color:'red'}}>Hello World!</
>	     div>,mountNode);

样式名称采用驼峰命名法。（除了特点的前缀，其它都应该以大写开头）


