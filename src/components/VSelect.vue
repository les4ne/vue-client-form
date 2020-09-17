<template>
  <div id="v-select__group">
    <label :for="name">{{ label }}</label>

    <select :name="name" :id="name" :multiple="multiple">
      <slot></slot>
    </select>
  </div>
</template>

<script>
export default {
  name: 'v-select',
  props: {
    label: String,
    multiple: String,
    name: String,
  },
}
</script>

<style lang="scss" scoped>
$light-blue-color: #0e98d7;
$dark-blue-color: #2d398e;
$white-color: #ffffff;
#v-select__group {
  display: flex;
  flex-direction: column;
  color: $light-blue-color;
  margin-bottom: 40px;

  label {
    font-weight: bold;
    text-transform: uppercase;
    cursor: pointer;
  }

  select {
    font-size: 1.2em;
    background: transparent;
    border: none;
    border-bottom: 2px solid $light-blue-color;
    outline: none;
    color: $white-color;
    transition: background 0.5s;
    padding: 5px;

    option {
      padding: 5px;
    }

    option:checked {
      background: $light-blue-color
        linear-gradient(0deg, $light-blue-color 0%, $light-blue-color 100%);
    }
  }

  select:focus {
    background: $dark-blue-color;
    transition: background 0.5s;
  }
}
</style>
