<template>
  <div class="app">
        <tresjs/>

  </div>

</template>

<script>
import tresjs from "@/views/tresjs.vue";
import starMap2d from "@/views/starMap2d.vue";
import stars from "@/views/stars.vue";

export default {
  components: {tresjs, starMap2d, stars},
  props: [],
  data() {
    return {
    }
  },
  computed: {},
  methods: {},
}
</script>

<style lang="scss">
.app {
  width: 90dvw;
  height: 80dvh;

  .user-el-tabs {
    width: 100%;
    height: auto;
  }
  .stars {
    width: 100dvw;
    height: 80dvh;
  }
}
</style>
