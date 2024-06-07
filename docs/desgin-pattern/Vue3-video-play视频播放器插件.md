# Vue3-video-play视频播放器插件

## 1.下载插件   

```
npm install vue3-video-play和npm install -D less
```

## 2.在main.js里面引入并全局注册(vue3+vite)

```
import { videoPlay } from "vue3-video-play/lib/index";
import "vue3-video-play/dist/style.css";



app.use(videoPlay);
```

## 3.在要使用的播放器的页面直接使用

```vue
<vue3VideoPlay width="100%" height="100%" title="钢铁侠" :src="options.src" :poster="options.poster" @play="onPlay" @pause="onPause" @timeupdate="onTimeupdate" @canplay="onCanplay" />
<!-- 
<vue3VideoPlay width="100%" height="100%" title="冰河世纪" :src="options.src" :type="options.type" :autoPlay="false" />
-->

<script setup>
import { reactive } from 'vue';
import man from "../../../assets/man.jpg"

const options = reactive({
    src: "https://cdn.jsdelivr.net/gh/xdlumia/files/video-play/IronMan.mp4", //视频源
    poster: man, //视频封面图片
})

// const options = reactive({
//     src: "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8", //视频源
//     type: 'm3u8', //视频类型
// })

const onPlay = (ev) => {
    console.log('播放了')
}
const onPause = (ev) => {
    console.log(ev, '暂停了')
}
const onTimeupdate = (ev) => {
    console.log(ev, '时间更新了')
}
const onCanplay = (ev) => {
    console.log(ev, '可以播放了')
}

</script>
```





文档参考地址：[项目概览 - vue3-video-play - GitCode](https://gitcode.com/xdlumia/vue3-video-play/overview?utm_source=csdn_github_accelerator&isLogin=1)