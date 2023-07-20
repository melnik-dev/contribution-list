<template>
<div class="box">
  <slot></slot>
</div>
</template>

<script>
export default {
  name: "ContributionBox",
  props: {
    flex: {
      default: 1
    },
    border: {
      default: '1px solid black'
    },
    padding: {
      default: '20px'
    },
    boxGap: {
      default: '0'
    },
    fDirection: {
      default: 'row'
    },
    mBottom: {
      default: '0'
    }
  }
}
</script>

<style scoped>
.box {
  display: flex;
  flex:  v-bind(flex);
  border:  v-bind(border);
  padding: v-bind(padding);
  gap: v-bind(boxGap);
  flex-direction: v-bind(fDirection);
  margin-bottom: v-bind(mBottom);
}
</style>