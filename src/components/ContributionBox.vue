<template>
<div class="box">
  <slot></slot>
</div>
</template>

<script>
export default {
  name: "ContributionBox"
}
</script>

<style scoped>
.box {
  display: flex;
  flex: 1;
  border: 1px solid black;
  padding: 20px;
}
</style>