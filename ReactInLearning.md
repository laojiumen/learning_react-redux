#React
==========
##first programing(构建一个单页面)运用react,jquery,html等内容。
###Some Notes
* 1. 一个标准react的框架：
<html>
  <head>
    <title>Hello React</title>
    <script src="http://fb.me/react-0.13.0.js"></script>
    <script src="http://fb.me/JSXTransformer-0.13.0.js"></script>
    <script src="http://code.jquery.com/jquery-1.10.0.min.js"></script>
  </head>
  <body>
    <div id="content"></div>
    <script type="text/jsx">
	var CommentBox = React.createClass({
 	 render: function() {
   	     return (
     		 <div className="commentBox">
     		   Hello, world! I am a CommentBox.
     		 </div>
  	 	 );
 	 }
       });
	React.render(
  	  <CommentBox />,
 	   document.getElementById('content')
	);
    </script>
	
  </body>
</html>
render: function 用于创建一个用react描述的元素， 并通过React.render来将创建的元素插入生成的div中
× 2. jsx语法：简单的原理就是在javascript中插入xml内容，例如：
var CommentBox = React.createClass({
	render: function() {
	return (
			<div className="commentBox">
			Hello, world! I am a CommentBox.
			</div>
	       );
	}
});
React.render(
		<CommentBox />,
		document.getElementById('content')
	    );
在其中，return语句中就包含了<div>元素

* 3.使用props，读取父节点传递过来的数据，并渲染自己
* 4.使用getInitialState()组件初始化状态（仅渲染一次），例子：
var CommentBox = React.createClass({
  getInitialState: function() {
    return {data: []};
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm />
      </div>
    );
  }
});
* 5.更新state（例如: 从服务器获取get的方法）,使用componentDidMount()加载数据，当加载成功的时候运用render来更新UI。可以使用轮巡的方式来实时更新，例如:
1.定义一个function, loadCommentsFromServer: function(){$ajax:...}
2.在componentDidMount()时调用,this.loadCommentsFromServer;
  调用setInterval(this.loadCommentsFromServer, this.props.pollInterval)更新状态.
3.在React.render时，定义<CommentBox url="...", pollInterval={2000}>,更新
