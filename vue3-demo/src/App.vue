<template>
  <div id="cesiumContainer">

  </div>
</template>

<script setup>
import * as Cesium from 'cesium'
import { onMounted } from 'vue'
onMounted(() => {
  Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNThkODlmMy03NGZlLTQ1NDUtYTE4My0wZjVkMDI1ZTUzY2IiLCJpZCI6MTUyMDgxLCJpYXQiOjE2ODg2OTI1Nzd9.EpYO589GwERntjrAEa8W3KBo6NOeGgXnQ3_0Kg8EHpo'
  const esri = new Cesium.ArcGisMapServerImageryProvider({
    url: "https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer",
    enablePickFeatures: false,
  });
  // Viewer是一切API的开始
  let viewer = new Cesium.Viewer('cesiumContainer', {
    imageryProvider: esri,   //默认的谷歌地图影像  影像图层 ImageryLayer

    //地形图层TerrainProvider
    terrainProvider: Cesium.createWorldTerrain({  //  地形图层
      // requestWaterMask: true //水面特效
    }),
  })
})
</script>

<style lang="scss" scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>