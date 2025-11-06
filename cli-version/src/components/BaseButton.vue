<script>
export default {
  name: 'BaseButton'
}
</script>

<template>
  <!-- This v-on="$listeners" is a way
  to assign events to an element in a component.
  Without it, Vue does not know where to listen
  for the events. deprecated == attrs -->
  <button v-on="$attrs">
    <slot></slot>
  </button>
</template>

<style></style>