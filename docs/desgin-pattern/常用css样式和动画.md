## 文本太多时，将多余的文本隐藏并让其显示成点（显示一行）

```css
 white-space: nowrap;
/* 文本不换行 */
overflow: hidden;
/* 隐藏超出容器宽度的文本 */
text-overflow: ellipsis;
 /* 在超出容器宽度时使用省略号代替文本 */


文本太多时，将多余的文本隐藏并让其显示成点（显示两行）
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 2;
overflow: hidden;
text-overflow: ellipsis;
```

 

## 导航条flex布局

```css
display: flex;
align-items: center;
justify-content: space-around;
height: 44px;
```

 补充

```css
.kuai{
  display: flex;
  /* 让里面的元素水平方向居中 */
  /* justify-content: center; */
  /* 让里面的块级元素平均分配，不会触及到父元素的边界，并居中 */
  justify-content: space-evenly;
  /* 让两边的块级元素向两边靠拢，并和父元素的边界重合，并且彼此之间隔开距离 */
  /* justify-content: space-between; */
  /* 让两边的块级元素向两边靠拢，但是不会触及到父元素的边界，并且彼此之间隔开距离 */
  /* justify-content: space-around; */
}
```



## 表单表格布局

```css
table {
      border-collapse: collapse;
/* 设置表格合并边框 这种会合并所有的边框，所有的边框都显示不出来，
   如果想显示tr的边框，可以将下面的两行换成 border-collapse: collapse;然后设置tr的边框即可  */
      border-spacing: 0;
      margin: auto;
      text-align: center;
    }
    td,
    tr {
      border: 1px solid #ccc;
      /* 设置单元格的边框样式 */
      padding: 5px;
      /* 设置单元格的内边距 */
      height: 30px;
    }
    tr {
      width: 100%;
    }
    td {
      width: 200px;
    }
```

 

## 粉色按钮

```css
button {
      border: none;
      width: 60px;
      height: 29px;
      color: white;
      background-color: pink;
      font-size: 14px;
      font-weight: 500;
      cursor: pointer;
    }
```

 

## 遍历出很多的数据放在span中，设置的是span的样式

```css
.filterCates span {
    display: inline-block;
    padding: 5px 10px;
    margin-right: 10px;
    margin-top: 15px;
    border: 1px solid red;
   }
```

 

 

/* 用于设置元素在垂直方向上超出内容高度时的显示方式。其中，scroll 表示当元素内容高度超出可见部分时，会显示一个滚动条，以便用户可以通过滚动来查看完整的内容。 */

```css
  overflow-y: scroll;
```

 

 

```css
\>img {
width: 100%;
/* 把图片转换成块级元素可以去掉图片默认间距 */
display: block;
}
```



给老的商品加删除线

```css
text-decoration: line-through;
```



点击滚动到指定位置

```
/* 点击一级标题  二级滚动到相应距离 */

const containerRef = ref<any>(0);
const scrollToPosition = (index: number) => {
if (index >= 1) {
if (containerRef.value) {
let newshuzu = JSON.parse(JSON.stringify(zhuyao.value))
newshuzu.splice(index)
//console.log(newshuzu);
let changdu = 0;
newshuzu.forEach((item: any) => {
changdu += item.foods.length
})
//console.log(changdu);
containerRef.value.scrollTop = index * 40 + changdu * 90; // 将滚动位置设置为 200 像素
}
} else {
if (containerRef.value) {
containerRef.value.scrollTop = 0; // 将滚动位置设置为 0 像素
}
}

};
```

 

 

## 隐藏滚动条

```
.ce-center {
   background-color: white;
   width: 180px;
   font-size: 14px;
   overflow-y: auto; //将滚动条隐藏，让这一块变成可滚动的区域
}

  //将滚动条隐藏
  .ce-center::-webkit-scrollbar {
   display: none;
  }
```



## 点击按钮出现弹出层，并附带过渡效果（注意不能使用，v-if和v-show）

