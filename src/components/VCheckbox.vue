<template>
  <div id="v-checkbox__group">
    <label :for="name">{{ label }}</label>
    <input type="checkbox" :name="name" :id="name" />
  </div>
</template>

<script>
export default {
  name: 'checkbox',
  props: {
    label: String,
    name: String,
  },
}
</script>

<style lang="scss" scoped>
@import '../assets/sass/checkbox';
</style>
