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
  width: 90%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  color: $light-blue-color;
  align-items: flex-start;
  margin: 0 auto 40px auto;

  label {
    font-weight: bold;
    text-transform: uppercase;
    cursor: pointer;
  }

  select {
    width: 100%;
    font-size: 1.2em;
    background: transparent;
    border: none;
    border-bottom: 2px solid $light-blue-color;
    outline: none;
    color: $white-color;
    -webkit-transition: background 0.5s;
    -o-transition: background 0.5s;
    transition: background 0.5s;
    padding: 5px;

    option {
      padding: 5px;
    }

    option:checked {
      background: $light-blue-color -webkit-gradient(linear, left bottom, left
            top, from($light-blue-color), to($light-blue-color));
      background: $light-blue-color -o-linear-gradient(bottom, $light-blue-color
            0%, $light-blue-color 100%);
      background: $light-blue-color
        linear-gradient(0deg, $light-blue-color 0%, $light-blue-color 100%);
    }
  }

  select:focus {
    background: $dark-blue-color;
    -webkit-transition: background 0.5s;
    -o-transition: background 0.5s;
    transition: background 0.5s;
  }
}
</style>
