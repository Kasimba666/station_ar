<script setup lang="ts">
import { useGLTF, GLTFModel, useTweakPane } from '@tresjs/cientos'

// const modelRef = shallowRef<THREE.Object3D>()
// const { scenes } = await useGLTF('/src/data/station_ar.gltf', { draco: true })
</script>

<template>
<!--  <primitive-->
<!--      :object="scenes"-->
<!--  />-->

  <GLTFModel
      ref="modelRef"
      path="/src/data/station_ar.glb"
      draco
  />
</template>
