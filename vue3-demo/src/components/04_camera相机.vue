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
  const viewer = new Cesium.Viewer('cesiumContainer', {})

  const position = Cesium.Cartesian3.fromDegrees(110, 20, 20000)

  // setView 定义相机目的地, 直接跳转到
  // viewer.camera.setView({
  //   destination: position,
  //   orientation: {
  //     heading: Cesium.Math.toRadians(0),
  //     pitch: Cesium.Math.toRadians(-90),  //  -90 默认  0  平视 
  //     roll: Cesium.Math.toRadians(0)
  //   }
  // })

  // 快速切换视角, 带飞行动画, 可以设置飞行的时长
  viewer.camera.flyTo({
    destination: position,
    duration: 3,  //  单位秒
    orientation: {
      heading: Cesium.Math.toRadians(0),
      pitch: Cesium.Math.toRadians(0),  //  -90 默认  0  平视 
      roll: Cesium.Math.toRadians(0)
    }
  })

  // lookAt  将相机定位到某个位置, 但是不改变相机的高度
  const position2 = Cesium.Cartesian3.fromDegrees(110, 20)
  viewer.camera.lookAt(
    position2,
    new Cesium.HeadingPitchRange(
      Cesium.Math.toRadians(0),
      Cesium.Math.toRadians(-90),  //  -90 默认  0  平视
      20000
    )
  )
})


</script>

<style lang="scss" scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>