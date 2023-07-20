<template>
  <details>
    <summary>
      <slot name="title">
        title
      </slot>
    </summary>
    <p>
      <slot name="subtitle">
        text
      </slot>
    </p>

  </details>
</template>

<script>
export default {
  name: "ContributionDetails",
  props: {
    mark: {
      type: String,
      default: 'block'
    }
  }
}
</script>

<style scoped>
p {
  display: flex;
  flex-direction: column;
  flex: 1;
  margin: 0;
  margin-left: 30px;
  position: relative;
}
summary::marker,
summary::-webkit-details-marker {
  display: none;
}

summary::-moz-list-bullet {
  list-style-type: none;
}

summary {
  padding: .3em .6em .3em 1.5em;
  display: flex;
  cursor: pointer;
  position: relative;
}

summary:before {
  display: v-bind(mark);
  left: .3em;
  top: .4em;
  color: transparent;
  background: url("data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjM0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIzNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cGF0aCBkPSJNOC41OSAxNi4zNGw0LjU4LTQuNTktNC41OC00LjU5TDEwIDUuNzVsNiA2LTYgNnoiLz48L3N2Zz4=") no-repeat 50% 50% / 1em 1em;
  width: 1em;
  height: 1em;
  content: "";
  position: absolute;
  transition: transform .5s;
}

details[open] > summary:before {
  transform: rotateZ(90deg);
}

summary ~ * {
  padding: 0 1em 0 1em;
}

details[open] summary ~ * {
  animation: sweep .5s ease-in-out;
}

@keyframes sweep {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

details {
  display: flex;
  width: 100%;
  margin-bottom: .5rem;
}

</style>