<template>
  <ContributionBox box-gap="40px">
    <ContributionAllList :lists="lists"/>
    <ContributionAllDiagram :lists="lists"/>
  </ContributionBox>
</template>

<script>
import listDB  from "./listDB"
import ContributionBox from './components/ContributionBox.vue'
import ContributionAllList from './components/ContributionAllList.vue'
import ContributionAllDiagram from './components/ContributionAllDiagram.vue'

export default {
  name: 'App',
  components: {
    ContributionBox,
    ContributionAllList,
    ContributionAllDiagram
  },
  data() {
    return {
      lists: []
    }
  },
  mounted() {
    this.lists = listDB.list
  }
}
</script>

<style>
#app {
  max-width: 900px;
  margin: 0 auto;
  margin-top: 60px;
}

* {
  box-sizing: border-box;
}

</style>
