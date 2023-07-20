<template>
<div class="diagram__item"  v-if="shuffleArray">
  <ContributionDiagramSquare
      v-for="(item, i) in shuffleArray"
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
      shuffleArray: []
    }
  },
  methods: {
    pushSquares() {
      this.shuffleArray = []
      this.items.forEach(elm => {
        if(elm.checked) {
          for (let i = 0; i < elm.count; i++) {
            this.shuffleArray.push({color: elm.color, id: elm.id})
          }
        }

      })
      this.onShuffleArray(this.shuffleArray)
    },
    onShuffleArray(arr) {
      arr.sort(() => Math.random() - 0.5)
    },
    decrementCount(itemId) {
      this.$emit('decrementCount', itemId);
    }
  },
  watch: {
    items: {
      handler() {
        this.pushSquares();
      },
      deep: true
    }
  },
  mounted() {
    this.pushSquares()
  }
}
</script>

<style scoped>
.diagram__item {
  display: flex;
  flex-wrap: wrap;
}
</style>