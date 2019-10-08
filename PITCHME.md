# 前端工作内容
- 网页设计
- 客户端 小程序开发
- 前端独立开发

## 技术
- HTML
- CSS
- JavaScript

### 网页设计(页面重构, 切图)
- 输入 设计图(psd, png)
- 输出 html页面(HTML, CSS, 图片)

- 标注 pxCook, 蓝湖, Photoshop CC
- 规格 750 * 1334 iPhone6 二倍设计稿
- 布局方式 div flex
- 单位 px

#### 布局方式
- 行盒 IFC text-align line-height vertical-align
- 块盒 BFC margin width height
- inline block
- table table-cell
- float
- position top left
- flex justify-content align-items
- grid grid-template-rows grid-template-columns

#### 单位
相对长度单位包括有： em, ex, ch, rem, vw, vh, vmax, vmin
绝对长度单位包括有： cm, mm, q, in, pt, pc, px
1in = 2.54cm = 25.4 mm = 101.6q = 72pt = 6pc = 96px
相对于设备的长度单位，像素是相对于显示器屏幕分辨率而言的。Windows用户所使用的分辨率一般是96像素/英寸。而MAC用户所使用的分辨率一般是72像素/英寸。

##### 固定布局 [px]
> 页面上的所有元素的尺寸一律使用px，pt这种固定单位编写，在<head>里把
```
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=0">
```
然后根据设计稿的宽高设定实现稿即可。

> 这种方式简单易上手，缺点显而易见，不能根据不同的屏幕做出不同的表现。例如直接设定主体宽度，然后居中展示，两边留白。宽屏两边留白多，窄屏两边留白少。
移动端使用固定布局
在viewport meta标签上设置content = “width=320”， 页面的各个元素也采用px作为单位。通过用JS动态修改标签的initial-scale使得页面等比例缩放， 从而刚好占满整个屏幕。这种方案类似弹性布局的rem。
在viewport meta标签上设置content=“width=640，user-scalable=no”，页面的各个元素采用px作为单位。由于手机浏览器的宽度小于640px(逻辑像素)（iphone plus系列为414px），所以浏览器viewport会自动缩放至全屏大小。经典案例：荔枝FM,人人都是播客的移动站

> 优势：
开发简单： 缩放交给浏览器，开发人员不需要自己操心，完全按照视觉稿切图
还原精准： 绝对等比例缩放，可以精准的还原原始视觉效果（会有清晰度的失真）
测试方便： 可以在pc端实现大部分的测试工作，即开发人员自己就能完成测试的大部分工作，手机端只要修改一些细节。

> 劣势：
像素丢失： 对于一些分辨率较低的手机，可能设备像素还未达到viewport指定的宽度，此时可能出现边框丢失等问题。现代手机基本不会发生这种情况。
缩放失效： 早期android手机不能根据meta中的width来进行缩放，需要配合initial-scale。这种完全依赖浏览器的方式也难免可能发生异常。
文本折行： 会发生在缩放失效的机型中。

# 客户端开发统一平台
 flutter uniapp taro

# js 功能 组件
无侵入 纯HTML原生模板
声明式的数据 接口 界面管理
数据同构 传输透明 界面规则化

react hook

# 预处理
parcel posthtml babel

# 后端
postgre postgrest lua js fdw 云db
nginx openresty caddy
内存表 消息队列

# 业务规则
数据库设计 ui设计 原型绑定 输出代码 全局统一规则控制
规则数据化 代码解析数据执行 技术和业务分离