```
 中间块的老样式
transform: scale(0.9);
opacity: 0;
transition: all linear 0.3s;

中间块的新样式
transform: scale(1);
opacity: 1;
 
遮罩层的老样式
width: 100%;
height: 100vh;
position: fixed;
top: 0;
left: 0;
background-color: rgba(0, 0, 0, 0.0);
z-index: -10;
transition: all 0.3s;
 
遮罩层的新样式
z-index: 100 !important;
background-color: rgba(0, 0, 0, 0.5) !important;
transition: all 1s;
```

 

## 简易手写遮罩层

```
<!-- 遮罩层 -->
    <div class="ceng" :class="yincang === 1 ? 'dong' : ''">
        <div class="kuai" :class="yincang === 1 ? 'xinkuai' : ''">
            <div class="ti">
                <div>{{ text }}标签</div>
                <div class="bi"><img :src="chahao" alt="" style="width: 20px" @click="guanbi">
                </div>
            </div>
            <div class="shuju">
                <div class="li">
                    <div class="zuo"><span>*&nbsp;&nbsp;</span>标签：</div>
                    <div class="you">
                        <input type="text" v-model="shuru1" class="mo" placeholder="请输入标签">
                    </div>
                </div>
            </div>
            <div class="anniu">
                <el-button @click="guanbi" style="margin-right: 20px;">取消</el-button>
                <el-button type="primary" @click="jia">确认</el-button>
            </div>
        </div>
    </div>
    
// js部分  
import chahao from "@/assets/叉号.png" 
    
let yincang = ref(1)
let text = ref('')
let shuru1 = ref('')


//点击叉号或取消的时候
let guanbi = () => {
    yincang.value = 0
}

//点击确认的时候
let jia = () => {
    yincang.value = 0
}


//css样式
.ceng {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.0);
    z-index: -10;
    transition: all 0.3s;


    .kuai {
        width: 410px;
        margin: auto;
        margin-top: 10%;
        background-color: white;
        border-radius: 5px;
        z-index: 999;
        transform: scale(0.9);
        opacity: 0;
        transition: all linear 0.3s;


        .ti {
            width: 100%;
            height: 50px;
            line-height: 50px;
            display: flex;
            justify-content: space-between;
            padding: 0 20px;
            box-sizing: border-box;
            font-size: 14px;
            color: #17233d;
            font-weight: 700;

            div {
                font-size: 16px;
            }
        }

        .shuju {
            width: 100%;
            border-top: 1px solid #e8eaec;
            border-bottom: 1px solid #e8eaec;
            padding: 10px 40px 10px 30px;
            box-sizing: border-box;
            text-align: center;

            .li {
                width: 100%;
                height: 50px;
                line-height: 50px;
                display: flex;
                justify-content: space-around;

                .zuo {
                    width: 100px;
                    height: 100%;
                    text-align: right;

                    span {
                        color: #f56c6c;
                    }
                }

                .you {
                    width: 240px;
                    height: 100%;


                    .mo {
                        width: 100%;
                        height: 33px;
                        outline: none;
                        border: 1px solid #cdd0d6;
                        border-radius: 5px;
                        padding-left: 10px;
                        box-sizing: border-box;
                        transition: all 0.5s;
                    }


                    .new-class {
                        border: 1px solid #f56c6c;
                    }
                }
            }

        }

        .anniu {
            width: 100%;
            height: 60px;
            line-height: 60px;
            padding: 0 20px;
            box-sizing: border-box;
            text-align: right;

        }
    }

    .xinkuai {
        transform: scale(1);
        opacity: 1;
    }

}

.dong {
    z-index: 100 !important;
    background-color: rgba(0, 0, 0, 0.3) !important;
    transition: all 1s;
}
```







## 让表格的头部（thead）固定，（tbody）区域可以滚动

```
首先在table外面加一个盒子并给盒子设置这个属性
overflow-y: scroll;

然后给thead 里面的td加上
thead td {
      background-color: white;
      position: sticky;
      top: 0;
      z-index: 2;
      padding: 0;
    }
```



