<template>
  <!-- <button class="delete" @click="deleteEntity">删除实体</button> -->
  <button @click="deleteEntity">删除</button>
  <div id="cesiumContainer">

  </div>
</template>

<script setup>
import * as Cesium from 'cesium'
import { onMounted, ref } from 'vue'
let data, viewer;
const deleteEntity = () => {
  viewer.dataSources.remove(data)
}
onMounted(() => {
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNThkODlmMy03NGZlLTQ1NDUtYTE4My0wZjVkMDI1ZTUzY2IiLCJpZCI6MTUyMDgxLCJpYXQiOjE2ODg2OTI1Nzd9.EpYO589GwERntjrAEa8W3KBo6NOeGgXnQ3_0Kg8EHpo'
  // viewer是所有API的开始
  viewer = new Cesium.Viewer('cesiumContainer', {
    shouldAnimate: true,  //  是否开启动画
  })

  // 导入geojson数据
  Cesium.GeoJsonDataSource.load('../src/assets/camera.json').then(res => {
    data = res
    // 替换billboard的图片， 遍历
    res.entities.values.forEach(item => {
      // 聚合
      res.clustering.enabled = true
      // 聚合距离
      res.clustering.pixelRange = 30
      // 聚合最小像素
      res.clustering.minimumClusterSize = 3
      // 聚合事件
      res.clustering.clusterEvent.addEventListener((clusteredEntities, cluster) => {
        cluster.billboard.show = true
        cluster.label.show = false
        cluster.billboard.scale = 1.2
        if(clusteredEntities.length >= 300) {
          cluster.billboard.image = pin300
        } else if(clusteredEntities.length >= 100) {
          cluster.billboard.image = pin100
        } else if(clusteredEntities.length >= 50) {
          cluster.billboard.image = pin50
        } else if(clusteredEntities.length >= 30) {
          cluster.billboard.image = pin30
        } else if(clusteredEntities.length >= 10) {
          cluster.billboard.image = pin10
        }
      })
      item.billboard.image = '../src/assets/camera.png'
      // 图片样式
      item.billboard.scale = 0.1
    })
    viewer.dataSources.add(res)
    viewer.flyTo(res)
  })
  const pinBuilder = new Cesium.PinBuilder();
  const pin300 = pinBuilder
    .fromText("300+", Cesium.Color.RED, 48)
    .toDataURL();
  const pin100 = pinBuilder
    .fromText("100+", Cesium.Color.ORANGE, 48)
    .toDataURL();
  const pin50 = pinBuilder
    .fromText("50+", Cesium.Color.YELLOW, 48)
    .toDataURL();
  const pin30 = pinBuilder
    .fromText("30+", Cesium.Color.GREEN, 48)
    .toDataURL();
  const pin10 = pinBuilder
    .fromText("10+", Cesium.Color.BLUE, 48)
    .toDataURL();

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