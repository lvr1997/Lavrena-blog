---
title: vue表单自动保存（页面缓存）
titleTemplate: Vue
publish: true
date: 2024-01-12
tags:
  - vue
---

> 本篇文章引用自[vue项目表单自动保存（定时缓存）功能 + beforeRouteLeave钩子函数使用_vue3 a-form缓存提交保存数据-CSDN博客](https://blog.csdn.net/qq_41594043/article/details/103157587)
> 作者：[小雨繁星儿](https://blog.csdn.net/qq_41594043 "小雨繁星儿")

1、首先要写一个将数据缓存到本地的方法

```jsx
setLocal() { 
    let localData =this.form.getFieldsValue()
    let questions = []
    this.input.map(item => {
    if(item.question!==''||item.answer!=='')
        questions.push(item)
    })
    localData.tips = questions
    localData.beginTime = localData.beginTime? localData.beginTime.format("YYYY-MM-DD"):null        
    console.log(localData)
	let valuesStr = JSON.stringify(localData)
	window.localStorage.setItem('recordData',valuesStr)
	this.$message.success('保存成功！');
},
```

其实主要就是 window.localStorage.setItem(‘recordData’,valuesStr) 这行代码

注：localStorage只能set字符串格式的数据，所以别忘了先用JSON.stringify()转成字符串 稍后取数据再用JSON.parse()转回对象即可

2、页面加载mounted取数据

```jsx
if(window.localStorage.getItem('recordData')) {
  let getLocal = JSON.parse(window.localStorage.getItem('recordData'))
  console.log(getLocal)
  this.$nextTick(() =>{
  this.form.setFieldsValue(
  pick(getLocal,'beginTime','address','recorder','asker','joinIds','remark','nmgName','tele','leaveAddr','workCom','ageNum','gender','education','nmgIds')
  )
  this.form.setFieldsValue({
	  beginTime:getLocal.beginTime?moment(getLocal.beginTime):null
  })
});          
if(getLocal.tips.length<= this.input.length) {
	getLocal.tips.map((item,index) => {
	  this.input[index] = item
	})
} else {
	this.input = getLocal.tips            
	let num = Number(getLocal.tips.length)-3            
	for (i = 0; i < num; i++) {
	  this.questionArray.push({})
	}
}
  console.log(this.input)
}
```

主要代码：JSON.parse(window.localStorage.getItem(‘recordData’)
取出数据后，按照自己的情况，将数据填充至表单即可 （我这里使用的UI框架是vue ant design ）

3、开启定时器
再然后就是关键的 怎么定时自动保存呢？

当然是要用到定时器啦，but单纯的使用setInterval会导致页面卡死，setInterval不会清除定时器队列，每重复执行1次都会导致定时器叠加，最终卡死，
但是setTimeout是自带清除定时器的，因此此方法可以实现每隔一段时间执行一次方法的功能。以下方法在method里定义 created或者mounted里调用都可以

```jsx
changeValue() {
  //console.log("我是定时器 ")      
  this.timer = window.setInterval(() => {
	setTimeout(this.setLocal(), 0)
  }, 10000)
}
```

4、关闭定时器
由于我的项目是一个管理系统，所以有时只是切换路由，并未将表单页面销毁，所以这里关闭定时器的操作我就没放在beforeDestroy钩子里，而是一个离开当前路由之前的钩子函数– beforeRouteLeave代码如下

```jsx
beforeRouteLeave(to, form, next) {
    if (this.timer) { 
	    // 如果定时器还在运行 或者直接关闭，不用判断      
	    clearInterval(this.timer) // 关闭    
	}
    next()
}
```


切换进入当前路由之前的钩子函数 beforeRouteEnter

```jsx
beforeRouteEnter(to, form, next) {
    //离开该路由之前想进行的操作    
    next()
}
```