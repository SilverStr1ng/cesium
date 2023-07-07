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
  new Cesium.Viewer('cesiumContainer', {})

  // 返回一个笛卡尔坐标
  const cartesian1 = Cesium.Cartesian3.fromDegrees(114, 30, 30)  //  经度  纬度  高度
  const cartesian2 = Cesium.Cartesian3.fromDegrees(114, 30, 20)  //  经度  纬度  高度

  console.log(cartesian1, cartesian2)

  // 笛卡尔坐标转经纬度  返回一个弧度坐标
  let latLng1 = Cesium.Cartographic.fromCartesian(cartesian1)
  let latLng2 = Cesium.Cartographic.fromCartesian(cartesian2)
  console.log(latLng1, latLng2)

  // 弧度坐标转换为角度坐标, 数学方法
  // const lon = 180 / Math.PI * latLng1.longitude
  // const lat = 180 / Math.PI * latLng1.latitude
  // console.log(lon, lat)

  // 封装方法转换
  let lon = Cesium.Math.toDegrees(latLng1.longitude)
  let lat = Cesium.Math.toDegrees(latLng1.latitude)
  console.log(lon, lat)
})


// 0.1 + 0.2 != 0.3
// js小数位精度问题
</script>

<style lang="scss" scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>