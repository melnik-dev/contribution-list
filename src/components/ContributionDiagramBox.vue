<template>
  <div class="diagram__box">
    <button v-if="hasCheckedItem" @click="toggleSorting">
      {{ isSortedDiagram ? 'Перемешать' : 'Сортировать' }}
    </button>
    <ContributionDiagramSorted
        @decrement-count="decrementCount"
        v-if="isSortedDiagram"
        :items="items"/>
    <ContributionDiagramMixed
        @decrement-count="decrementCount"
        v-else :items="items"/>
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
  props: ['listId', 'items',],
  emits: ['decrementCount'],
  data() {
    return {
      isSortedDiagram: true
    }
  },
  computed: {
    hasCheckedItem() {
      // Проверяем, отмечен хоть один Items
      return this.items && this.items.some(item => item.checked === true)
    }
  },
  methods: {
    toggleSorting() {
      this.isSortedDiagram = !this.isSortedDiagram
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