## 让tbody里的tr的颜色隔一行改变一个颜色，并在鼠标放到某个tr上时也改变颜色

```
tbody {

   /* 下面三个是交替出现不同的背景颜色，鼠标放上去也会变色 */

   tr:nth-child(odd) {
    background: #F9F9F9;
   }

   tr:nth-child(even) {
    background: white;
   }

   tr:hover {
    background: #F5F5F5;
   }

}
```

 

 

## 底部弹出，过渡，通过类名控制

```css
.modal-content {
 width: 100%;
 height: 75%;
 background-color: rgba(0, 0, 0, 0.6);
 color: white;
 position: fixed;
 bottom: 0rpx;
 transition: height 0.3s ease-in-out;//过渡效果
 z-index: 1001;
}
.modal-contents{
 height: 0;
}
```

 



## 一个可以滚动的表格，且头部固定

```scss
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fixed Header Table in Scrolling Container</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .container {
            width: 800px;
            height: 200px;
            overflow: auto;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th,
        td {
            padding: 10px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }


        tbody tr:nth-child(odd) {
            background: #F9F9F9;
        }

        tbody tr:nth-child(even) {
            background: white;
        }

        tbody tr:hover {
            background: #F5F5F5;
        }



        thead {
            position: sticky;
            top: 0;
            background-color: #f2f2f2;
        }
    </style>
</head>

<body>
    <div class="container">
        <table>
            <thead>
                <tr>
                    <th>Header 1</th>
                    <th>Header 2</th>
                    <th>Header 3</th>
                    <th>Header 4</th>
                </tr>
            </thead>
            <tbody>
                <!-- 添加更多行 -->
                <tr>
                    <td>Data 1</td>
                    <td>Data 2</td>
                    <td>Data 3</td>
                    <td>Data 4</td>
                </tr>
                <tr>
                    <td>Data 5</td>
                    <td>Data 6</td>
                    <td>Data 7</td>
                    <td>Data 8</td>
                </tr>
                <tr>
                    <td>Data 1</td>
                    <td>Data 2</td>
                    <td>Data 3</td>
                    <td>Data 4</td>
                </tr>
                <tr>
                    <td>Data 5</td>
                    <td>Data 6</td>
                    <td>Data 7</td>
                    <td>Data 8</td>
                </tr>
                <tr>
                    <td>Data 1</td>
                    <td>Data 2</td>
                    <td>Data 3</td>
                    <td>Data 4</td>
                </tr>
                <tr>
                    <td>Data 5</td>
                    <td>Data 6</td>
                    <td>Data 7</td>
                    <td>Data 8</td>
                </tr>

                <!-- 添加更多行 -->
            </tbody>
        </table>
    </div>
</body>

</html>
   
```

 

 

 

 

## 进入时从上到下拉伸，离开时从下到上收缩的动画

```
<td >
  <transition name="stretch" @before-enter="beforeEnter" @enter="enter" @leave="leave"
    @after-leave="afterLeave">
    <div :class="`caidan${index}`" v-show="yin[index]">
      <div v-for="(itemm, indexx) in item.child" class="xiaxuan">
        {{ itemm }}
      </div>
    </div>
  </transition>
</td>


//触发的事件
let beforeEnter = (el) => {
  el.style.transform = 'scaleY(0)';
}
let enter = (el, done) => {
  // 异步执行动画结束后的回调
  setTimeout(() => {
    el.style.transform = 'scaleY(1)';
    done();
  }, 0);
}
let leave = (el, done) => {
  el.style.transform = 'scaleY(0)';
  setTimeout(() => {
    done();
  }, 500);
}
let afterLeave = (el) => {
  el.style.transform = '';
}


//css的样式
.stretch-enter-active,
.stretch-leave-active {
  transition: transform 0.5s;
}

.stretch-enter,
.stretch-leave-to {
  transform: scaleY(0);
  transform-origin: center bottom;
}

```

 

 

