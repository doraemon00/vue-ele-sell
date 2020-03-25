
<a name="HVKxc"></a>
## 说明

---

vue项目，主要实现功能是外卖应用中的核心模块——商家功能<br />技术栈：Vue + BScroll<br />

<a name="OfTFF"></a>
## 项目安装

---



```
克隆项目
git clone https://github.com/doraemon00/vue-ele-sell.git

安装依赖
npm install

运行项目
npm run dev

发布环境
npm run build
```

<br />
<br />

<a name="s7rn9"></a>
## 实现功能

---

- 首页header部分，点击会出现弹窗，展示商家信息
- Goods（商品）、Ratings（评论）、seller（商家）三大路由组件视图均可滚动
- 商品页中，左菜单，右商品列表实现联动效果
- 评论页中，实现星级评价展示，评价类型筛选展示
- 商家页中，实现根据对应商家ID的收藏功能，商家实景可左右滑动
- 购物车模块，添加商品动画以及购物车基本功能


<br />

<a name="tNkZy"></a>
## 效果演示

---

**扫码体验**<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/618347/1585111466864-4a9c2a12-8968-496f-907f-5d61b890a13b.png#align=left&display=inline&height=240&name=image.png&originHeight=292&originWidth=300&size=8124&status=done&style=none&width=247)<br />
<br />
<br />[线上地址](http://ele.wykl.top/)<br />
<br />

<a name="9LKeX"></a>
## 问题汇总

---

<a name="L9mdD"></a>
### 移动端1px实现原理
**问题**<br />设计稿中750在移动端，比如iphone6(dpr为2)中就相当于350px,那么其中的1px就相当于0.5px,也就是需要我们进行1px的处理<br />
<br />**常用解决方案**<br />1.transform + 伪元素<br />2.媒体查询根据DPR进行缩放（方案1升级版）<br />

<a name="DN2Ix"></a>
### css模块的运用

- 图标：icon.css   文字图标样式
- 公共：base.css   处理一些公共样式，比如一像素，清除浮动，网站字体
- 工具：mixin.css  stylus语法函数



<a name="Crebm"></a>
### sticky-footer 布局
**实现效果**<br />如果页面内容不够长的时候，页脚块粘贴在视窗底部；如果内容足够长时，页脚会被内容向下推送。（不同于底部fixed）<br />
<br />**实现方案**<br />1.flex布局
```
<body class="Site">
  <header>…</header>
  <main class="Site-content">…</main>
  <footer>…</footer>
</body>

.Site {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

.Site-content {
  flex: 1;
}
```

<br />2.absolute
> 需要指定html、body 100%的高度，且content的padding-bottom需要与footer的height一致。

```
html, body {
    height: 100%;
}
.wrapper {
    position: relative;
    min-height: 100%;
    padding-bottom: 50px;
    box-sizing: border-box;
}
.footer {
    position: absolute;
    bottom: 0;
    height: 50px;
}
```


<a name="E00wE"></a>
### 组件间通讯

- 父传子
- 子传父
- 兄弟通讯
  - EventBus，创建中央事件总线来触发事件和监听事件
  - Vuex

**<br />**父传子：props**<br />在子组件定义props接收父组件传来的数据对象
```html
简要摘要
//父组件
<v-son :titles="titles"></v-son>

//子组件
props:{
	titles:{
  	type:Object
  }
}
```
**<br />**子传父：$emit**<br />子组件中通过$emit派发事件，父组件通过@接收监控
```html
//子组件<v-son>
<button @click="send"></button>
methods:{
	send(){
	this.$emit('send',value)
	}
}

//父组件
<v-son @send="receive"><v-son>
methods:{
	receive(e){
		console.log(e)
	}
}
```
**<br />**非父子组件之间的通信**
```html
//新建一个vue实例作为中央事件的总线
const event = new Vue()

//监听事件
event.$on('eventName',(val)=>{
  //do something
})

//触发事件
event.$emit('eventName','this is a message')
```

<br />

<a name="uz6EC"></a>
### 星星评分组件的实现

<br />1.根据屏幕适配定义通用函数，决定图片的显示
```html
stylus语法 

bg-image($url)
    background-image: url($url + '@2x.png')
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3)
        background-image: url($url + '@3x.png')
```

<br />2.新建星星组件
```html
添加对应尺寸图标到项目文件夹中（可以直接添加到这个star文件夹下）

定义css样式

.star
  font-size: 0
  .star-item
    display: inline-block
    background-repeat: no-repeat
  &.star-48
    .star-item
      width: 20px
      height: 20px
      margin-right: 22px
      background-size: 20px 20px
      &:last-child
        margin-right: 0
      &.on
        bg-image('star48_on')
      &.half
        bg-image('star48_half')
      &.off
        bg-image('star48_off')
  &.star-36
    .star-item
      width: 15px
      height: 15px
      margin-right: 6px
      background-size: 15px 15px
      &:last-child
        margin-right: 0
      &.on
        bg-image('star36_on')
      &.half
        bg-image('star36_half')
      &.off
        bg-image('star36_off')
  &.star-24
    .star-item
      width: 10px
      height: 10px
      margin-right: 3px
      background-size: 10px 10px
      &:last-child
        margin-right: 0
      &.on
        bg-image('star24_on')
      &.half
        bg-image('star24_half')
      &.off
        bg-image('star24_off')
```

<br />3.对请求数据中星星的数量进行处理
```html
定义常量，方便管理

const LENGTH = 5;
const CLS_ON = "on";
const CLS_HALF = "half";
const CLS_OFF = "off";


计算属性中：
computed: {
    itemClasses() {
      let result = [];
      let score = Math.floor(this.score * 2) / 2;
      let hasDecimal = score % 1 !== 0;
      let integer = Math.floor(score);
      for (let i = 0; i < integer; i++) {
        result.push(CLS_ON);
      }
      if (hasDecimal) {
        result.push(CLS_HALF);
      }
      while (result.length < LENGTH) {
        result.push(CLS_OFF);
      }
      return result;
    }
  }
```

<br />

<a name="NO9hd"></a>
### Better-scroll框架使用
> 需要注意：在页面需要进行点击事件的时候，需要设置 click:true


<br />使用中需要注意的问题：<br />1.布局需要外层容器包裹内层容器，wrapper->content，其中滚动的区域为content<br />2.当content的高度不超过父容器的高度，是不能滚动的<br />