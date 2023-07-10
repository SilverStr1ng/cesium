<template>
  <!-- <button class="delete" @click="deleteEntity">删除实体</button> -->
  <button @click="deleteEntity">删除</button>
  <div id="cesiumContainer">

  </div>
</template>

<script setup>
import * as Cesium from 'cesium'
import { onMounted, ref } from 'vue'
let data, handler, pointList = [];
const deleteEntity = () => {
  handler.removeInputAction(Cesium.ScreenSpaceEventType.LEFT_CLICK)
}
onMounted(() => {
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNThkODlmMy03NGZlLTQ1NDUtYTE4My0wZjVkMDI1ZTUzY2IiLCJpZCI6MTUyMDgxLCJpYXQiOjE2ODg2OTI1Nzd9.EpYO589GwERntjrAEa8W3KBo6NOeGgXnQ3_0Kg8EHpo'
  // viewer是所有API的开始
  const viewer = new Cesium.Viewer('cesiumContainer', {
    shouldAnimate: true,  //  是否开启动画
  })
  const position = Cesium.Cartesian3.fromDegrees(114.30, 30.50);

  const orientation = Cesium.Transforms.headingPitchRollQuaternion(
    position,
    new Cesium.HeadingPitchRoll.fromDegrees(90, 0, 0)
  );

  const entities = viewer.entities.add({
    position,
    orientation,
    model: {
      uri: '../src/assets/Cesium_Air.glb',
      minimumPixelSize: 20,  //  模型的最小像素大小
    }
  })

  viewer.flyTo(entities)

})
</script>

<style lang="scss" scoped>
button {
  position: fixed;
  top: 10px;
  z-index: 50;
}

#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>