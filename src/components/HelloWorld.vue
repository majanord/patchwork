<template>
  <v-stage :config='configKonva'>
    <v-layer>
      <v-circle :config='configCircle'></v-circle>

      <v-shape v-for="(p, i) in pwork" :key="i" :config="p" />
    </v-layer>
  </v-stage>
</template>

<script >

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      configKonva: {
        width: 1000,
        height: 1500,
      },
      configCircle: {
        x: 100,
        y: 100,
        radius: 70,
        fill: 'red',
        stroke: 'black',
        strokeWidth: 4,
      },
      pwork: this.patchwork(),
    };
  },
  methods: {
    patter() {
      const size = 50;
      const squareA = (en) => {
        const a = { x: en.x, y: en.y };
        const b = { x: en.x + size, y: en.y };
        const c = { x: en.x, y: en.y + size };
        const d = { x: en.x + size, y: en.y + size };
        const triA1 = () => ({
          start: a,
          to: b,
          tre: c,
        });

        const triA2 = () => ({
          start: c,
          to: d,
          tre: b,
        });

        return [
          triA1(), triA2(),
        ];
      };

      const squareB = (en) => {
        const a = { x: en.x, y: en.y };
        const b = { x: en.x + size, y: en.y };
        const c = { x: en.x, y: en.y + size };
        const d = { x: en.x + size, y: en.y + size };

        const triB1 = () => ({
          start: a,
          to: b,
          tre: d,
        });

        const triB2 = () => ({
          start: a,
          to: c,
          tre: d,
        });

        return [
          triB1(), triB2(),
        ];
      };

      let pattern = [];

      for (let i = 0; i < 10; i += 1) {
        console.log('row', i);
        for (let j = 0; j < 18; j += 1) {
          console.log('col', j);
          console.log('A', i % 2 !== 0 && j % 2 === 0);
          let check = true;
          if (i % 2 === 0) {
            check = (j % 2 === 0);
          } else {
            check = (j % 2 !== 0);
          }
          if (check) {
            pattern = pattern.concat(squareA({ x: i * size, y: j * size }));
          } else {
            pattern = pattern.concat(squareB({ x: i * size, y: j * size }));
          }
        }
      }
      return pattern;
    },
    triangleConfig(start, to, tre, color) {
      return {
        sceneFunc: (context, shape) => {
          context.beginPath();
          context.moveTo(start.x, start.y);
          context.lineTo(to.x, to.y);
          context.lineTo(tre.x, tre.y);
          context.closePath();

          // special Konva.js method
          context.fillStrokeShape(shape);
        },
        fill: color,
        stroke: color,
        strokeWidth: 1,
      };
    },
    randomColor() {
      const colors = [
        '#C5FA94',
        '#27BD42',
        '#0B9851',
        '#138152',
        '#A1EAE6',
        '#ACD9F0',
        '#56B1E8',
        '#21B9D0',
        '#334C9F',
        '#32405D', '#EAEAEA', '#E6DFCF', '#A5A5A5', '#7F59AC', '#A590B9', '#7A3288', '#FEC5D6', '#F297B8', '#FD7FA4', '#D3316C', '#E0DC71', '#ECBC5A', '#E9A13B', '#F09850', '#ECD468', '#F1613C', '#F0CFAF', '#D6AA83', '#DE4152', '#992E36',
      ];

      return colors[Math.floor(Math.random() * colors.length)];
    },
    patchwork() {
      const patter = this.patter();
      return patter.map((triangle) => {
        const color = this.randomColor();
        const out = this.triangleConfig(triangle.start, triangle.to, triangle.tre, color);
        return out;
      });
    },
  },
};
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped lang='scss'>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
