<template>
  <div id="v-button__group">
    <input type="button" :value="value" />
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
$white-color: #ffffff;
$dark-blue-color: #2d398e;
#v-button__group {
  display: flex;
  justify-content: flex-end;

  input {
    padding: 15px 50px;
    border: 2px solid $white-color;
    background: transparent;
    color: $white-color;
    font-weight: bold;
    font-size: 1em;
    transition: 0.5s;
    text-transform: uppercase;
    cursor: pointer;
  }

  input:hover {
    background: $white-color;
    color: $dark-blue-color;
    transition: 0.5s;
  }

  input:focus {
    outline: none;
  }
}
</style>
