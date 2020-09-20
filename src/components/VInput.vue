<template>
  <div id="v-input__group">
    <label :for="name" id="label">{{ label }}</label>
    <input
      :type="type"
      :id="name"
      :name="name"
      :class="{
        error:
          typeof validation !== 'undefined' &&
          validation.$dirty &&
          validation.$invalid,
      }"
      v-on:input="updateValue($event.target.value)"
      @blur="onBlur"
      autocomplete="off"
    />
    <template v-if="typeof validation !== 'undefined' && validation.$dirty">
      <span v-for="(error, index) in errors" :key="index">{{ error }}</span>
    </template>
  </div>
</template>

<script>
import errorMessages from '../errors'

export default {
  name: 'v-input',
  props: {
    label: String,
    name: String,
    value: String,
    type: {
      type: String,
      default: 'text',
    },
    validation: {
      type: Object,
      required: false,
    },
  },
  computed: {
    errors() {
      let params = this.validation.$params
      let errors = []

      for (let param in params) {
        if (!this.validation[param]) {
          errors.push(errorMessages[param])
        }
      }

      return errors
    },
  },
  methods: {
    updateValue: function(value) {
      this.$emit('input', value)
    },
    onBlur() {
      if (typeof this.validation !== 'undefined') {
        this.validation.$touch()
      }
    },
  },
}
</script>

<style lang="scss" scoped>
@import '../assets/sass/input';
</style>
