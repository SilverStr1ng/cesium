<template>
  <!-- <button class="delete" @click="deleteEntity">删除实体</button> -->
  <button @click="deleteEntity">删除</button>
  <div id="cesiumContainer">

  </div>
</template>

<script setup>
import * as Cesium from 'cesium'
import { onMounted, ref } from 'vue'
const deleteEntity = ref(null)
let data;
onMounted(() => {
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNThkODlmMy03NGZlLTQ1NDUtYTE4My0wZjVkMDI1ZTUzY2IiLCJpZCI6MTUyMDgxLCJpYXQiOjE2ODg2OTI1Nzd9.EpYO589GwERntjrAEa8W3KBo6NOeGgXnQ3_0Kg8EHpo'
  // viewer是所有API的开始
  const viewer = new Cesium.Viewer('cesiumContainer', {
    infoBox: false,  //  关闭点击要素之后的弹框
    selectionIndicator: false,  //  关闭点击要素之后的高亮
    shouldAnimate: true,  //  是否开启动画
  })

  // entity 基于 primitive 封装
  // 完美的封装了primitive的所有属性, 调用方便
  // primitive 更接近webgl底层, 可以直接操作顶点, 但是调用不方便
  // 可以绘制更高级的图形, 比如点线面
  // 1. Draw a translucent ellipse on the surface with a checkerboard pattern
  // var instance = new Cesium.GeometryInstance({
  //   geometry: new Cesium.EllipseGeometry({
  //     center: Cesium.Cartesian3.fromDegrees(-100.0, 20.0),
  //     semiMinorAxis: 500000.0,
  //     semiMajorAxis: 1000000.0,
  //     rotation: Cesium.Math.PI_OVER_FOUR,
  //     vertexFormat: Cesium.VertexFormat.POSITION_AND_ST
  //   }),
  //   id: 'object returned when this instance is picked and to get/set per-instance attributes'
  // });

  // viewer.scene.primitives.add(new Cesium.Primitive({
  //   geometryInstances: instance,
  //   appearance: new Cesium.EllipsoidSurfaceAppearance({
  //     // material: Cesium.Material.fromType('Grid')  //  样式
  //     material: new Cesium.Material({
  //       fabric: {
  //         type: 'Color',
  //         uniforms: {
  //           color: new Cesium.Color(1.0, 0.0, 0.0, 0.5)
  //         }
  //       }
  //     })
  //   })
  // }));

  // 2. Draw different instances each with a unique color
  var rectangleInstance = new Cesium.GeometryInstance({
    geometry: new Cesium.RectangleGeometry({
      rectangle: Cesium.Rectangle.fromDegrees(-140.0, 30.0, -100.0, 40.0),
      vertexFormat: Cesium.PerInstanceColorAppearance.VERTEX_FORMAT
    }),
    id: 'rectangle',
    attributes: {
      color: new Cesium.ColorGeometryInstanceAttribute(0.0, 1.0, 1.0, 0.5)
    }
  });
  // 创建一个多边形
  // 具体为三角形, 紧邻矩形
  var triangleInstance = new Cesium.GeometryInstance({
    geometry: new Cesium.PolygonGeometry({
      polygonHierarchy: new Cesium.PolygonHierarchy(
        Cesium.Cartesian3.fromDegreesArray([
          -100, 43,
          -90, 35,
          - 100, 27,

        ])
      ),
      vertexFormat: Cesium.PerInstanceColorAppearance.VERTEX_FORMAT
    }),
    id: 'triangle',
    attributes: {
      color: new Cesium.ColorGeometryInstanceAttribute(0.0, 0.0, 1.0, 0.5)
    }
  });
  viewer.scene.primitives.add(new Cesium.Primitive({
    geometryInstances: [rectangleInstance, triangleInstance],
    appearance: new Cesium.PerInstanceColorAppearance()
  }));
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