## 遮罩层淡入淡出缩放

html

```html
<!-- 遮罩层 -->
        <div class="ceng" :class="yincang === 1 ? 'dong' : ''" :key="10">
            <div class="kuai" :class="yincang === 1 ? 'xinkuai' : ''">
                <div class="ti">
                    <div>{{ text }}</div>
                    <div class="bi"><img :src="chahao" alt="" style="width: 20px;margin-top: 15px;" @click="guanbi">
                    </div>
                </div>
                <div class="shuju">
                    <div class="li">
                        <div class="zuo">平台名</div>
                        <div class="you">
                            <el-input />
                        </div>
                    </div>
                    <div class="li">
                        <div class="zuo">联系人</div>
                        <div class="you">
                            <el-input />
                        </div>
                    </div>
                    <div class="li">
                        <div class="zuo">电话</div>
                        <div class="you">
                            <el-input />
                        </div>
                    </div>
                    <div class="li">
                        <div class="zuo">注册时间</div>
                        <div class="you">
                            <el-input />
                        </div>
                    </div>
                    <div class="li">
                        <div class="zuo">基地</div>
                        <div class="you">
                            <el-input />
                        </div>
                    </div>
                    <div class="li">
                        <div class="zuo">分配比例</div>
                        <div class="you">
                            <el-input />
                        </div>
                    </div>
                </div>
                <div class="anniu">
                    <el-button @click="guanbi">取消</el-button>
                    <el-button type="primary" @click="jia">{{ an }}</el-button>
                </div>
            </div>
        </div>
```

 css

```scss
    .ceng {
        width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        left: 0;
        background-color: rgba(0, 0, 0, 0.0);
        z-index: -10;
        transition: all 0.3s;

        .kuai {
            width: 460px;
            height: 500px;
            margin: auto;
            margin-top: 10%;
            background-color: white;
            border-radius: 5px;
            z-index: 999;
            transform: scale(0.9);
            opacity: 0;
            transition: all linear 0.3s;


            .ti {
                width: 100%;
                height: 50px;
                line-height: 50px;
                display: flex;
                justify-content: space-between;
                padding: 0 20px;
                box-sizing: border-box;
                font-size: 14px;
                color: #17233d;
                font-weight: 700;
            }

            .shuju {
                width: 100%;
                height: 380px;
                border-top: 1px solid #e8eaec;
                border-bottom: 1px solid #e8eaec;
                padding: 10px 50px;
                box-sizing: border-box;
                text-align: center;

                .li {
                    width: 100%;
                    height: 50px;
                    line-height: 50px;
                    display: flex;
                    justify-content: space-around;

                    .zuo {
                        width: 70px;
                        height: 100%;
                        text-align: right;
                    }

                    .you {
                        width: 240px;
                        height: 100%;

                    }
                }

            }

            .anniu {
                width: 100%;
                height: 60px;
                line-height: 60px;
                padding: 0 20px;
                box-sizing: border-box;
                text-align: right;

            }
        }

        .xinkuai {
            transform: scale(1);
            opacity: 1;
        }
    }
```

 

将数据存储在本地   如果有的话使用本地的，然后监听数据，改变的话就把最新的数据存储在本地

```js
let list = ref([])
//将数据存储在本地   如果有的话使用本地的，然后监听数据，改变的话就把最新的数据存储在本地
const tryget = localStorage.getItem('list')
if (tryget) {
  list.value = JSON.parse(tryget)
}

watch(list.value, (newlist) => {
  localStorage.setItem('list', JSON.stringify(newlist));
})
```



文字和图片怎么让他在同一水平线

```css
/* 垂直居中对齐 */  给他们外面的盒子设置
display: flex;
align-items: center;
```



## 让一个小图片旋转

```css
//给这个图片设置一个状态   点击后让这个状态改变，根据这个状态true时加这个类名xuanzhuan，false时加这个类名houzhuan

.xuanzhuan {
        transform: rotate(180deg);
        transition: transform 0.3s ease;
      }

.houzhuan {
     transform: rotate(0deg);
     transition: transform 0.3s ease;
   }


```



