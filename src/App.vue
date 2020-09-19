<template>
  <div id="app">
    <h1>Форма создания Клиента</h1>
    <form id="form" @submit.prevent="formSubmit">
      <span class="warnInfo">* Поля обязательные для заполнения</span>
      <h2>Атрибуты формы:</h2>

      <v-input
        name="form-surname"
        label="фамилия *"
        v-model="surname"
        @input="$v.surname.$touch"
        :invalid="{
          invalid:
            ($v.surname.$dirty && !$v.surname.required) ||
            !$v.surname.minLength,
        }"
      >
        <span v-if="$v.surname.$dirty && !$v.surname.required">
          • Поле не должно быть пустым.
        </span>
        <span v-if="!$v.surname.minLength">
          • Поле должно иметь как минимум {{ $v.surname.$params.minLength.min }}
          букв(ы).
        </span>
      </v-input>

      <v-input
        name="form-name"
        label="имя *"
        v-model="name"
        @input="$v.name.$touch"
        :invalid="{
          invalid: ($v.name.$dirty && !$v.name.required) || !$v.name.minLength,
        }"
      >
        <span v-if="$v.name.$dirty && !$v.name.required">
          • Поле не должно быть пустым.
        </span>
        <span v-if="!$v.name.minLength">
          • Поле должно иметь как минимум
          {{ $v.name.$params.minLength.min }} букв(ы).
        </span>
      </v-input>

      <v-input
        name="form-patronymic"
        label="отчество"
        v-model="patronymic"
        @input="$v.patronymic.$touch"
        :invalid="{
          invalid: $v.patronymic.$dirty && !$v.patronymic.minLength,
        }"
      >
        <span v-if="!$v.patronymic.minLength">
          • Поле должно иметь как минимум
          {{ $v.patronymic.$params.minLength.min }} букв(ы).
        </span>
      </v-input>

      <v-input
        type="date"
        name="form-date-of-birth"
        label="дата рождения *"
        v-model="dateBirth"
        @input="$v.dateBirth.$touch"
        :invalid="{
          invalid: $v.dateBirth.$dirty && !$v.dateBirth.required,
        }"
      >
        <span v-if="$v.dateBirth.$dirty && !$v.dateBirth.required">
          • Поле не должно быть пустым.
        </span>
      </v-input>

      <v-input
        name="form-tel-number"
        label="номер телефона *"
        v-model="telNumber"
        @input="$v.telNumber.$touch"
        :invalid="{
          invalid:
            ($v.telNumber.$dirty && !$v.telNumber.required) ||
            !$v.telNumber.minLength ||
            !$v.telNumber.maxLength ||
            !$v.telNumber.numeric ||
            !$v.telNumber.telFormat,
        }"
      >
        <span v-if="$v.telNumber.$dirty && !$v.telNumber.required">
          • Поле не должно быть пустым.
        </span>
        <span v-if="!$v.telNumber.minLength || !$v.telNumber.maxLength">
          • Поле должно иметь 11 цифр.
        </span>
        <span v-if="!$v.telNumber.numeric">
          • Поле должно содержать только цифры.
        </span>
        <span v-if="!$v.telNumber.telFormat">
          • Номер должен начинаться с 7.
        </span>
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
        :statement="$v.clientGroup.$dirty && !$v.clientGroup.required"
        @input="$v.clientGroup.$touch"
        :invalid="{
          invalid: $v.clientGroup.$dirty && !$v.clientGroup.required,
        }"
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
        name="address-index"
        label="Индекс"
        v-model="addressIndex"
        @input="$v.addressIndex.$touch"
        :invalid="{
          invalid:
            !$v.addressIndex.minLength ||
            !$v.addressIndex.maxLength ||
            !$v.addressIndex.numeric,
        }"
      >
        <span v-if="!$v.addressIndex.minLength || !$v.addressIndex.maxLength">
          • Поле должно иметь 6 цифр.
        </span>
        <span v-if="!$v.addressIndex.numeric">
          • Поле должно содержать только цифры.
        </span>
      </v-input>

      <v-input name="address-country" label="Страна"></v-input>
      <v-input name="address-region" label="Область"></v-input>
      <v-input
        name="address-city"
        label="Город *"
        v-model="addressCity"
        @input="$v.addressCity.$touch"
        :invalid="{
          invalid:
            ($v.addressCity.$dirty && !$v.addressCity.required) ||
            !$v.addressCity.minLength,
        }"
      >
        <span v-if="$v.addressCity.$dirty && !$v.addressCity.required">
          • Поле не должно быть пустым.
        </span>
        <span v-if="!$v.addressCity.minLength">
          • Поле должно иметь как минимум
          {{ $v.addressCity.$params.minLength.min }} букв(ы).
        </span>
      </v-input>
      <v-input name="address-street" label="Улица"></v-input>
      <v-input name="address-home" label="Дом"></v-input>

      <h2>Паспорт:</h2>
      <v-select
        name="document-type"
        label="тип документа *"
        v-model="documentType"
        :statement="$v.documentType.$dirty && !$v.documentType.required"
        @input="$v.documentType.$touch"
        :invalid="{
          invalid: $v.documentType.$dirty && !$v.documentType.required,
        }"
      >
        <option value="1"></option>
        <option value="2">Паспорт</option>
        <option value="3">Свидетельство о рождении</option>
        <option value="4">Вод. удостоверение</option>
      </v-select>

      <v-input
        name="passport-series"
        label="серия"
        v-model="passportSeries"
        @input="$v.passportSeries.$touch"
        :invalid="{
          invalid:
            !$v.passportSeries.minLength ||
            !$v.passportSeries.maxLength ||
            !$v.passportSeries.numeric,
        }"
      >
        <span v-if="!$v.passportSeries.numeric">
          • Поле должно содержать только цифры.
        </span>
        <span
          v-if="!$v.passportSeries.minLength || !$v.passportSeries.maxLength"
        >
          • Поле должно иметь
          {{ $v.passportSeries.$params.minLength.min }} цифр(ы).
        </span>
      </v-input>

      <v-input
        name="form-tel-number"
        label="номер телефона *"
        v-model="telNumber"
        @input="$v.telNumber.$touch"
        :invalid="{
          invalid:
            ($v.telNumber.$dirty && !$v.telNumber.required) ||
            !$v.telNumber.minLength ||
            !$v.telNumber.maxLength ||
            !$v.telNumber.numeric ||
            !$v.telNumber.telFormat,
        }"
      >
        <span v-if="$v.telNumber.$dirty && !$v.telNumber.required">
          • Поле не должно быть пустым.
        </span>
        <span v-if="!$v.telNumber.minLength || !$v.telNumber.maxLength">
          • Поле должно иметь 11 цифр.
        </span>
        <span v-if="!$v.telNumber.numeric">
          • Поле должно содержать только цифры.
        </span>
        <span v-if="!$v.telNumber.telFormat">
          • Номер должен начинаться с 7.
        </span>
      </v-input>
      <v-input
        name="passport-number"
        label="номер"
        v-model="passportNumber"
        @input="$v.passportNumber.$touch"
        :invalid="{
          invalid:
            !$v.passportNumber.minLength ||
            !$v.passportNumber.maxLength ||
            !$v.passportNumber.numeric,
        }"
      >
        <span
          v-if="!$v.passportNumber.minLength || !$v.passportNumber.maxLength"
        >
          • Поле должно иметь 6 цифр.
        </span>
        <span v-if="!$v.passportNumber.numeric">
          • Поле должно содержать только цифры.
        </span>
      </v-input>

      <v-input name="passport-issued-by" label="кем выдан"></v-input>

      <v-input
        type="date"
        name="passport-date-of-issue"
        label="дата выдачи *"
        v-model="passportIssueDate"
        @input="$v.passportIssueDate.$touch"
        :invalid="{
          invalid:
            $v.passportIssueDate.$dirty && !$v.passportIssueDate.required,
        }"
      >
        <span
          v-if="$v.passportIssueDate.$dirty && !$v.passportIssueDate.required"
        >
          • Поле не должно быть пустым.
        </span>
      </v-input>

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
      minLength: minLength(11),
      maxLength: maxLength(11),
    },
    clientGroup: {
      required,
    },
    addressIndex: {
      numeric,
      minLength: minLength(6),
      maxLength: maxLength(6),
    },
    addressCity: {
      required,
      minLength: minLength(2),
    },
    documentType: {
      required,
    },
    passportSeries: {
      numeric,
      minLength: minLength(4),
      maxLength: maxLength(4),
    },
    passportNumber: {
      numeric,
      minLength: minLength(6),
      maxLength: maxLength(6),
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
    formSubmit() {
      if (this.$v.$invalid) {
        this.$v.$touch()
        return
      }
      console.log('Submitted')
    },
  },
}
</script>

