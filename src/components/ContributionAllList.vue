<template>
  <ContributionBox f-direction="column" v-if="lists.length">
    <ContributionDetails v-for="list in lists" :key="list.id">

      <template #title>
        <ContributionList :list="list"/>
      </template>

      <template #subtitle>
        <ContributionBox border="none" padding="0" box-gap="5px" m-bottom="5px"
                         v-for="item in list.items"
                         :key="`${list.id}${item.id}`"
        >
          <ContributionCheckbox
              v-model="item.checked"
              :id="`item-${list.id}${item.id}`"
              :label="`item-${list.id}${item.id}`"
              :name="`item-${list.id}${item.id}`"
          >
            {{ item.name }}
          </ContributionCheckbox>
              <input class="input__count" type="text"
                     v-model.number="item.count"
                     @change="onChange($event, list.id, item.id, 'count')"
              >
              <input class="input__color" type="color"
                     v-model="item.color"
                     @change="onChange($event, list.id, item.id, 'color')"
              >
        </ContributionBox>
      </template>

    </ContributionDetails>
  </ContributionBox>
</template>

<script>
import ContributionBox from './ContributionBox.vue'
import ContributionDetails from './ContributionDetails.vue'
import ContributionCheckbox from './ContributionCheckbox.vue'
import ContributionList from './ContributionList.vue'

export default {
  name: "ContributionAllList",
  components: {
    ContributionBox,
    ContributionDetails,
    ContributionCheckbox,
    ContributionList
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
    onChange(evt, listId, itemId, prop) {
      const item = this.findItemById(listId, itemId)
      if (item) {
        item[prop] = prop === 'count' ? Number(evt.target.value) : evt.target.value
      }
    },
  }
}
</script>

<style scoped>

.input__count {
  width: 30px;
  border: none;
}

.input__color {
  width: 22px;
  height: 22px;
  padding: 0;
  border: 0;
  cursor: pointer;
}
.input__color::-webkit-color-swatch-wrapper {
  padding: 0;
  border: none;
}
.input__color::-moz-color-swatch {
  border: none;
}
.input__color::-webkit-color-swatch {
  border: none;
}
</style>