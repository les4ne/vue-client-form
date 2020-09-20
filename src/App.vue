<template>
  <div id="app">
    <h1>Форма создания Клиента</h1>
    <form id="form" @submit.prevent="submit">
      <span class="warnInfo">* Поля обязательные для заполнения</span>
      <h2>Атрибуты формы:</h2>

      <v-input
        name="form-surname"
        label="фамилия *"
        v-model="surname"
        :validation="$v.surname"
      >
      </v-input>

      <v-input
        name="form-name"
        label="имя *"
        v-model="name"
        :validation="$v.name"
      >
      </v-input>

      <v-input
        name="form-patronymic"
        label="отчество"
        v-model="patronymic"
        :validation="$v.patronymic"
      >
      </v-input>

      <v-input
        type="date"
        name="form-date-of-birth"
        label="дата рождения *"
        v-model="dateBirth"
        :validation="$v.dateBirth"
      >
      </v-input>

      <v-input
        type="number"
        name="form-tel-number"
        label="номер телефона *"
        v-model="telNumber"
        :validation="$v.telNumber"
      >
      </v-input>

      <v-select name="form-sex" label="пол">
        <option value="1" default></option>
        <option value="2">мужской</option>
        <option value="3">женский</option>
      </v-select>

      <v-select
        name="client-group"
        label="группа клиентов *"
        multiple="multiple"
        v-model="clientGroup"
        :validation="$v.clientGroup"
      >
        <option value="1">VIP</option>
        <option value="2">Проблемные</option>
        <option value="3">ОМС</option>
      </v-select>

      <v-select name="attending-doctor" label="Лечащий врач">
        <option value="1"></option>
        <option value="2">Иванов</option>
        <option value="3">Захаров</option>
        <option value="4">Чернышева</option>
      </v-select>
      <v-checkbox name="do-not-send-sms" label="Не отправлять СМС"></v-checkbox>

      <h2>Адрес:</h2>
      <v-input
        type="number"
        name="address-index"
        label="Индекс"
        v-model="addressIndex"
        :validation="$v.addressIndex"
      >
      </v-input>

      <v-input name="address-country" label="Страна"></v-input>
      <v-input name="address-region" label="Область"></v-input>
      <v-input
        name="address-city"
        label="Город *"
        v-model="addressCity"
        :validation="$v.addressCity"
      >
      </v-input>
      <v-input name="address-street" label="Улица"></v-input>
      <v-input name="address-home" label="Дом"></v-input>

      <h2>Паспорт:</h2>
      <v-select
        name="document-type"
        label="тип документа *"
        v-model="documentType"
        :validation="$v.documentType"
      >
        <option value="1"></option>
        <option value="2">Паспорт</option>
        <option value="3">Свидетельство о рождении</option>
        <option value="4">Вод. удостоверение</option>
      </v-select>

      <v-input
        type="number"
        name="passport-series"
        label="серия"
        v-model="passportSeries"
        :validation="$v.passportSeries"
      >
      </v-input>

      <v-input
        name="passport-number"
        label="номер"
        v-model="passportNumber"
        :validation="$v.passportNumber"
      >
      </v-input>

      <v-input name="passport-issued-by" label="кем выдан"></v-input>

      <v-input
        type="date"
        name="passport-date-of-issue"
        label="дата выдачи *"
        v-model="passportIssueDate"
        :validation="$v.passportIssueDate"
      >
      </v-input>

      <span class="warnInfo">{{ submitStatus }}</span>

      <v-button value="создать клиента"></v-button>
    </form>
  </div>
</template>

<script>
import VInput from '@/components/VInput.vue'
import VSelect from '@/components/VSelect.vue'
import VCheckbox from '@/components/VCheckbox.vue'
import VButton from '@/components/VButton.vue'

import {
  required,
  minLength,
  maxLength,
  numeric,
  helpers,
  between,
} from 'vuelidate/lib/validators'

const telFormat = helpers.regex('numeric', /^7[0-9]*$/)

export default {
  name: 'App',
  data() {
    return {
      surname: '',
      name: '',
      patronymic: '',
      dateBirth: '',
      telNumber: '',
      clientGroup: '',
      addressIndex: '',
      addressCity: '',
      documentType: '',
      passportSeries: '',
      passportNumber: '',
      passportIssueDate: '',
      submitStatus: '',
    }
  },
  validations: {
    name: {
      required,
      minLength: minLength(4),
    },
    surname: {
      required,
      minLength: minLength(4),
    },
    patronymic: {
      minLength: minLength(4),
    },
    dateBirth: {
      required,
    },
    telNumber: {
      required,
      numeric,
      telFormat,
      minLengthEleven: minLength(11),
      maxLengthEleven: maxLength(11),
    },
    clientGroup: {
      required,
    },
    addressIndex: {
      numeric,
      minLengthSix: minLength(6),
      maxLengthSix: maxLength(6),
    },
    addressCity: {
      required,
      minLengthTwo: minLength(2),
    },
    documentType: {
      required,
    },
    passportSeries: {
      numeric,
      minLengthNumeric: minLength(4),
      maxLengthNumeric: maxLength(4),
    },
    passportNumber: {
      numeric,
      minLengthSix: minLength(6),
      maxLengthSix: maxLength(6),
    },
    passportIssueDate: {
      required,
    },
  },
  components: {
    VInput,
    VSelect,
    VCheckbox,
    VButton,
  },
  methods: {
    submit() {
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitStatus = 'Ошибка отправки, проверьте введенные данные!'
      } else {
        this.submitStatus = 'Отправка данных...'
        setTimeout(() => {
          this.submitStatus = 'Клиент успешно создан!'
        }, 500)
      }
    },
  },
}
</script>

<style lang="scss">
@import '/assets/sass/app';
</style>
