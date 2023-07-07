<template>
  <!-- <button class="delete" @click="deleteEntity">删除实体</button> -->
  <!-- <button @click="deleteEntity">删除红点</button> -->
  <div id="cesiumContainer">

  </div>
</template>

<script setup>
import * as Cesium from 'cesium'
import { onMounted, ref } from 'vue'
const deleteEntity = ref(null)
let redList = []
onMounted(() => {
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNThkODlmMy03NGZlLTQ1NDUtYTE4My0wZjVkMDI1ZTUzY2IiLCJpZCI6MTUyMDgxLCJpYXQiOjE2ODg2OTI1Nzd9.EpYO589GwERntjrAEa8W3KBo6NOeGgXnQ3_0Kg8EHpo'
  // viewer是所有API的开始
  const viewer = new Cesium.Viewer('cesiumContainer', {
    infoBox: false,  //  关闭点击要素之后的弹框
    selectionIndicator: false,  //  关闭点击要素之后的高亮
  })

  let lon, lat, num = 0
  const line = viewer.entities.add({
    // callbackProperty 生成一个回调函数, 该回调函数会在每一帧都执行, 生成一个动态的实体
    polyline: {
      positions: new Cesium.CallbackProperty(() => {
        num += 0.002
        lon = 120 + num
        lat = 30 + num
        if (lon < 121) {
          return Cesium.Cartesian3.fromDegreesArray([120, 30, lon, lat])
        } else {
          line.polyline.positions = new Cesium.Cartesian3.fromDegreesArray([
            120, 30, 121, 31,
          ]);
        }
      }, false),  //  false表示只执行一次, 必须要有
      material: Cesium.Color.YELLOW,
      width: 5
    }
  })
  let position = Cesium.Cartesian3.fromDegrees(120, 30, 1000000)
  viewer.camera.setView({
    destination: position
  })

})
</script>

<style lang="scss" scoped>
.delete {
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