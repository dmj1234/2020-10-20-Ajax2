####  什么是Ajax
- Ajax:即javascript和XML。Ajax是一种用于创建快速动态网页的技术。通过在后台与服务器进行少量的数据交换，Ajax可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下。对网页的某个部分进行更新。而传统的网页不使用Ajax的话，如果需要更新内容，必须加载整个网页面。


#### Ajax的工作原理
- 客户端发送请求，请求交给ajax的xhr，xhr把请求提交给服务，服务器进行业务处理，服务器响应数据交给xhr对象，**xhr对象**接受数据，由javascript把数据写到页面上。
- **我在这里理解为：xhr是实现了局部刷新的产物。**


#### 同步和异步的区别
  ”同步“就好比：你去外地上学(人生地不熟)，突然生活费不够了；此时你决定打电话回家，通知家里转生活费过来，可是当你拨出电话时，对方一直处于待接听状态(即：打不通，联系不上)，为了拿到生活费，你就不停的oncall、等待，最终可能不能及时要到生活费，导致你今天要做的事都没有完成，而白白花掉了时间。
  “异步”就是：在你打完电话发现没人接听时，猜想：对方可能在忙，暂时无法接听电话，所以你发了一条短信(或者语音留言，亦或是其他的方式)通知对方后便忙其他要紧的事了；这时你就不需要持续不断的拨打电话，还可以做其他事情；待一定时间后，对方看到你的留言便回复响应你，当然对方可能转钱也可能不转钱。但是整个一天下来，你还做了很多事情。 或者说你找室友临时借了一笔钱，又开始
happy的上学时光了。
- 同步交互：指发送一个请求,需要等待返回,然后才能够发送下一个请求，有个等待过程；
- 异步交互：指发送一个请求,不需要等待返回,随时可以再发送下一个请求，即不需要等待。 区别：一个需要等待，一个不需要等待，在部分情况下，我们的项目开发中都会优先选择不需要等待的异步交互方式。

- 如果一个函数的返回值处于
  setTimeout
  AJAX（即XMLHttpRequest）
  AddEventListener（监听事件）    
  那么就是异步

#### 实现Ajax的基本步骤
- 要实现一个AJAX异步调用和局部刷新，需要以下几个步骤:
- 创建XMLHttpRequest对象，即创建一个异步调用对象
- 设置回调函数
- 使用open方法与服务器建立连接
- 向服务器发送数据
- 在回调函数中针对不同的响应状态进行处理

#### onreadystatechange事件
- 当请求被发送到服务器时，我们需要执行 一些基于响应的任务。每当readyState改变时，就会触发onreadystatechange事件。
- readyState属性存有XMLHttpRequest的状态信息。

XMLHttpRequest对象的三个重要属性：
- **onreadystatechange**            存储函数（或函数名）每当readyState属性改变时，就会调用该函数。
- **readyState**       存有XMLHttpRequest的状态。从0到4发生变化。
   0：请求未初始化
   1：服务器连接以建立
   2：请求已接收
   3：请求处理中
   4：请求已完成，且响应已就绪
- **status**      
  200："OK"
  400：未找到网页                          
```js
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
```

#### 在回调函数中针对不同的响应状态进行处理
```js
function callback() {
  // 判断异步对象的状态
  if(xhr.readyState == 4) {
    // 判断交互是否成功
    if(xhr.status == 200) {
      // 获取服务器响应的数据
      var res = xhr.responseText
      // 解析数据
      res = JSON.parse(res)
    }
  } 
}
```
- 回调面试题
```js
const array = ['1','2','3'].map(parseInt)
console.log(array)
结果：[1,NaN,NaN]

原本写法：
const array = ['1','2','3'].map((item,i,arr)=>{
  return parseInt(item)
})

console.log(array)
结果：[1,2,3]
// 简略写法时，传参和调参要一样，map传三个参数，
// 简化写法相当于return parseInt(item,i,arr)
// parseInt只接受两个参数(1,0,arr)=>
// parseInt(1,0,arr) => 1
// parseInt(2,1,arr) => NaN//把2作为1进制的数进行解析，而1进制只有0所以NaN
// parseInt(3,2,arr) => NaN

正确写法：
const array = ['1','2','3'].map((item)=>parseInt(item))

console.log(array)
```

#### 何为Promise
- Promise是一个构造函数，它有resolve、reject、race等静态方法，它的原型prototype上有then、catch。因此只要作为Promise的实例，都可以共享调用Promise.prototype的方法（then、catch）
- 语法：  return new Promise((resolve,reject) => {} )