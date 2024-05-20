<template>
  <div class="app">
    <el-tabs type="border-card" class="user-el-tabs">
      <el-tab-pane label="Tres.js">
        <tresjs/>
      </el-tab-pane>
      <el-tab-pane label="stars 2d">
        <starMap2d/>
      </el-tab-pane>
      <el-tab-pane label="stars">

        <div class="stars">
          <stars/>
        </div>
      </el-tab-pane>
    </el-tabs>
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
  width: 100dvw;
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
