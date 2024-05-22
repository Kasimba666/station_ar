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
          ref="asteroidRef"
          v-for="item in asteroidsRef"
          :args="[item['radius'], 0]"
          :position="[item['position']['x'], item['position']['y'], item['position']['z']]"
      />


      <TresMesh
          @click="onClick"
          :position="[0.38, 0.24, 0,38]"
      >
        <TresBoxGeometry
            :args="[0.06, button1Height, 0.06]"
        />
        <TresMeshToonMaterial color="#0700ef"/>
      </TresMesh>

      <OrbitControls />
      <TresGridHelper :args="[4, 4]" />
      <Suspense>
        <GLTFModel
            ref="modelStationRef"
            path="/src/data/station_ar.glb"
            draco
        />
      </Suspense>
      <Suspense>
        <GLTFModel
            ref="modelAibashRef"
            path="/src/data/aibash.glb"
            :position="[-1, -0.1, -1]"
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
    </TresCanvas>
  </div>

</template>

<script>
import {TresCanvas, useRenderLoop } from '@tresjs/core';
import {OrbitControls, GLTFModel, Icosahedron, Stars} from '@tresjs/cientos';
import {shallowRef, reactive} from 'vue';

export default {
  components: {TresCanvas, OrbitControls, GLTFModel, Icosahedron, Stars},
  data() {
    return {
      asteroidsPositions: [],
    }
  },
  setup() {
    const { onLoop } = useRenderLoop();
    const cameraRef = shallowRef();
    const modelStationRef = shallowRef();
    const modelAibashRef = shallowRef();
    const xRotation = shallowRef(0);
    const yRotation = shallowRef(0);
    const zRotation = shallowRef(0);

    const radius = shallowRef(0);


    const button1Height = shallowRef();
    const asteroidsAmount = shallowRef(20);

    const asteroidsQs = [];
    const asteroidsRef = reactive([]);

    return {
      cameraRef,
      modelStationRef: modelStationRef,
      modelAibashRef: modelAibashRef,
      asteroidsRef,
      radius,
      onLoop,
      xRotation,
      yRotation,
      zRotation,

      button1Height,
      asteroidsAmount,
      asteroidsQs
    }
  },
  methods: {
    init() {
      const pi = Math.PI;
      for (let i = 0; i < this.asteroidsAmount; i++)  {
        this.asteroidsQs.push(
            {position: {
                x: {
                  qAngleSpeed: Math.random() ,
                  qAngleShift: Math.random() * 2 * pi,
                  qScale: Math.random() * 3,
                  qShift: 0
                },
                y: {
                  qAngleSpeed: Math.random() ,
                  qAngleShift: Math.random() * 2 * pi,
                  qScale: Math.random() * 3,
                  qShift: 0
                },
                z: {
                  qAngleSpeed: Math.random() ,
                  qAngleShift: Math.random() * 2 * pi,
                  qScale: Math.random() * 3,
                  qShift: 0
                }
              },
            radius: 0.1 * Math.random()
            }
        );
      }
    },
    onClick(e) {
      this.button1Height = 0.02;
      console.log(this.button1Height);
      let buttonTimeOut = setTimeout(()=>{
        this.button1Height = 0.05;
        clearTimeout(buttonTimeOut);
        console.log(this.button1Height);
      }, 200);
    },
    onPointerEnter(e) {
      console.log(e);
    },
    onPointerLeave(e) {
      console.log(e);
    },
  },
  mounted() {
    this.init();
    const pi = Math.PI;
    this.button1Height = 0.05;
    this.onLoop(({delta, elapsed})=> {
      // if (!this.modelStationRef) return;
      this.asteroidsRef=[];
      this.asteroidsQs.forEach((v)=>{
        this.asteroidsRef.push(
            {position:
              {
                x: Math.sin(v.position.x.qAngleSpeed * elapsed + v.position.x.qAngleShift) * v.position.x.qScale + v.position.x.qShift,
                y: Math.sin(v.position.y.qAngleSpeed * elapsed + v.position.y.qAngleShift) * v.position.y.qScale + v.position.y.qShift,
                z: Math.cos(v.position.z.qAngleSpeed * elapsed + v.position.z.qAngleShift) * v.position.z.qScale + v.position.z.qShift
              },
              radius: v.radius
            })
      });
      this.xRotation += 0.2 * delta;
      this.yRotation += 0.03 * delta;
      this.zRotation += 0.04 * delta;

    });
  },
}
</script>

<style lang="scss">

.tres {
  width: 90dvw;
  height: 80dvh;
}

</style>
