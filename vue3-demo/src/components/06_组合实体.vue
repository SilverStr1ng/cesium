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
  const viewer = new Cesium.Viewer('cesiumContainer', {
    infoBox: false,  //  关闭点击要素之后的弹框
    selectionIndicator: false,  //  关闭点击要素之后的高亮
  })

  // const billboard = viewer.entities.add({
  //   position: Cesium.Cartesian3.fromDegrees(110, 30, 100),
  //   billboard: {
  //     image: '../src/assets/position.png',
  //     scale: 0.3,
  //     color: Cesium.Color.RED,
  //   }
  // })

  // const line = viewer.entities.add({
  //   polyline: {
  //     positions: Cesium.Cartesian3.fromDegreesArrayHeights([
  //       110, 30, 0,
  //       110, 30, 100,
  //     ]),
  //     width: 2,
  //     material: Cesium.Color.GREEN,
  //   }
  // })

  // const label = viewer.entities.add({
  //   position: Cesium.Cartesian3.fromDegrees(110, 30, 100),
  //   label: {
  //     text: '某某小区',
  //     font: '20px sans-serif',
  //     fillColor: Cesium.Color.WHITE,
  //     pixelOffset: new Cesium.Cartesian2(0, -40),
  //   },
  // })

  const entity = viewer.entities.add({
    // 组合
    position: Cesium.Cartesian3.fromDegrees(110, 30, 100),
    billboard: {
      image: '../src/assets/position.png',
      scale: 0.3,
      color: Cesium.Color.RED,
    },
    polyline: {
      positions: Cesium.Cartesian3.fromDegreesArrayHeights([
        110, 30, 0,
        110, 30, 100,
      ]),
      width: 2,
      material: Cesium.Color.GREEN,
    },
    position: Cesium.Cartesian3.fromDegrees(110, 30, 100),
    label: {
      text: '某某小区',
      font: '20px sans-serif',
      fillColor: Cesium.Color.WHITE,
      pixelOffset: new Cesium.Cartesian2(0, -40),
    },
  })

  viewer.zoomTo(entity)

})
</script>

<style lang="scss" scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>