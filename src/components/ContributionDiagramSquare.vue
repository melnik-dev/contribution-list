<template>
<div class="square">
</div>
</template>

<script>
export default {
  name: "ContributionDiagramSquare",
  props: {
    color: {
      default: 'black'
    }
  }
}
</script>

<style scoped>
.square {
  width: 14px;
  height: 14px;
  background: v-bind(color);
  margin: 2px;
  cursor: pointer;
}
</style>