# 纯前端通过SheetJs插件生成EXCEL文件

1.下载SheetJs插件

npm install xlsx --save

2.引入插件

import XLSX from 'xlsx';

3.自定义EXCEL文件的表头和表体数据

```js
// 我们把它放在一个函数当中

let excel=()=>{

console.log(data1.value);// 数据源
let tabdata1 = JSON.parse(JSON.stringify(data1.value))
let chu = []
// 自定义EXCEL表的表体数据  对数据源进行处理，并放入新的数组中，使其变成二维数组的形式
tabdata1.forEach((item, index) => {
    chu.push([`${index + 1}`, item.Date, item.Worktime, '', '', '', '', '', item.hejiCount])
    if (item.children.length > 0) {
        item.children.forEach((items, idx) => {
            chu.push([index + 1 + '.' + (idx + 1), '', '', items.zhiId, items.Machine, items.Type, items.Count, items.Remark, ''])
        })
    }
})
console.log(chu);
// chu是我们处理好的EXCEL文件数据，一般是一个二维数组的形式,形如[['班级'，'性别','爱好'],['8.1班'，'男','游泳'],['8.6'，'女','画画']]
// 第一个是EXCEL表第一行的表头，剩下的按照顺序是EXCEL表的表体数据   
chu.unshift(['序号', '日期', '工时', '制工单号', '机型', '型号', '数量', '备注', '合计数量'])//EXCEL表第一行的表头
const workbook = XLSX.utils.book_new();
const worksheet = XLSX.utils.aoa_to_sheet(chu);
XLSX.utils.book_append_sheet(workbook, worksheet, 'Sheet1');
XLSX.writeFile(workbook, 'example.xlsx');

}


```



# vue3纯前端导出Excel表格

1.下载插件vue-json-excel

```vue
npm install vue-json-excel3
```

2.在main.js中全局引入

```js
import { createApp } from 'vue'
const app = createApp({})
import JsonExcel from "vue-json-excel3";
app.component("downloadExcel", JsonExcel);
```

3.使用

```vue
<download-excel :data="excelpage" :fields="json_fields" name="filename.xls">
    <el-button type="primary">下载excel</el-button>
</download-excel>


<script setup>
import { ref } from 'vue'
// 下载excel的相关数据    导出excel的表格数据
let excelpage = ref([
  {
    student_id: '1',
    student_name: '张三',
    student_majorclass: '计算机科学与技术1班',
    student_score: 90,
    specialty: '编程语言',
  },
  {
    student_id: '2',
    student_name: '李四',
    student_majorclass: '计算机科学与技术5班',
    student_score: 20,
    specialty: '数据库系统',
  }
])  
// 定义导出的表头
let json_fields = ref({
  学号: "student_id",    //常规字段
  姓名: "student_name", //支持嵌套属性
  专业班级: "student_majorclass",
  成绩: "student_score",
  特长: "specialty",
})

</script>
```



# Moment.js是一个处理日期的插件

```js
// 安装插件  npm install moment

// 引入插件   import moment from 'moment';

//使用插件    item是标准时间

const dateObj = moment(item, 'YYYY-MM-DD'); // 将日期字符串转换为 Moment.js 对象
console.log(dateObj.format('YYYY-MM-DD')); // 格式化输出日期

```





# vue3进度条加载插件

```js
//首先下载插件    npm install nprogress --save

//在路由表中引入插件和样式
// 进入条插件
import NProgress from "nprogress";
import "nprogress/nprogress.css";

//通过路由守卫在页面加载之前显示进度条，页面加载完成之后，隐藏进度条
router.beforeEach((to, from, next) => {
  NProgress.start(); // 开始加载进度条
  next();
});

router.afterEach(() => {
  NProgress.done(); // 完成加载进度条
});




//如果要修改进度条的颜色，可以在node_modules/nprogress/nprogress.css里面修改

```



# 实现电脑打印功能

```js
let printContent = `
<!DOCTYPE html>
<html>
<head>
    <title>打印页面</title>
</head>
<style>

img{ max-width: 100%; max-height: 1000px;}
</style>
<body>
    <div id="dayintu">
        ${fujianid.value.map(item => `
      <img src="https://www.jiaofangbao.com/api/下载邮寄附件?id=${item}&apikey=a653602d4443410f88139b063b09dd23" alt="" id="yintu">
        `).join('')}
    </div>
</body>
</html>
`;


    let printWindow = window.open("", "_blank"); // 打开一个新窗口
    printWindow.document.write(printContent); // 在新窗口中写入只包含图片的页面
    printWindow.document.close(); // 关闭写入流

    printWindow.onload = function () {
        printWindow.print(); // 在新窗口中打印页面
    };
```



## 在线预览PPT WORD EXCEL文件

```vue
<!-- https://view.officeapps.live.com/op/view.aspx?src=下载链接      实现ppt  word  excel在线预览 -->
// 因为浏览器默认只支持PDF，不支持其他格式的预览
<iframe src="https://view.officeapps.live.com/op/view.aspx?src=https://burnham.cdkm.com/convert/file/st3p9ugq76afqrt46k6xe5k8pcqytw0w/ppt.ppt" frameborder='no' allowtransparency='yes' width="100%" height="600">
</iframe>
```

