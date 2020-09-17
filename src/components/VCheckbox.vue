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
$light-blue-color: #0e98d7;
$dark-blue-color: #2d398e;
$white-color: #ffffff;
#v-checkbox__group {
  display: flex;
  flex-direction: column;
  color: $light-blue-color;
  margin-bottom: 40px;

  label {
    font-weight: bold;
    text-transform: uppercase;
    cursor: pointer;
  }

  input {
    width: 40px;
    -webkit-appearance: none;
    -moz-appearance: none;
    height: 40px;
    border-bottom: 0.1mm solid $light-blue-color;
    background-color: transparent;
    cursor: pointer;
    transition: 0.5s;
  }

  input:checked {
    background: $dark-blue-color;
    transition: 0.5s;
  }

  input:checked:after {
    margin-left: 14px;
    width: 8px;
    height: 27px;
    border: solid $white-color;
    border-width: 0 1.5mm 1.5mm 0;
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);
    -ms-transform: rotate(45deg);
    transform: rotate(45deg);
    content: '';
    display: inline-block;
    transition: 0.5s;
  }

  input:focus {
    outline: none;
  }
}
</style>
