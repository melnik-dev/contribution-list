<template>
  <ContributionBox f-direction="column" box-gap="5px" v-if="lists.length">
    <ContributionBox flex="0" padding="0"
                     v-for="list in lists"
                     :key="`d${list.id}`">

      <ContributionDetails mark="none">
        <template #title>
          {{ list.name }}
        </template>

        <template #subtitle>
          <ContributionDiagramBox
              @decrement-count="decrementCount"
              :listId="list.id"
              :items="list.items"/>
        </template>
      </ContributionDetails>
    </ContributionBox>
  </ContributionBox>
</template>

<script>
import ContributionBox from './ContributionBox.vue'
import ContributionDetails from './ContributionDetails.vue'
import ContributionDiagramBox from './ContributionDiagramBox.vue'

export default {
  name: "ContributionAllDiagram",
  components: {
    ContributionBox,
    ContributionDetails,
    ContributionDiagramBox,
  },
  props: ['lists'],
  methods: {
    findItemById(listId, itemId) {
      const list = this.lists.find(list => list.id === listId)
      if (list) {
        return list.items.find(item => item.id === itemId)
      }
      return null;
    },
    decrementCount({listId, itemId}) {
      const item = this.findItemById(listId, itemId)
      if (item) {
        item.count--
      }
    }
  },
}
</script>

<style scoped>


</style>