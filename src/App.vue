<template>
  <ContributionBox class="box__container">

    <ContributionBox class="left f-column">
      <ContributionDetails v-for="list in lists" :key="list.id">

        <template #title>
          <ContributionList :list="list"/>
        </template>

        <template #subtitle>
          <ContributionBox
              class="p-none border-none gap-5"
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

            <span>
              <input class="input__count" type="text"
                     v-model="item.count"
                     @change="onChange($event, list.id, item.id, 'count')">
            </span>
            <span>
              <input class="input__color" type="color"
                     v-model="item.color"
                     @change="onChange($event, list.id, item.id, 'color')">
            </span>
          </ContributionBox>

        </template>

      </ContributionDetails>
    </ContributionBox>


    <ContributionBox class="righ f-column gap-5">
      <ContributionBox
          class="p-none flex-0"
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

  </ContributionBox>

</template>

<script>
import ContributionBox from './components/ContributionBox.vue'
import ContributionDetails from './components/ContributionDetails.vue'
import ContributionCheckbox from './components/ContributionCheckbox.vue'
import ContributionDiagramBox from './components/ContributionDiagramBox.vue'
import ContributionList from './components/ContributionList.vue'

export default {
  name: 'App',
  components: {
    ContributionBox,
    ContributionDetails,
    ContributionCheckbox,
    ContributionDiagramBox,
    ContributionList
  },
  data() {
    return {
      lists: [{
        id: '1',
        name: 'List 1',
        items: [{
          id: '1',
          name: 'Item 1',
          checked: false,
          count: 10,
          color: 'red'
        }, {
          id: '2',
          name: 'Item 2',
          checked: true,
          count: 16,
          color: 'yellow'
        }, {
          id: '3',
          name: 'Item 3',
          checked: true,
          count: 40,
          color: 'green'
        }, {
          id: '4',
          name: 'Item 4',
          checked: false,
          count: 0,
          color: 'blue'
        }]
      }, {
        id: '2',
        name: 'List 2',
        items: [{
          id: '1',
          name: 'Item 1',
          checked: false,
          count: 10,
          color: '#ff0000'
        }, {
          id: '2',
          name: 'Item 2',
          checked: true,
          count: 16,
          color: '#00ff04'
        }, {
          id: '3',
          name: 'Item 3',
          checked: true,
          count: 40,
          color: '#0008ff'
        }, {
          id: '4',
          name: 'Item 4',
          checked: false,
          count: 0,
          color: '#ff00ea'
        }]
      },]
    }
  },
  methods: {
    findItemById(listId, itemId) {
      const list = this.lists.find(list => list.id === listId);
      if (list) {
        return list.items.find(item => item.id === itemId);
      }
      return null;
    },
    onChange(evt, listId, itemId, prop) {
      const item = this.findItemById(listId, itemId);
      if (item) {
        item[prop] = prop === 'count' ? Number(evt.target.value) : evt.target.value;
      }
    },
    decrementCount({listId, itemId}) {
      console.log('itemId ', itemId)
      console.log('listId ', listId)
      const item = this.findItemById(listId, itemId);
      if (item) {
        item.count--
      }
    }
  }
}
</script>

<style>
#app {
  margin-top: 60px;
}

* {
  box-sizing: border-box;
}

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

.box__container {
  max-width: 900px;
  margin: 0 auto;
  gap: 40px;
}

.p-none {
  padding: 0 !important;
}

.border-none {
  border: none !important;
}

.gap-5 {
  gap: 5px
}

.f-column {
  flex-direction: column;
}

.flex-0 {
  flex: 0 !important;
}
</style>
