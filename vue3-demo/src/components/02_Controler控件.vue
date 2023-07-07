<template>
  <div id="cesiumContainer">

  </div>
</template>

<script setup>
import * as Cesium from 'cesium'
import { onMounted } from 'vue'
onMounted(() => {
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNThkODlmMy03NGZlLTQ1NDUtYTE4My0wZjVkMDI1ZTUzY2IiLCJpZCI6MTUyMDgxLCJpYXQiOjE2ODg2OTI1Nzd9.EpYO589GwERntjrAEa8W3KBo6NOeGgXnQ3_0Kg8EHpo'
  // viewer是所有API的开始
  new Cesium.Viewer('cesiumContainer',{
    timeline: false,  //  关闭时间轴控件
    animation: false,  //  动画控件
    geocoder: false,  //  搜索按钮
    homeButton: false, //  主页按钮
    sceneModePicker: false,  // 投影方式按钮
    baseLayerPicker: false,  //  基础图层选择器按钮
    navigationHelpButton: false,  //  帮助手势按钮
    fullscreenButton: false,  //  全屏按钮
  })
})
</script>

<style lang="scss" scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>