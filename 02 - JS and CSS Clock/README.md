# Day 02 | 纯JS+CSS时钟
>author：[shineee](https://github.com/orangeshinee) \
>创建时间：20170602

## [在线效果](http://blog.shineee.win/JavaScript30-Challenge/02%20-%20JS%20and%20CSS%20Clock/index-shine.html)

![clock](http://oekt5d96o.bkt.clouddn.com/17-6-2/19883232.jpg)

---

### **主要步骤**：
- 通过获取系统时间取得钟表时刻
- 将秒、分、时分贝转化为钟表上的角度
- 每秒运行一次，每一次运行更改各指针旋转角度

### **代码说明**
- 主体
```html
    <div class="clock">
        <div class="clock-face"> <!--the apperace of the clock -->
            <div class="hand hour-hand" style="background: red"></div>
            <div class="hand min-hand" style="background: yellow"></div>
            <div class="hand second-hand"></div>
        </div>
    </div
```

- style样式
```css
.clock {
            width: 30rem;
            height: 30rem;
            border: 5px solid skyblue;
            border-radius: 50%; /* 弧度 使其变为圆形*/
            position: relative;/* 相对定位 */
            margin: 50px auto;
            padding: 1rem;
        }
```
```css
 .hand {
            width: 50%;
            height: 4px;
            background: black;
            position: absolute;/*指针位置固定于clock中*/
            top: 50%;
            transform-origin: 100%; 
            /*使指针的旋转中心为右侧，也可以使用right */
            transition: all 1.5s;
            transform: rotate(90deg);/*使指针初始指向为12点*/
            box-shadow:/*指针阴影*/
                0 0 0 .1px #fff,
                0 0 0 0.5px rgba(0,0,0,0.1),
                0 0 0.5px rgba(0,0,0,0.4),
                2px 3.5px .5px rgba(0, 0, 0, .5);
            transition-timing-function: cubic-bezier(0.9, 0.54, 0.26, 1.68)    ;
        }
```
```css
.min-hand {
            width: 36%;/*更改分针长度 下同*/
            margin-left: 14%;
            /*因为width更改所以margin随同更改，
            两者相加为50%，以保证指针旋转中心仍在右侧*/
            transition: all 2s; /*初始化转动时间 下同*/
          }

.hour-hand{
            width: 24%;
            margin-left: 26%;
            transition: all 3s;
          }
```

- JS部分
```javascript
 <script>//脚本动作
        //声明时分秒三个变量
        const handsecond = document.querySelector('.second-hand');
        const handmin = document.querySelector('.min-hand');
        const handhour = document.querySelector('.hour-hand');      

        function setDate()
        {
            const now = new Date();
            const seconds = now.getSeconds();
            const secdegrees = (seconds/60* 360)+90;
            handsecond.style.transform = `rotate(${secdegrees}deg)`;
            
            /*
            解决指针到12点时角度突变问题
            当指针指向12点时，角度从450度突变到90，所以在这里添加一个if/else
            当角度为90时，transtion的时间为0 即停止旋转 可以解决问题
            */
            if (secdegrees === 90) handsecond.style.transition = 'all 0s';
            else handsecond.style.transition = 'all .5s';

            const mins = now.getMinutes();
            const mindegrees = (mins/60*360)+90;
            handmin.style.transform = `rotate(${mindegrees}deg)`;

            if (mindegrees === 90) handmin.style.transition = 'all 0s';
            else handmin.style.transition = 'all 0.15s';
            
            const hours = now.getHours();
            const hourdegrees=((hours/12)*360)+90+((mins/60)*30)-360;
            handhour.style.transform = `rotate(${hourdegrees}deg)`;

        }

        setInterval(setDate,1000);//每秒运行一次setDate
        //setDate(); 
        /*加上这个function可以使打开页面时直接显示当前时间，
        没有指针从12点旋转到当前时间的动画。
        没有美感所以删掉了=￣ω￣=*/
    </script>
```
- 相关方法
 
  HTML5向Web API新引入了document.querySelector以及document.querySelectorAll两个方法用来更方便地从DOM选取元素，功能类似于jQuery的选择器。<br>
  W3School关于方法的[解释说明](https://www.w3schools.com/jsref/met_document_queryselector.asp)。
```javascript
    document.querySelector()
    /*该方法返回满足条件的单个元素。
    按照深度优先和先序遍历的原则使用参数提供的CSS选择器在DOM进行查找，
    返回第一个满足条件的元素。*/
```
```javascript
    document.querySelectorAll()
    /*该方法返回满足条件的所有元素。
    该方法返回所有满足条件的元素，结果是个nodeList集合。
    查找规则与前面所述一样。*/
```


