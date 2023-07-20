<template>
  <ContributionCheckbox
      @change="toggleAllItems"
      v-model="listChecked"
      :id="`list-${list.id}`"
      :label="`list-${list.id}`"
      :name="`list-${list.id}`"
      :point="isPoint"
  >
    {{ list.name }}
  </ContributionCheckbox>
</template>

<script>
import ContributionCheckbox from './ContributionCheckbox.vue'

export default {
  name: "ContributionList",
  components: {
    ContributionCheckbox
  },
  props: ['list'],
  data() {
    return {
      listChecked: false,
    };
  },
  computed: {
    hasCheckedItem() {
      // Проверяем, отмечен хоть один Items
      return this.list.items && this.list.items.some(item => item.checked === true)
    },
    hasCheckedAllItem() {
      // Проверяем, отмечены ли все Items
      return this.list.items && this.list.items.every(item => item.checked === true)
    },
    isPoint() {
      return this.hasCheckedItem && !this.hasCheckedAllItem
    }
  },
  methods: {
    toggleAllItems() {
      const haveCheckAll = !this.hasCheckedItem
      this.list.items.forEach(item => {item.checked = haveCheckAll})
      this.listChecked = haveCheckAll
    },
    updateListCheckStatus() {
      this.listChecked = this.hasCheckedAllItem || false
    }
  },
  watch: {
    'list.items': {
      handler() {
        this.updateListCheckStatus()
      },
      deep: true,
    },
  },
  mounted() {
    this.updateListCheckStatus()
  }
}
</script>

<style scoped>

</style>