<template>
  <div class="star-map">
    <canvas id="star-map-canvas" width="800" height="600"></canvas>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { random } from 'lodash';

export default {
  data() {
    return {
      canvas: {},
      canvasContext: {}
    }
  },
  setup() {
    const starCount = ref(1000); // количество звёзд
    const starRadiusMin = ref(1); // минимальный радиус звезды
    const starRadiusMax = ref(5); // максимальный радиус звезды
    const starColorMin = ref(0); // минимальный цвет звезды (0-255)
    const starColorMax = ref(255); // максимальный цвет звезды (0-255)
    const starBrightnessMin = ref(0.1); // минимальная яркость звезды
    const starBrightnessMax = ref(1); // максимальная яркость звезды
    function generateStars() {

      this.canvasContext.clearRect(0, 0, this.canvas.width, this.canvas.height);

      for (let i = 0; i < starCount.value; i++) {
        const starRadius = random(starRadiusMin.value, starRadiusMax.value);
        const starColor = `rgb(${random(starColorMin.value, starColorMax.value)}, ${random(starColorMin.value, starColorMax.value)}, ${random(starColorMin.value, starColorMax.value)})`;
        const starBrightness = random(starBrightnessMin.value, starBrightnessMax.value);

        const starX = random(0, this.canvas.width);
        const starY = random(0,this. canvas.height);

        this.canvasContext.beginPath();
        this.canvasContext.arc(starX, starY, starRadius, 0, 2 * Math.PI);
        this.canvasContext.fillStyle = starColor;
        this.canvasContext.globalAlpha = starBrightness;
        this.canvasContext.fill();
      }
    }

    return {
      starCount,
      starRadiusMin,
      starRadiusMax,
      starColorMin,
      starColorMax,
      starBrightnessMin,
      starBrightnessMax,
      generateStars,
    };


  },
  methods: {

  },
  mounted() {
    this.canvas = document.getElementById('star-map-canvas');
    this.canvasContext = this.canvas.getContext('2d');

    this.generateStars();

  },

};
</script>

<style lang="scss">
.star-map {
  width: 800px;
  height: 600px;
  border: 1px solid black;
}

#star-map-canvas {
  border: none;
}
</style>
