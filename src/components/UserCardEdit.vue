<template>
  <div>
    <v-card-title class="text-center justify-center">
      Редактирование пользователя <br> {{ user.fullName }}
    </v-card-title>
    <v-card-text>
      <v-form v-if="user" ref="form" v-model="valid">
        <v-file-input
          label="Фотография"
          prepend-icon="mdi-camera"
          v-model="user.image"
        />
        <v-text-field
          v-model="user.firstname"
          :rules="[rules.required]"
          label="Имя"
        />
        <v-text-field
          v-model="user.lastname"
          :rules="[rules.required]"
          label="Фамилия"
        />
        <v-select
          v-model="user.gender"
          :items="['male', 'female']"
          label="Пол"
        >
          <template v-slot:selection="data">
            {{ getGenderString(data.item) }}
          </template>
          <template v-slot:item="data">
            {{ getGenderString(data.item) }}
          </template>
        </v-select>
        <v-menu>
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="user.birthday"
              :rules="[rules.required]"
              label="Дата рождения"
              v-bind="attrs"
              v-on="on"
            />
          </template>
          <v-date-picker
            v-model="user.birthday"
          />
        </v-menu>
        <v-text-field
          v-model="user.address.streetName"
          :rules="[rules.required]"
          label="Улица"
        />
        <v-text-field
          v-model="user.address.buildingNumber"
          :rules="[rules.required]"
          label="Номер здания"
        />
        <v-text-field
          v-model="user.address.city"
          :rules="[rules.required]"
          label="Город"
        />
        <v-text-field
          v-model="user.address.country"
          :rules="[rules.required]"
          label="Страна"
        />
        <v-text-field
          v-model="user.address.zipcode"
          :rules="[rules.required]"
          label="Индекс"
        />
        <v-text-field
          v-model="user.phone"
          :rules="[rules.required]"
          label="Телефон"
        />
        <v-text-field
          v-model="user.website"
          :rules="[rules.required]"
          label="Веб-сайт"
        />
        <v-text-field
          v-model="user.email"
          :rules="[rules.required, rules.email]"
          label="Email"
        />
      </v-form>
    </v-card-text>
    <v-card-actions class="justify-center">
      <v-btn @click="handleCloseEdit" color="error">
        Отмена
      </v-btn>
      <v-btn @click="handleSave" color="primary ml-2">
        Сохранить
      </v-btn>
    </v-card-actions>
  </div>
</template>

<script>
export default {
  name: "UserCardEdit",
  data: () => ({
    valid: true,
    user: {},
    rules: {
      required: value => !!value || 'Обязательное поле',
      email: value => {
        const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        return pattern.test(value) || 'Введен некорректный email'
      },
    },
  }),
  props: {
    userData: Object,
  },
  watch: {
    userData: {
      immediate: true,
      handler(newValue){
        this.user = newValue;
      }
    }
  },
  methods: {
    getGenderString(value) {
      return value === 'male' ? 'Мужской' : 'Женский'
    },
    handleCloseEdit() {
      this.user = this.userData
      this.$emit('closeEdit')
    },
    handleSave() {
      if (this.$refs.form.validate()) {
        // api call
        this.$emit('closeEdit')
      }
    }
  }
}
</script>

<style scoped>

</style>
