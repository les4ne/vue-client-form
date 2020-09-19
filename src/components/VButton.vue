<template>
  <div id="v-button__group">
    <input type="submit" :value="value" />
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
  width: 90%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: end;
  -ms-flex-pack: end;
  justify-content: flex-start;
  margin: 0 auto;

  input {
    padding: 15px 50px;
    border: 2px solid $white-color;
    background: transparent;
    color: $white-color;
    font-weight: bold;
    font-size: 1em;
    -webkit-transition: 0.5s;
    -o-transition: 0.5s;
    transition: 0.5s;
    text-transform: uppercase;
    cursor: pointer;
  }

  input:hover {
    background: $white-color;
    color: $dark-blue-color;
    -webkit-transition: 0.5s;
    -o-transition: 0.5s;
    transition: 0.5s;
  }

  input:focus {
    outline: none;
  }
}
</style>
