vscode  px 转 rem  插件 cssrem
font-size 推荐使用px
纵向高度使用px 横向宽度使用rem （包括margin padding）； 需要整屏显示的内容，纵向高度建议使用rem  原因：移动设备宽度有限，高度可以无限滚动；
border， border-radius， box-shadow使用px；

设计稿标注工具： markman PxCook

//单行css截字
div{
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
}
//多行截字
div{
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    overflow: hidden;
}

盒模型：
1.标准盒模型： box-sizing: conten-box; 宽度只包含设置的宽度,padding和border会占有额外的空间
2.IE盒模型： box-sizing: border-box; 宽度包含设置的宽度、padding和border，都占有已设宽度的空间

//为页面所有元素设置固定的盒模型
*, *:before, *:after {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

移动端自适应适配：
vw 视口的宽度 vh 视口的高度  rem相对于根元素HTML的字体大小的单位
rem布局非常简单，其基本原理就是根据屏幕不同的分辨率,动态修改根字体的大小,
让所有的用rem单位的元素跟着屏幕尺寸一起缩放,从而达到自适应的效果。

设计稿宽度是750px， 可以这样配置：
html {
  font-size: calc(100vw / 7.5);
}
7.5 是根据设计稿的屏幕宽度决定的，这样750宽度下的根元素字体大小就是 750 / 7.5 = 100px = 1rem;
不改变默认字体的展示
#app {
    font-size: initial; //重置页面字体大小恢复为浏览器默认16px，否则就显示成50px了
}

优化，避免在大屏时过分扩大
html {
    //设置根字体大小单位为vw，页面元素的尺寸单位都设为rem，搭配vw和rem，可实现布局根据视口变化而变化
    font-size: calc(100vw / 7.5);
    // 同时，通过Media Queries 限制根元素字体最大最小值
    @media screen and (min-width: 320px) {
        font-size: 64px;
    }
    @media screen and (max-width: 540px) {
        font-size: 108px;
    }
}

// body 也增加最大最小宽度限制，避免默认100%宽度的 block 元素跟随 body 而过大过小
body {
    max-width: 540px;
    min-width: 320px;
}

#app {
    font-size: initial;
}

弹性布局原则： 文字流式，控件弹性，图片等比缩放


小程序：
App(Object)接受Object参数，指定小程序的生命周期回调等
必须在app.js中调用，必须调用而且只能调用一次，否则后果未知

Mp-vue开发小程序
· 彻底的组件化开发能力：提高代码复用性
· 完整的 Vue.js 开发体验
· 方便的 Vuex 数据管理方案：方便构建复杂应用
· 快捷的 webpack 构建机制：自定义构建策略、开发阶段 hotReload
· 支持使用 npm 外部依赖
· 使用 Vue.js 命令行工具 vue-cli 快速初始化项目
· H5 代码转换编译成小程序目标代码的能力
在未来最理想的状态是，可以一套代码可以直接跑在多端：WEB、小程序（微信和支付宝）、Native（借助weex）

第三方UI框架： WeUI， iview webApp vant Webapp

 小程序开发注意事项 
 1. 开发微信小程序时建议用 iPhone6 作为视觉稿的标准。工程师拿到750的设计稿，在PS中量取的容器大小，可以直接定义为rpx，不需要进行2倍尺寸的换算。 
 2. 经过测试，小程序对于:first-child、:last-child、.class-a .class-b{}，甚至更多层级的嵌套都是支持的。 不过官方并不推荐级联的这种写法，因为考虑到后面切Native的扩展可能，会没办法支持级联选择。保险起见，不建议.class-a .class-b{}这种级联的写法，以免后期工具过滤导致页面错乱 
 3. 小程序会加入自动补全css前缀，使用的插件是postcss的autoprefixer，设置的兼容级别是> ios 8及> android 4.1。我们在写css的时候只需要写没有前缀的写法。比如：display:flex，工具自动编译为display:flex;display:-webkit-flex

小程序的最终渲染载体依然是浏览器内核，但是与传统网页UI渲染和JS脚本在同一线程执行不同的是：小程序基于性能考虑，启用了双线程的模型：
1. 视图层即webview线程，负责启用不同的webview来渲染不同的小程序页面；
2. 逻辑层：一个单独的线程执行js代码，可以控制视图层的逻辑。


vue
1. mixins使用
    1. 同名钩子函数将合并为一个数组，都会被调用，且混入对象的钩子函数将在组件自身钩子函数调用之前调用
    2. methods，components等会被合并为一个对象，对象键名冲突时取组件的键值对，一切以组件优先
    3. data冲突时也是以组件数据优先
2. 渲染函数的使用
    在根据不同条件显示不同标签元素时，可以用render函数代替if判断
3. 函数式组件

设计原则：
1. 单一职责原则
2. 开闭原则 ： 对扩展开放，对修改关闭

设计模式：
1. 策略模式
定义 : 要实现某一个功能，有多种方案可以选择。我们定义策略，把它们一个个封装起来，并且使它们可以相互转换。