## 颜色渐变

```css
background: linear-gradient(0deg, #29b0d4 0%, #11f8cd 100%); //线性渐变从前面的那个元素过渡到后面的那个元素
```



## 让输入框校验时产生红色边框

```js
<div class="you">
<input type="text" v-model="shuru1" class="mo" @blur="checkInput" placeholder="请输入品种类型">
</div>


//遮罩层里的输入框效果
let checkInput = (event) => {
    if (event.target.value === '') {
        event.target.classList.add('new-class');
    } else {
        event.target.classList.remove('new-class');
    }
}


.you {
    width: 240px;
    height: 100%;


    .mo {
        width: 100%;
        height: 33px;
        outline: none;
        border: 1px solid #cdd0d6;
        border-radius: 5px;
        padding-left: 10px;
        box-sizing: border-box;
        transition: all 0.5s;
    }


    .new-class {
        border: 1px solid #f56c6c;
    }
}
```

## 设置一个输入框的最大值和最小值

```js
    <input type="number" placeholder="请输入0~24之间的数字" v-model="iptvalue"  @input="bian" />

    //设置一个输入框的最大值和最小值    
	//我们使用 nextTick 来确保在用户输入完成后再执行处理逻辑，这样可以避免在用户输入过程中立即对输入进行处理，从而更加准确地控制输入的逻辑。
	const bian = (event) => {
		nextTick(() => {
			const value = parseFloat(iptvalue.value);
			if (value > 24) {
				iptvalue.value = '24';
			} else if (value < 0) {
				iptvalue.value = '0';
			}
		});
	};
```



## 让他里面的文字不了选中

```css
span,
p,
div {
    user-select: none;
}
```



## 点击按钮时改变按钮颜色

```css
view:active {
  background-color: #3292FF;
  color: white;
  transition: all 0.5s; 
}
```



## 一个块里面有三个块横向排列并平均分配，每个块里面是图片在上文字在下的格式

```css
.luru .luru-btn .btn-one {
  width: 100%;
  padding: 20rpx 0;
  box-sizing: border-box;
  display: flex;
  justify-content: space-evenly;
}


.luru .luru-btn .btn-one .one-div {
  width: 200rpx;
  height: 190rpx;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #3B3BC5;
  border-radius: 10px;
  color: white;
}
```



## 文字之间隔开距离

```css
letter-spacing: 0.2rem;
```



## 让图片撑满整个容器，且不变形 

```css
img {
  让图片撑满整个容器，且不变形 
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
}
```



## 清除图片的空白

```css
//清除图片的留白    要直接设置在图片本身上
vertical-align: middle;
```





## 获取当前日期

```js
const date = new Date();
let today = date.toLocaleDateString()//2023/12/23
```



## 实现地图拖拽放大的效果

```js
<template>
    <div class="bao">
        <div class="li" :style="{ position: 'absolute', transform: 'scale(' + scale + ')' }" @wheel="gundong"
            @mousedown="mapdown" ref="boxRef">
            <!-- 里面放入要缩放拖拽的内容 -->

        </div>
    </div>
</template>
<script setup>
import { ref } from "vue"

let scale = ref(1)
let boxRef = ref(null)

//滚轮滚动
let gundong = (e) => {
    e = e || window.e
    if (e.wheelDelta < 0) {
        console.log("向下滚")
        scale.value -= 0.2
    } else {
        console.log("向上滚")
        scale.value += 0.2
    }

    if (scale.value < 1) {
        scale.value = 1;
    } else if (scale.value > 3.5) {
        scale.value = 3.5;
    }
}

//鼠标按下的时候
let mapdown = (e) => {
    console.log(boxRef.value.offsetLeft);
    var x1 = e.pageX - boxRef.value.offsetLeft;
    var y1 = e.pageY - boxRef.value.offsetTop;
    document.onmousemove = function (e) {
        boxRef.value.style.left = e.pageX - x1 + 'px';
        boxRef.value.style.top = e.pageY - y1 + 'px';
    }
    document.onmouseup = function () {
        document.onmousemove = null;
    }
}

</script>
<style lang="scss">
.bao {
    width: 800px;
    height: 800px;
    background-color: #696969;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    overflow: hidden;
    transition: 0.1s;


    .li {
        width: 600px;
        height: 400px;
        background-color: aquamarine;
    }
}
</style>

```



