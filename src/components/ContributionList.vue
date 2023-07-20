<template>
  <div>
    <div class="list">
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
    </div>
    <div class="items">

    </div>
  </div>
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
    isCheckedOneItem() {
      // Проверяем, отмечен хоть один Items
      return this.list.items.some(item => item.checked === true)
    },
    isCheckedAllItem() {
      // Проверяем, отмечены ли все Items
      return this.list.items.every(item => item.checked === true)
    },
    isPoint() {
      if (this.isCheckedOneItem && !this.isCheckedAllItem) {
        return true;
      }
      return false
    }
  },
  methods: {
    toggleAllItems() {
      console.log('toggleAllItems')
      if (this.isCheckedOneItem) {
        // Снимаемсо всех
        this.list.items.forEach(item => (item.checked = false))
        this.listChecked = false
      } else {
        // Отмечаем все
        this.list.items.forEach(item => (item.checked = true))
        this.listChecked = true
      }
    },
    updateListCheckStatus() {
      if (this.isCheckedAllItem) {
        this.listChecked = true
      } else {
        this.listChecked = false
      }
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