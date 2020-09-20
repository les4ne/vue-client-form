<template>
  <div id="v-input__group">
    <label :for="name" id="label">{{ label }}</label>
    <input
      :type="type"
      :id="name"
      :name="name"
      :class="invalid"
      v-on:input="updateValue($event.target.value)"
      autocomplete="off"
    />
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'v-input',
  props: {
    label: String,
    name: String,
    invalid: Object,
    value: String,
    type: {
      type: String,
      default: 'text',
    },
  },
  methods: {
    updateValue: function(value) {
      this.$emit('input', value)
    },
  },
}
</script>

<style lang="scss" scoped>
$light-blue-color: #0e98d7;
$dark-blue-color: #2d398e;
$white-color: #ffffff;
$red-color: #f05340;

#v-input__group {
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

  input[type='date'] {
    font-size: 1.4em;
  }

  input {
    width: 100%;
    padding: 10px;
    font-size: 1.2em;
    background: transparent;
    border: none;
    border-bottom: 2px solid $light-blue-color;
    outline: none;
    color: $white-color;
    caret-color: $white-color;
    padding-left: 5px;
    -webkit-transition: background 0.5s;
    -o-transition: background 0.5s;
    transition: background 0.5s;
  }

  input:focus {
    background: $dark-blue-color;
    -webkit-transition: background 0.5s;
    -o-transition: background 0.5s;
    transition: background 0.5s;
  }

  .invalid {
    border-color: $red-color;
  }
}
</style>
