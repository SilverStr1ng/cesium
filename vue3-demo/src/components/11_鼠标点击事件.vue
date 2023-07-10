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
    infoBox: false,  //  关闭点击要素之后的弹框
    selectionIndicator: false,  //  关闭点击要素之后的高亮
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
      url: '../src/assets/b3dm/tileset.json'
    })
  )
  viewer.flyTo(tileset)

  const arr = [];

  const polyline = viewer.entities.add({
    polyline: {
      positions: [],
      width: 5,
      material: Cesium.Color.RED
    }
  })

  // 添加点击事件
  handler = new Cesium.ScreenSpaceEventHandler(viewer.scene.canvas)

  handler.setInputAction((event) => {
    //返回一个笛卡尔坐标
    let position = viewer.scene.pickPosition(event.position);
    //如果有这个坐标
    if (Cesium.defined(position)) {
      pointList.push(viewer.entities.add({
        position: position,
        point: {
          color: Cesium.Color.BLUE,
          pixelSize: 20,
        },
      }));
      arr.push(position)
      polyline.polyline.positions = arr
    }
  }, Cesium.ScreenSpaceEventType.LEFT_CLICK);
  handler.setInputAction(() => {
    pointList.forEach(item => {
      viewer.entities.remove(item)
    })
    viewer.entities.add(polyline)
    // 右键结束
    handler.removeInputAction(Cesium.ScreenSpaceEventType.LEFT_CLICK)
    handler.removeInputAction(Cesium.ScreenSpaceEventType.RIGHT_CLICK)
  }, Cesium.ScreenSpaceEventType.RIGHT_CLICK)

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