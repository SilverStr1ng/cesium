<template>
  <!-- <button class="delete" @click="deleteEntity">删除实体</button> -->
  <button @click="deleteEntity">删除红点</button>
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

  const point = viewer.entities.add({
    id: 'point',
    position: Cesium.Cartesian3.fromDegrees(121, 30),
    point: {
      pixelSize: 20,
      color: Cesium.Color.RED,
      outlineColor: Cesium.Color.WHITE,
      outlineWidth: 2
    }
  })

  const point2 = viewer.entities.add({
    id: 'point2',
    position: Cesium.Cartesian3.fromDegrees(121.30, 30),
    point: {
      pixelSize: 20,
      color: Cesium.Color.RED,
      outlineColor: Cesium.Color.WHITE,
      outlineWidth: 2
    }
  })

  const point3 = viewer.entities.add({
    id: 'point3',
    position: Cesium.Cartesian3.fromDegrees(121.60, 30),
    point: {
      pixelSize: 20,
      color: Cesium.Color.BLUE,
      outlineColor: Cesium.Color.WHITE,
      outlineWidth: 2
    }
  })

  redList.push(point, point2)

  viewer.zoomTo(point)

  // 删除方法(三种方法)
  deleteEntity.value = () => {
    // viewer.entities.removeById('point')
    // viewer.entities.remove(point)
    // viewer.entities.removeAll()
    // 遍历数组删除蓝点
    redList.forEach(item => {
      viewer.entities.remove(item)
    })
    // 清空数组
    redList = []
  }

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