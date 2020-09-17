<template>
  <div id="app">
    <h1>Форма создания Клиента</h1>
    <form action="" id="form">
      <h2>Атрибуты формы:</h2>
      <v-input name="form-surname" label="фамилия *"></v-input>
      <v-input name="form-name" label="имя *"></v-input>
      <v-input name="form-patronymic" label="отчество"></v-input>
      <v-input name="form-date-of-birth" label="дата рождения *"></v-input>
      <v-input name="form-tel-number" label="номер телефона *"></v-input>
      <v-input name="form-sex" label="пол"></v-input>
      <v-select
        name="client-group"
        label="Группа клиентов *"
        multiple="multiple"
      >
        <option value="1">VIP</option>
        <option value="2">Проблемные</option>
        <option value="3">ОМС</option>
      </v-select>
      <v-select name="attending-doctor" label="Лечащий врач">
        <option value="1">Иванов</option>
        <option value="2">Захаров</option>
        <option value="3">Чернышева</option>
      </v-select>
      <v-checkbox name="do-not-send-sms" label="Не отправлять СМС"></v-checkbox>

      <h2>Адрес:</h2>
      <v-input name="address-index" label="Индекс"></v-input>
      <v-input name="address-country" label="Страна"></v-input>
      <v-input name="address-region" label="Область"></v-input>
      <v-input name="address-city" label="Город *"></v-input>
      <v-input name="address-street" label="Улица"></v-input>
      <v-input name="address-home" label="Дом"></v-input>

      <h2>Паспорт:</h2>
      <v-select name="document-type" label="Тип документа *">
        <option value="1">Паспорт</option>
        <option value="2">Свидетельство о рождении</option>
        <option value="3">Вод. удостоверение</option>
      </v-select>
      <v-input name="passport-series" label="серия"></v-input>
      <v-input name="passport-number" label="номер"></v-input>
      <v-input name="passport-issued-by" label="кем выдан"></v-input>
      <v-input name="passport-date-of-issue" label="дата выдачи *"></v-input>
      <v-button value="создать"></v-button>
    </form>
  </div>
</template>

<script>
import VInput from '@/components/VInput.vue'
import VSelect from '@/components/VSelect.vue'
import VCheckbox from '@/components/VCheckbox.vue'
import VButton from '@/components/VButton.vue'

export default {
  name: 'App',
  components: {
    VInput,
    VSelect,
    VCheckbox,
    VButton,
  },
}
</script>

<style lang="scss">
$light-blue-color: #24c6dc;
$dark-blue-color: #0e98d7;
$light-violet-color: #514a9d;
$dark-violet-color: #3a469c;
$white-color: #ffffff;
$grey-color: rgba(0, 0, 0, 0.35);

body {
  background: $light-blue-color;
  background: -webkit-linear-gradient(
    to left,
    $light-violet-color,
    $light-blue-color
  );
  background: linear-gradient(to left, $light-violet-color, $light-blue-color);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 20px;
  width: 720px;
  margin: 60px auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border: 10px solid $dark-blue-color;
  background: $dark-violet-color;
  box-shadow: $grey-color 0px 5px 15px;

  h1 {
    color: $white-color;
    text-transform: uppercase;
  }

  form {
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;

    h2 {
      color: $white-color;
      text-transform: uppercase;
      text-align: center;
    }
  }
}
</style>
