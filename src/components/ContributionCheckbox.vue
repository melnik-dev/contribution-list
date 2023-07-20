<template>
  <label class="label" :for="label">

    <div class="check">
      <input
          class="check__input"
          :id="id"
          :name="name"
          type="checkbox"
          :checked="modelValue"
          @input="$emit('update:modelValue', $event.target.checked)"
      >
      <svg class="check__box" viewBox="0 0 20 20">
        <rect class="check__focus" width="20" height="20" rx="1"></rect>
        <rect class="check__square" x="3" y="3" width="14" height="14" rx="1"></rect>
        <polyline class="check__mark" points="5 9 9 13 15 6"></polyline>
        <rect v-if="point" class="check__mark--square" x="7" y="7" width="6" height="6" rx="1"></rect>
      </svg>
    </div>
    <slot></slot>
  </label>

</template>

<script>
export default {
  name: "ContributionCheckbox",
  props: {
    id: {
      type: String
    },
    name: {
      type: String
    },
    label: {
      type: String
    },
    modelValue: {
      type: Boolean
    },
    point: {
      type: Boolean,
      default: false
    }
  },
  emits: ["update:modelValue"],
}
</script>

<style scoped>
.label {
  display: flex;
  align-items: center;
  cursor: pointer;
  margin-right: auto;
}

.check {
  position: relative;
  width: 20px;
  height: 20px;
  margin-right: 5px;
}

.check__input {
  position: absolute;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

.check__box {
  position: absolute;

}

.check__focus {
  fill: none;
}

.check__square {
  fill: #ffffff;
  stroke: #000000;
  stroke-width: 1px;
}

.check__mark {
  display: none;
}

.check__input:checked + * .check__mark {
  display: block;
  fill: none;
  stroke: #000000;
  stroke-width: 1px;
}

.check__mark--square {
  display: block;
}
</style>