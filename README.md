# react-ele
react仿饿了么app    
技术：`react`+`react-router`+`redux`+`create-react-app`+`智能组件`+`木偶组件`    
```markdown
git clone git@github.com:YMBo/react-ele.git    
npm install    
npm start    
```
******************************************************
### 一、准备阶段：    
因为用的是`create-react-app`创建的项目，在项目中用到了less、rem，所以添加在`webpack`中添加这两个功能    
    
#### 1.初始化并添加less、px2rem功能    
[点我查看详情](https://ymbo.github.io/2017/09/06/create-react-app%E9%85%8D%E7%BD%AEwebpack/)    
    
### 二、记录    
#### 1.header
header区域没有什么特别得。用到的布局是flex    
#### 2.banner
banner区域：    
* 轮播图用的是`react-swipe`插件    
* 因为数据是从饿了么取来的，所以需要对整个数组拆分为几个小数组，这就是循环的页数，然后小数组里有一些元素，为每一页的展示项目    
* 比如图片的hash值为'asdfghh'，需要的图片地址需要进行格式上的转变为'a/sd/fghh',不明白为啥饿了么要这么做，直接用不可以么，我实现的方法是字符串转换为数组，进行插入，转换为字符串，详情看`src/components/banner/banner.js`文件，数据格式请看  `src/data/data.js`
* 轮播图下面的控制按钮，我是用操作dom对象来实现的，因为用这几个小按钮是我循环出来的，`this.state` 用不了,希望能找到更好的办法 。     
  （这个今天找到了解决办法，上面说到按钮是循环出来的，是在`componentDidMount`生命周期操作的，然后我将循环后的数组保存在this.state中，然后render的时候就不行了，我把循环的过程放到render中，this.state控制按钮行为的操作是成功的，所以`如果需要循环数据并展现在页面中时，要在render中操作`）
#### 3.首页预览    
![首页预览](https://github.com/YMBo/react-ele/blob/master/preview/1.png)    
其中深红色部分为随机打乱数据并展现，红色部分为模仿请求来的数据进行操作并展现，现在还没有下拉刷新和无限滚动    
#### 4.搜索框采用position：fixed与position：sticky结合的方式，达到顶部吸附功能    
![搜索框吸附](https://github.com/YMBo/react-ele/blob/master/preview/2.gif)    
#### 5.回到顶部    
回到顶部按钮是判断滚动高度来计算的，采用了`函数节流`的模式，提高效率    
#### 6.下拉加载更多功能    
由于数据都是本地的，所以利用`setTimeout`模拟网络请求延迟，如果所示:    
![加载更多](https://github.com/YMBo/react-ele/blob/master/preview/3.gif)    
#### 7.底部导航（路由）    
用的是`react-router 4`，效果：    
![footer](https://github.com/YMBo/react-ele/blob/master/preview/4.gif)    
注意因为首页的路由是`/`，所以匹配任何一个路由都会匹配到它，因此给它加一个精确匹配即可解决``    
``` javascript
<NavLink  to="/" exact activeClassName='active'>
	<svg className='index_footer_icon first' viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" >....</svg>
	<span className='index_footer_word'>外卖</span>
</NavLink >
```    
其中`activeClassName`表示如果在当前路由的话就添加上`active`的class，或者用`activeStyle`是添加style。    
最后`react-router 4`的改动很大，不清楚的地方可以百度、google查找