## 大悟地图拖拽放大的效果

```
vue_data['scale'] = 1
vue_data['left'] = 0
vue_data['top'] = 100
vue_data['down'] = false

//鼠标滚轮的时候
vue_methods['mapscale'] = function (e) {
    let that = this;
    that.scale -= (e.deltaY / 1000) * 1.6;//滚动放大的倍率，为原来的1.6倍
    if (that.scale < 1) {
        that.scale = 1;
    } else if (that.scale > 4.5) {
        that.scale = 4.5;
    }
}

//鼠标按下时候
vue_methods['mapmove'] = function (e) {
    let that = this;
    if (that.down) {
        that.left += e.movementX / that.scale;
        that.top += e.movementY / that.scale;
    }

}
//鼠标移动的时候
vue_methods['mapdown'] = function (e) {
    let that = this;
    that.down = true;
}
//鼠标松开的时候
vue_methods['mapup'] = function (e) {
    let that = this;
    that.down = false;
    console.log("释放了")
}






 <div :style="'transition: .1s; transform: scale(' + scale + ') translate(' + left + 'px, ' + top + 'px)' " @@mousedown="mapdown" @@mousemove="mapmove" @@mousewheel="mapscale" @@mouseup="mapup">
//里面是要拖拽的东西


</div>


```



## VUE3地图拖拽放大效果

```
<template>
    <div class="con" @mouseleave="mapup">
        <div class="box" :style="'transform: scale(' + scale + ') translate(' + left + 'px, ' + top + 'px)'"
            @mousewheel="mapscale" @mousedown="mapdown" @mousemove="mapmove" @mouseup="mapup">
            <!-- 里面是SVG图片 -->
        </div>
    </div>
</template>
<script setup>
import { ref, onMounted } from "vue"
let scale = ref(1)
let left = ref(0)
let top = ref(0)
let down = ref(false)

//鼠标滚轮的时候
let mapscale = (e) => {
    scale.value -= (e.deltaY / 1000) * 1.6;//滚动放大的倍率，为原来的1.6倍
    if (scale.value < 1) {
        scale.value = 1;
    } else if (scale.value > 4.5) {
        scale.value = 4.5;
    }
}
//鼠标按下时候
let mapdown = (e) => {
    down.value = true;
    console.log('按下了2');
}
//鼠标移动的时候
let mapmove = (e) => {
    if (down.value) {
        left.value += e.movementX / scale.value;
        top.value += e.movementY / scale.value;
    }
    console.log(down.value);
    console.log('移动中');
}
//鼠标松开的时候
let mapup = (e) => {
    down.value = false;
    console.log('松开了');
}

</script>
<style lang="scss">
.con {
    width: 700px;
    height: 500px;
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -50%);
    border: 1px solid #ccc;
    overflow: hidden;

    .box {
        width: 250px;
        height: 250px;
        border: 1px solid #ccc;
        background-color: plum;

        img {
            width: 250px;
            height: 250px;
        }
    }
}
</style>
```



## 路由跳转完后让组件有过渡动画的效果

```
<div class="tab_con" :class="className">
// 内容

</div>





const className = ref('') // 用来存放新的类名
onMounted(() => {
    className.value = 'my-class'//组件加载完成后给他加一个新的类名
}




// 老类名
.tab_con {
	opacity: 0;
    transition: 1s;
    position: relative;
    left: -1000px;
}

// 新类名
.my-class {
    opacity: 1;
    transition: 1s;
    position: relative;
    left: 0px;
}
```

