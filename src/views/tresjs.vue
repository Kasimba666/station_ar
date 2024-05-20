<template>
  <div class="tres">
    <TresCanvas
        clear-color="#000000"
    >
      <TresPerspectiveCamera
          ref="cameraRef"
          preset="realistic"
          :fov="65"
      />
      <Icosahedron
          ref="asteroid1Ref"
          :args="[0.06, 0]"
          :position="[xPosition1, 0.5, zPosition1]"
      />
      <Icosahedron
          ref="asteroid2Ref"
          :args="[0.05, 0]"
          :position="[xPosition2, 1, zPosition2]"
      />
      <Icosahedron
          ref="asteroid3Ref"
          :args="[0.07, 0]"
          :position="[xPosition3, 1.5, zPosition3]"
      />
      <Icosahedron
          ref="asteroid4Ref"
          :args="[0.05, 0]"
          :position="[xPosition4, 2, zPosition4]"
      />
<!--          :rotation="[0, yRotation, 0]"-->
      <OrbitControls />
      <TresGridHelper :args="[4, 4]" />
              <Suspense>
                <GLTFModel
                    ref="modelRef"
                    path="/src/data/station_ar.glb"
                    draco
                />
              </Suspense>
      <TresDirectionalLight :position="[2, 4, 2]" :intensity="0.9" cast-shadow />
      <TresAmbientLight :color="0xffffff" :intensity="0.7" />
      <Stars
          :rotation="[0, yRotation, 0]"
          :radius="50"
          :depth="50"
          :count="5000"
          :size="0.3"
          :size-attenuation="true"
      />
      <Stars
          :rotation="[0, yRotation, 0]"
          :radius="100"
          :depth="50"
          :count="5000"
          :size="0.8"
          :size-attenuation="true"
          color="teal"
      />
      <Suspense>
        <Smoke
            :speed="0.8"
            :segments="12"
            color="teal"
        />
      </Suspense>
    </TresCanvas>
  </div>

</template>

<script>
import {TresCanvas, useRenderLoop } from '@tresjs/core';
import {OrbitControls, GLTFModel, Icosahedron, Stars, Smoke} from '@tresjs/cientos';
import {shallowRef} from 'vue';

export default {
  components: {TresCanvas, OrbitControls, GLTFModel, Icosahedron, Stars, Smoke},
  data() {
    return {

    }
  },
  setup() {
    const { onLoop } = useRenderLoop();
    const cameraRef = shallowRef();
    const modelRef = shallowRef();
    const xRotation = shallowRef(0);
    const yRotation = shallowRef(0);
    const zRotation = shallowRef(0);
    const xPosition1 = shallowRef(0);
    const yPosition1 = shallowRef(0);
    const zPosition1 = shallowRef(0);
    const xPosition2 = shallowRef(0);
    const yPosition2 = shallowRef(0);
    const zPosition2 = shallowRef(0);
    const xPosition3 = shallowRef(0);
    const yPosition3 = shallowRef(0);
    const zPosition3 = shallowRef(0);
    const xPosition4 = shallowRef(0);
    const yPosition4 = shallowRef(0);
    const zPosition4 = shallowRef(0);
    const asteroid1Ref = shallowRef();
    const asteroid2Ref = shallowRef();
    const asteroid3Ref = shallowRef();

    return {
      cameraRef,
      modelRef,
      xRotation,
      yRotation,
      zRotation,
      xPosition1,
      yPosition1,
      zPosition1,
      xPosition2,
      yPosition2,
      zPosition2,
      xPosition3,
      yPosition3,
      zPosition3,
      xPosition4,
      yPosition4,
      zPosition4,
      onLoop,
      asteroid1Ref,
      asteroid2Ref,
      asteroid3Ref,
    }
  },
  methods: {
    init() {
    },

  },
  mounted() {
    this.init();
    const pi = Math.PI;
    this.onLoop(({delta, elapsed})=> {
      if (!this.modelRef) return;
      this.xRotation += 0.2 * delta;
      this.yRotation += 0.03 * delta;
      this.zRotation += 0.04 * delta;
      this.xPosition1 = Math.sin(0.8 * elapsed)*1.2;
      this.zPosition1 = Math.cos(0.7 * elapsed)*1.9;
      this.xPosition2 = Math.sin(1 * elapsed + pi/2)*1.7;
      this.zPosition2 = Math.cos(1 * elapsed + pi/2)*1.9;
      this.xPosition3 = Math.sin(0.5 * elapsed + pi*3/2)*1.2;
      this.zPosition3 = Math.cos(0.6 * elapsed + pi*3/2)*2.1;
      this.xPosition4 = Math.sin(0.6 * elapsed + pi)*1.2;
      this.zPosition4 = Math.cos(0.6 * elapsed + pi)*1.9;
      // this.zRotation += 0.04 * delta;
      // this.asteroid1Ref.position
    });
  },
}
</script>

<style lang="scss">

.tres {
  width: 100dvw;
  height: 80dvh;
}

</style>
