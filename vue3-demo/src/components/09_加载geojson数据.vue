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

    // const linestring1 = turf.lineString([[-24, 63], [-23, 60], [-25, 65], [-20, 69]]);
    // console.log(linestring1)
    // // 把geoJson对象转换成了实体entity
    // const data = Cesium.GeoJsonDataSource.load(linestring1)
    // data.then(res => {
    //   viewer.entities.add(res.entities.values[0])
    //   viewer.zoomTo(res.entities.values[0])
    // })


    // const multiLine = turf.multiLineString([[[8, 8], [10, 10]], [[1, 1], [5, 5]]]);
    // Cesium.GeoJsonDataSource.load(multiLine).then(res => {
    //   data = res
    //   viewer.dataSources.add(data);
    //   viewer.zoomTo(data);
    // })

    // deleteEntity.value = () => {
    //   viewer.dataSources.remove(data)
    // }

    // 生成多边形
    // const polygon = turf.polygon([[
    //   [121, 30],
    //   [121.5, 30],
    //   [121.5, 30.5],
    //   [121, 30.5],
    //   [121, 30]
    // ]]);
    // Cesium.GeoJsonDataSource.load(polygon).then(res => {
    //   data = res
    //   viewer.dataSources.add(data);
    //   viewer.zoomTo(data);
    // })

    // 加载topojson
    // const topojson = Cesium.GeoJsonDataSource.load('../src/assets/usa.topojson')
    // topojson.then(res => {
    //   data = res
    //   viewer.dataSources.add(data);
    //   viewer.zoomTo(data);
    // })

    // 加载kml数据
    // const promise = Cesium.KmlDataSource.load('/src/assets/gdp.kmz')
    // console.log(promise)
    // viewer.dataSources.add(promise)

    data = Cesium.CzmlDataSource.load('../src/assets/vehicle.czml')
    data.then(res => {
        viewer.dataSources.add(res);
        let entity = res.entities.getById("Vehicle")
        viewer.trackedEntity = entity;  //trackedEntity 可以实现一直移动相机跟踪entity目标
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