<template>
  <div>
    <div class="grid" :style="{ 'grid-template-areas': gridAreas }">
      <div
        v-for="(item, index) in items"
        :key="index"
        class="grid__item"
        :style="{
          'background-color': item.bgColor,
          'grid-area': `a${index}`
        }"
      >
        {{ `a${index}` }}
      </div>
    </div>
    <div><button @click="moarItems">➕ Moar</button></div>
  </div>
</template>

<script>
const layouts = [
  {
    className: "layout-1",
    items: 3,
    template: [[0, 0, 0, 0, 1, 1], [0, 0, 0, 0, 2, 2]]
  },
  { className: "layout-2", items: 3, template: [[0, 0, 1, 1, 2, 2]] },
  { className: "layout-3", items: 1, template: [[0, 0, 0, 0, 0, 0]] },
  {
    className: "layout-4",
    items: 3,
    template: [[1, 1, 0, 0, 0, 0], [2, 2, 0, 0, 0, 0]]
  },
  { className: "layout-5", items: 3, template: [[0, 0, 1, 1, 2, 2]] },
  { className: "layout-6", items: 2, template: [[0, 0, 0, 1, 1, 1]] }
];

export default {
  data() {
    return {
      items: []
    };
  },
  mounted() {
    console.log(
      `🦄🦄`,
      new Array(10).map(i => ({
        bgColor: this.randomColor()
      }))
    );
  },
  computed: {
    gridAreas() {
      let currentLayout = 0;
      let grid = "";
      for (let index = 0; index <= this.items.length; index++) {
        const layout = layouts[currentLayout];
        grid = `
${grid}
/* ${layout.className} */
${layout.template
          .map(line => `"${line.map(e => `a${index + e}`).join(" ")}"`)
          .join("\n")}
`;

        index += layout.items - 1;
        currentLayout++;
        if (currentLayout > layouts.length - 1) currentLayout = 1;
      }
      return grid;
    }
  },
  methods: {
    randomColor() {
      var letters = "0123456789ABCDEF";
      var color = "#";
      for (var i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }
      return color;
    },
    moarItems() {
      this.items = [
        ...this.items,
        ...new Array(10).map(i => ({
          bgColor: this.randomColor()
        }))
      ];
    }
  }
};
</script>

<style>
pre {
  text-align: left;
}
.grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-gap: 1rem;
}
.grid__item {
  color: white;
  font-size: 4rem;
  font-weight: bold;
  text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 10rem;
}
</style>
