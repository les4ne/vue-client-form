<template>
  <div id="v-input__group">
    <label :for="name" id="label">{{ label }}</label>
    <input
      type="text"
      :id="name"
      :name="name"
      autocomplete="off"
      class="alert-danger"
    />
    <span class="alert-danger">• Must contain only alpha numeric numbers</span>
    <span class="alert-danger">• Must contain only alpha numeric numbers</span>
    <span class="alert-danger">• Must contain only alpha numeric numbers</span>
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

  span {
    color: #f05340;
    font-size: 1em;
    font-weight: bold;
  }

  .alert-danger {
    border-color: #f05340;
  }
}
</style>
