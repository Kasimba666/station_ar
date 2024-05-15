<template>
  <div class="t-canvas">
    <TresCanvas
        preset="realistic"
        clear-color="#d9d9d9"
    >
<!--        shadows-->
<!--        alpha-->
      <TresPerspectiveCamera
          ref="cameraRef"
          :fov="50"
      />
      <OrbitControls />
      <TresGridHelper :args="[4, 4]" />
      <Suspense>
        <Model ref="modelRef"/>
      </Suspense>
      <TresDirectionalLight :position="[2, 4, 2]" :intensity="0.9" cast-shadow />
      <TresAmbientLight :color="0xffffff" :intensity="0.7" />
    </TresCanvas>

  </div>
</template>

<script setup lang="ts">

import Model from '/src/components/model.vue';
import {TresCanvas, useRenderLoop } from '@tresjs/core';
import {OrbitControls, GLTFModel} from '@tresjs/cientos';
import {shallowRef} from 'vue';

// import { useLoader } from '@tresjs/core'
// import { GLTFLoader } from 'three/addons/loaders/GLTFLoader'
// // import {useTweakPane} from '@tresjs/cientos';

//
const { onLoop } = useRenderLoop();
const cameraRef = shallowRef();
const modelRef = shallowRef();


onLoop(({delta, elapsed})=> {
  if (!modelRef.value) return;
  // cameraRef.value.position.lookAt([0, 1, 0]);
  cameraRef.value.position.y = 4;
  // cameraRef.value.lookAt([0, 0, 0]);
  cameraRef.value.position.x = Math.sin(elapsed/10)*2;
  cameraRef.value.position.z = Math.cos(elapsed/10)*2;
  // modelRef.value.rotation.x += delta/2;
  // modelRef.value.rotation.z = elapsed;


});

// });

</script>

<style scoped>
.t-canvas {
  height: 80dvw;
  width: 100dvh;
  margin: 5px;
  padding: 5px;
}
</style>
