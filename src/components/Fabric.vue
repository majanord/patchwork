<template>
    <canvas id="canvas" width="300" height="300" ref="canvasel"></canvas>

</template>
<script>
import { konva } from 'konva';

export default {
  name: 'fabricCanvas',
  props: {
    msg: String,
  },
  data() {
    return {
    };
  },
  mounted() {
    // const ref = this.$refs.canvasel;
    // // const canvas = new konva.Canvas(ref);

    // const triang = new fabric.Triangle({
    //   top: 0,
    //   left: 0,
    //   width: 200,
    //   height: 100,
    //   fill: 'red',
    //   rotatingPointOffset: 45,
    // });
    // canvas.add(triang);
  },
};
</script>
