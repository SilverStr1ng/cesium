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

  // 实体 entity
  // 写法1
  // 声明点
  // const point = new Cesium.Entity({
  //   position: Cesium.Cartesian3.fromDegrees(110, 30),
  //   point: {
  //     pixelSize: 10,
  //     color: Cesium.Color.RED,
  //     outlineColor: Cesium.Color.WHITE,
  //     outlineWidth: 2
  //   }
  // })
  // // 添加点
  // viewer.entities.add(point)


  // 写法2 (推荐)  直接添加
  // const point = viewer.entities.add({
  //   id: 'point',
  //   position: Cesium.Cartesian3.fromDegrees(121, 30),
  //   point: {
  //     pixelSize: 20,
  //     color: Cesium.Color.RED,
  //     outlineColor: Cesium.Color.WHITE,
  //     outlineWidth: 2
  //   }
  // })
  // viewer.zoomTo(point)

  // billboard
  //   const billboard = viewer.entities.add({
  //     position: Cesium.Cartesian3.fromDegrees(110, 30, 10),
  //     billboard: {
  //       image: '../src/assets/position.png',
  //       scale: 0.5,
  //       color: Cesium.Color.RED,
  //     }
  //   })
  //   viewer.zoomTo(billboard)

  // 文字
  // const label = viewer.entities.add({
  //   position: Cesium.Cartesian3.fromDegrees(110, 30, 10),
  //   label: {
  //     text: 'Cesium',
  //     fillColor: Cesium.Color.WHITE,
  //     showBackground: true,
  //     backgroundColor: new Cesium.Color(255,255,0),
  //   }
  // })
  // viewer.zoomTo(label)

  // 线
  // const polyline = viewer.entities.add({
  //   polyline: {
  //     positions: Cesium.Cartesian3.fromDegreesArray([
  //       110, 30,
  //       110, 31,
  //       111, 31,
  //       111, 30,
  //       110, 30
  //     ]),
  //     width: 5,
  //     material: Cesium.Color.RED
  //   }
  // })
  // viewer.zoomTo(polyline)

  // 多边形
  // const polygon = viewer.entities.add({
  //   polygon: {
  //     hierarchy: {
  //       positions: Cesium.Cartesian3.fromDegreesArray([110, 30,
  //         110, 31,
  //         111, 31,
  //         111, 30,
  //         110, 30]),
  //     },
  //     material: Cesium.Color.RED.withAlpha(0.5),
  //     height: 10000,  //离地面高度
  //     extrudedHeight: 20000,  // 拉伸高度
  //     outline: true, //比较拉伸后使用
  //     outlineColor: Cesium.Color.WHITE,
  //     fill: false, //是否填充
  //   }
  // })
  // viewer.zoomTo(polygon)

  // const box = viewer.entities.add({
  //   position: Cesium.Cartesian3.fromDegrees(110, 30, 10),
  //   box: {
  //     dimensions: new Cesium.Cartesian3(400000, 300000, 500000),  //长宽高
  //     material: Cesium.Color.RED.withAlpha(0.5),
  //     outline: true,
  //     outlineColor: Cesium.Color.WHITE,
  //   }
  // })
  // viewer.zoomTo(box)

  // 椭圆
  // const ellipse = viewer.entities.add({
  //   position: Cesium.Cartesian3.fromDegrees(110, 30, 10),
  //   ellipse: {
  //     semiMinorAxis: 300000,
  //     semiMajorAxis: 400000,
  //     material: Cesium.Color.RED.withAlpha(0.5),
  //     outline: true,
  //     outlineColor: Cesium.Color.WHITE,
  //     extrudedHeight: 200000,
  //     rotation: Cesium.Math.toRadians(45),
  //   }
  // })
  // viewer.zoomTo(ellipse)

  // 矩形
  const rectangle = viewer.entities.add({
    position: Cesium.Cartesian3.fromDegrees(110, 30, 10),
    rectangle: {
      // coordinates: Cesium.Rectangle.fromDegrees(110, 30, 111, 31),
      coordinates: Cesium.Rectangle.fromDegrees(110, 30, 111, 31),
      material: '../src/assets/dog.jpg',
      outline: true,
      outlineColor: Cesium.Color.WHITE,
      extrudedHeight: 200000,
      rotation: Cesium.Math.toRadians(45),
    }
  })
  viewer.zoomTo(rectangle)

})
</script>

<style lang="scss" scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>