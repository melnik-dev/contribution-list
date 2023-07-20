<template>
<div class="diagram__item"  v-if="diagramSquares">
  <ContributionDiagramSquare
      v-for="(item, i) in diagramSquares"
      :key="i"
      @click="decrementCount(item.id)"
      :color="item.color" />
</div>
</template>

<script>
import ContributionDiagramSquare from './ContributionDiagramSquare.vue'
export default {
  name: "ContributionDiagramMixed",
  components: {
    ContributionDiagramSquare
  },
  props: ['items'],
  emits: ['decrementCount'],
  data() {
    return {
      diagramSquares: []
    }
  },
  methods: {
    buildDiagram() {
      this.diagramSquares = []
      this.items.forEach(elm => {
        if(elm.checked) {
          for (let i = 0; i < elm.count; i++) {
            this.diagramSquares.push({color: elm.color, id: elm.id})
          }
        }
      })
      this.diagramSquares.sort(() => Math.random() - 0.5)
    },
    decrementCount(itemId) {
      this.$emit('decrementCount', itemId);
    }
  },
  watch: {
    items: {
      handler() {
        this.buildDiagram();
      },
      deep: true
    }
  },
  mounted() {
    this.buildDiagram()
  }
}
</script>

<style scoped>
.diagram__item {
  display: flex;
  flex-wrap: wrap;
}
</style>