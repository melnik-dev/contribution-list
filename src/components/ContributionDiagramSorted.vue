<template>
  <div v-for="item in items" :key="`s${item.id}`">
    <div v-if="item.checked" class="diagram__item" >
      <ContributionDiagramSquare
          v-for="index in item.count"
          :key="`s${item.id}${index}`"
          @click="decrementCount(item.id)"
          :color="item.color"/>
    </div>
  </div>
</template>

<script>
import ContributionDiagramSquare from './ContributionDiagramSquare.vue'
export default {
  name: "ContributionDiagramSorted",
  components: {
    ContributionDiagramSquare
  },
  props: ['items'],
  emits: ['decrementCount'],
  methods: {
    decrementCount(itemId) {
      this.$emit('decrementCount', itemId);
    }
  }
}
</script>

<style scoped>
.diagram__item {
  display: flex;
  flex-wrap: wrap;
}
</style>