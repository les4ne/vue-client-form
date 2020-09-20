<template>
  <div id="v-button__group">
    <input type="submit" :value="value" />
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'v-button',
  props: {
    value: String,
  },
}
</script>

<style lang="scss" scoped>
@import '../assets/sass/button';
</style>
