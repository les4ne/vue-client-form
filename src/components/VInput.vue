<template>
  <div id="v-input__group">
    <label :for="name" id="label">{{ label }}</label>
    <input type="text" :id="name" :name="name" autocomplete="off" />
  </div>
</template>

<script>
export default {
  name: 'v-input',
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

#v-input__group {
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
    padding: 10px 400px;
    font-size: 1.2em;
    background: transparent;
    border: none;
    border-bottom: 2px solid $light-blue-color;
    outline: none;
    color: $white-color;
    caret-color: $white-color;
    padding-left: 5px;
    transition: background 0.5s;
  }

  input:focus {
    background: $dark-blue-color;
    transition: background 0.5s;
  }
}
</style>
