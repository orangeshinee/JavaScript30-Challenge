# Day 03 | JS控制CSS变量
>author：[shineee](https://github.com/orangeshinee) \
>创建时间：20170607

<br>
　　一不小心放了五天。。。<br>
　　果然人还是不能懒，，懒起来就不想动了。。

### [本课效果实例](https://blog.shineee.win/JavaScript30-Challenge/03%20-%20CSS%20Variables/index-shine.html)

### 主要步骤
- 创建全局变量
- 为img调用全局css变量
- JS部分，监听鼠标事件，通过改变input值来更改全局css变量

### 主要代码分析
```css
:root {/*全局变量声明*/
        --base: #f32f32;
        --spacing: 10px;
        --blur: 10px;
    }
    /*
    :root伪类匹配文档树的根元素。
    应用到HTML，:root 即表示为<html>元素，
    除了优先级更高外，相当于html标签选择器。
    */
```
> 更多关于:root内容，详见[文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:root)


```javascript
function handleUpdate(){
        //获取suffix为单位px。当无单位时则为空
        const suffix = this.dataset.sizing || '';
        document.documentElement.style.setProperty(`--${this.name}`,this.value+suffix);
    }
```

### 主要方法及属性
```css
filter: blur(10px)
```
- filter是一个强大的滤镜，包括blur(模糊)、brightness(亮度)、contrast(对比度)、drop-shadow(阴影)等等。详见[参考文献](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter)。


```javascript
document.documentElement.style.setProperty(`--${this.name}`,this.value+suffix);
```
- 设置属性并赋值。因为this.value只是数值，但是blur和spacing都有单位px，所以要加上单位suffix，即this.dataset.sizing。
```javascript
inputs.forEach(input => input.addEventListener('change',handleUpdate));
inputs.forEach(input => input.addEventListener('mousemove',handleUpdate));
```
- 鼠标有两个监听事件
- 1. <b>change</b> | 该事件仅适用于文本域（text field），以及 textarea 和 select 元素。在鼠标选择color时，此事件发生。
- 2. <b>mousemove</b> | 在滑块移动的时候监听值改变，以此改变全局CSS变量。