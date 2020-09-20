<template>
  <div id="v-select__group">
    <label :for="name">{{ label }}</label>
    <select
      :name="name"
      :id="name"
      :multiple="multiple"
      :class="{
        error:
          typeof validation !== 'undefined' &&
          validation.$dirty &&
          validation.$invalid,
      }"
      v-on:input="updateValue($event.target.value)"
      @blur="onBlur"
    >
      <slot></slot>
    </select>
    <template v-if="typeof validation !== 'undefined' && validation.$dirty">
      <span v-for="(error, index) in errors" :key="index">{{ error }}</span>
    </template>
  </div>
</template>

<script>
import errorMessages from '../errors'

export default {
  name: 'v-select',
  props: {
    label: String,
    multiple: {
      type: String,
      required: false,
    },
    name: String,
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
@import '../assets/sass/select';
</style>
