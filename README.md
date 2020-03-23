
<a name="HVKxc"></a>
## 说明

---

vue项目，主要实现功能是外卖应用中的核心模块——商家功能<br />技术栈：Vue + BScroll

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



<a name="s7rn9"></a>
## 实现功能

---

- 首页header部分，点击会出现弹窗，展示商家信息
- Goods（商品）、Ratings（评论）、seller（商家）三大路由组件视图均可滚动
- 商品页中，左菜单，右商品列表实现联动效果
- 评论页中，实现星级评价展示，评价类型筛选展示
- 商家页中，实现根据对应商家ID的收藏功能，商家实景可左右滑动
- 购物车模块，添加商品动画以及购物车基本功能


<a name="tNkZy"></a>
## 效果演示

---


[线上地址](http://ele.wykl.top/)


<a name="9LKeX"></a>
## 问题汇总

---

<a name="L9mdD"></a>
### 移动端1px实现原理
**问题**<br />设计稿中750在移动端，比如iphone6(dpr为2)中就相当月350px,那么其中的1px就相当于0.5px,也就是需要我们进行1px的处理

**常用解决方案**<br />1.transform + 伪元素<br />2.媒体查询根据DPR进行缩放（方案1升级版）

<a name="DN2Ix"></a>
### css模块的运用

- 图标：icon.css 文字图标样式
- 公共：base.css 处理一些公共样式，比如一像素，清除浮动，网站字体
- 工具：mixin.css stylus语法函数