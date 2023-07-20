<template>
<div class="diagram__box">
  <button @click="sortedDiagram">
    {{ isSorted ? 'Перемешать' : 'Сортировать'}}
  </button>
  <ContributionDiagramSorted
      @decrement-count="decrementCount"
      v-if="isSorted"
      :items="items" />
  <ContributionDiagramMixed
      @decrement-count="decrementCount"
      v-else :items="items" />
</div>
</template>

<script>

import ContributionDiagramSorted from './ContributionDiagramSorted.vue'
import ContributionDiagramMixed from './ContributionDiagramMixed.vue'
export default {
  name: "ContributionDiagramBox",
  components: {
    ContributionDiagramSorted,
    ContributionDiagramMixed
  },
  props: ['listId','items', ],
  emits: ['decrementCount'],
  data() {
    return {
      isSorted: true
    }
  },
  methods: {
  sortedDiagram() {
    this.isSorted = !this.isSorted
  },
    decrementCount(itemId) {
      this.$emit('decrementCount', {
        itemId: itemId,
        listId: this.listId
      });
    }
  }
}
</script>

<style scoped>
button {
  position: absolute;
  top: -25px;
  right: 10px;
}
</style>