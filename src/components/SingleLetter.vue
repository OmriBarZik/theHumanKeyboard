<script>
import { ref } from "vue";
import theHumanKeyboard from "../assets/theHumanKeyboard.jpeg";
export default {
  mounted() {
    const ctx = this.letterCanvas.getContext("2d");

    ctx.drawImage(this.img, 0, 0);
  },
  data() {
    const img = ref(document.createElement("img"));
    img.value.src = theHumanKeyboard;

    return {
      /** @type {import("vue").Ref<HTMLCanvasElement>} */
      letterCanvas: ref(null),
      img,
    };
  },
};
</script>

<template>
  <canvas ref="letterCanvas"></canvas>
</template>
