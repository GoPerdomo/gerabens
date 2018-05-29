<template>
  <button :class="kind" :type="type">{{ label }}</button>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: "button",
    },
    label: {
      type: String,
      required: true,
    },
    kind: String,
  }
}
</script>

<style scoped>
button {
  background-color: lightblue;
}

.action {
  background-color: orange;
}
</style>
