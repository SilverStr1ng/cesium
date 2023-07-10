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
  const position = Cesium.Cartesian3.fromDegrees(114.30, 30.50);

  const orientation = Cesium.Transforms.headingPitchRollQuaternion(
    position,
    new Cesium.HeadingPitchRoll.fromDegrees(90, 0, 0)
  );

  const entities = viewer.entities.add({
    position,
    orientation,
    model: {
      uri: '../src/assets/Cesium_Air.glb',
      minimumPixelSize: 20,  //  模型的最小像素大小
    }
  })
  viewer.scene.primitives.add(new Cesium.ParticleSystem({
    image: '/src/assets/fire.png',
    imageSize: new Cesium.Cartesian2(20, 20), //尺寸
    startScale: 1.0, //初始大小
    endScale: 4.0, //最后大小 
    particleLife: 3.0, ////设置每一个粒子存在的时间
    speed: 5.0, //发射粒子的速度
    emitter: new Cesium.CircleEmitter(2),  //设置发射器(圆形发射器) 
    // emitter: new Cesium.BoxEmitter(new Cesium.Cartesian3(10, 10, 10)),
    emissionRate: 5,//例子发射数量
    modelMatrix: entities.computeModelMatrix(
      viewer.clock.startTime,  //时间控件中的起始时间
      new Cesium.Matrix4()  //4*4矩阵数据
    ),  //设置位置
    lifetime: 16, //生命期属性为所需的持续时间
    // loop: false,  //只循环一次
  }));

  viewer.flyTo(entities)

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