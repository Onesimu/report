---
marp: true
title: 转正述职报告
description: 技术部田伟
theme: uncover
paginate: true
_paginate: false
---

# 前端工作内容
- 网页设计
- 客户端 小程序开发
- 网页应用

## 技术
- HTML/CSS
- JavaScript

---

### 网页设计(页面重构, 切图)
- 输入 设计图(psd, png)
- 输出 html页面(HTML, CSS, 图片)

- 标注 pxCook, 蓝湖, Photoshop CC
- 规格 750 * 1334 iPhone6 二倍设计稿
- 布局方式 div absolute flex
- 单位 px

---

#### 布局方式
- 行盒 IFC text-align line-height vertical-align
- 块盒 *BFC* margin width height
- inline block
- table table-cell
- float
- *position* top left
- *flex* justify-content align-items
- grid grid-template-rows grid-template-columns

---

#### 单位
相对长度单位包括： *em*, ex, ch, *rem*, *vw*, vh, vmax, vmin
绝对长度单位包括： cm, mm, q, in, pt, pc, *px*
1in = 2.54cm = 25.4 mm = 101.6q = 72pt = 6pc = 96px
px: 相对于设备的长度单位，像素是相对于显示器屏幕分辨率而言的。

---

###### 固定单位布局 [px]
> 页面上的所有元素的尺寸一律使用px，pt这种固定单位编写，在<head>里添加
```
<meta name="viewport" content="width=device-width,initial-scale=1.0">
```
然后根据设计稿的宽高设定实现稿即可。

> 通过JS动态修改标签的initial-scale使得页面等比例缩放， 从而刚好占满整个屏幕。

> 优势：
开发简单： 缩放交给浏览器，开发人员不需要自己处理，完全按照视觉稿切图
还原精准： 绝对等比例缩放，可以精准还原原始视觉效果
测试方便： 可以在pc端实现大部分的测试工作，手机端只要修改一些细节

---

## 客户端开发统一平台
 - Flutter (Google, Dart, Fuchsia) 
 - uni-app (DCloud, Js/Vue, mp) 
 - taro (京东, Js/React, mp)

## js功能 组件化
React 函数组件 hooks
无侵入 纯HTML模板
```
<div> 
 <p data-if="{user.id==50}" data-text="用户ID等于50">xxx</p> 
 <p>其他内容</p> 
</div> 
```
声明式的数据 接口 交互管理
数据同构 传输透明 交互规则化
原型绑定 数据库设计 ui设计 全局统一规则控制
规则数据化 代码解析数据执行 技术和业务分离

---
```
@dom def render = {
  val githubUserName = Var("")
  def inputHandler = { event: Event => githubUserName := event.currentTarget.asInstanceOf[Input].value }
  <div>
    <input type="text" oninput={ inputHandler }/>
    { val name = githubUserName.bind
      if (name == "") { <div>Please input your Github user name</div> } 
      else {
        val githubResult = FutureBinding(Ajax.get(s"https://api.github.com/users/${name}"))
        githubResult.bind match {
          case None => <div>Loading the avatar for { name }</div>
          case Some(Success(response)) =>
            val json = JSON.parse(response.responseText)
            <img src={ json.avatar_url.toString }/>
          case Some(Failure(exception)) => <div>{ exception.toString }</div>
        }
      }
    }
  </div>
}
```

---

```
 const Fetch = () => {
   const getUrl = text => `https://api.github.com/search/repositories?q=${text}`
   const { value, bind } = useField('react')
   const { data, loading, setUrl } = useFetch(getUrl('react'))
   return (
     <div>
       <input type="text" value={value} {...bind} />
       <button onClick={() => { setUrl(getUrl(value)) }} >
         search
       </button>
       {
         loading ? <div>Loading...</div>
           : (<span>{`total_count: ${data.total_count}`}</span>)
       }
     </div>
   )
 }
  return <Fetch />
```
---
- 如果用户名为空，显示“请输入用户名”的提示文字；
- 如果用户名非空，发起 Github API，并根据 API 结果显示不同的内容：

- 如果尚未加载完，显示“正在加载”的提示信息；
- 如果成功加载，把回应解析成 JSON，从中提取头像 URL 并显示；
- 如果加载时出错，显示错误信息。
---
每一行代码都可以对应验收标准中的一句话，描述着业务规格，而非“异步流程”这样的技术细节。

让我们回顾一下验收标准，看看和源代码是怎么一一对应的：

如果用户名为空，显示“请输入用户名”的提示文字；
```
if (name == "") {
<div>Please input your Github user name</div>
```
如果用户名非空，发起 Github API，并根据 API 结果显示不同的内容：
```
} else {
val githubResult = FutureBinding(Ajax.get(s"https://api.github.com/users/${name}"))
githubResult.bind match {
```

---

如果尚未加载完，显示“正在加载”的提示信息；
```
case None =>
  <div>Loading the avatar for { name }</div>
```  

如果成功加载，把回应解析成 JSON，从中提取头像 URL 并显示；
```
case Some(Success(response)) =>
  val json = JSON.parse(response.responseText)
  <img src={ json.avatar_url.toString }/>
```
如果加载时出错，显示错误信息。
```
case Some(Failure(exception)) => // 如果加载时出错，
  <div>{ exception.toString }</div> // 显示错误信息。
```
---

# 预处理
parcel 
postHtml postCss babel

# 运行环境优化
http2
http3(QUIC)