<style lang="scss">
$light-blue-color: #24c6dc;
$dark-blue-color: #0e98d7;
$light-violet-color: #514a9d;
$dark-violet-color: #3a469c;
$white-color: #ffffff;
$red-color: #f05340;
$grey-color: rgba(0, 0, 0, 0.35);

$break-small: 320px;
$break-large: 1200px;

* {
  margin: 0;
  padding: 0;
}

body {
  width: 100%;
  height: 100%;
  background: $light-blue-color;
  background: -webkit-gradient(
    linear,
    right top,
    left top,
    from($light-violet-color),
    to($light-blue-color)
  );
  background: -o-linear-gradient(right, $light-violet-color, $light-blue-color);
  background: linear-gradient(to left, $light-violet-color, $light-blue-color);
  background-size: cover;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 20px;
  width: 720px;
  margin: 60px auto;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  border: 10px solid $dark-blue-color;
  background: $dark-violet-color;
  -webkit-box-shadow: $grey-color 0px 5px 15px;
  box-shadow: $grey-color 0px 5px 15px;

  h1 {
    color: $white-color;
    text-transform: uppercase;
    margin-bottom: 5px;
  }

  form {
    width: 100%;
    max-width: 960px;
    height: 100%;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -ms-flex-direction: column;
    flex-direction: column;
    -ms-flex-line-pack: center;
    align-content: center;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    padding-right: 15px;

    h2 {
      color: $white-color;
      text-transform: uppercase;
      text-align: center;
      margin-bottom: 30px;
    }

    span {
      color: $red-color;
      font-weight: bold;
    }

    .warnInfo {
      margin-top: 10px;
      text-align: center;
      align-self: center;
      font-weight: normal;
    }
  }

  @media screen and (min-width: 320px) {
    width: 81%;
    margin: 10px auto;
    -webkit-transition: 0.5s;
    -o-transition: 0.5s;
    transition: 0.5s;
    border-width: 5px;
    h1 {
      text-align: center;
      font-size: 1.4em;
    }
    h2 {
      font-size: 1.1em;
    }
  }

  @media screen and (min-width: 364px) {
    -webkit-transition: 0.5s;
    -o-transition: 0.5s;
    transition: 0.5s;
    h1 {
      font-size: 1.5em;
    }
    h2 {
      font-size: 1em;
    }
  }

  @media screen and (min-width: 788px) {
    width: 720px;
    margin: 60px auto;
    -webkit-transition: 0.5s;
    -o-transition: 0.5s;
    transition: 0.5s;
    h1 {
      font-size: 2em;
    }
    h2 {
      font-size: 1.5em;
    }
  }
}
</style>
