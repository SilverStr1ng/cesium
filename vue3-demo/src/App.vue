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

  // 官网内的资源
  // const tileset = viewer.scene.primitives.add(
  //   new Cesium.Cesium3DTileset({
  //     url: Cesium.IonResource.fromAssetId(69380)
  //   })
  // )

  // 静态资源
  const tileset = viewer.scene.primitives.add(
    new Cesium.Cesium3DTileset({
      url: Cesium.IonResource.fromAssetId(75343)
    })
  )
  viewer.flyTo(tileset)

  // 添加点击事件
  handler = new Cesium.ScreenSpaceEventHandler(viewer.scene.canvas)

  let lastPick;
  handler.setInputAction((event) => {
    // 拾取模型
    const pick = viewer.scene.pick(event.endPosition);
    if (pick) {
      if (lastPick) {
        lastPick.color = Cesium.Color.WHITE
      }
      pick.color = Cesium.Color.ORANGERED;
      lastPick = pick;
    }
  }, Cesium.ScreenSpaceEventType.MOUSE_MOVE)

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