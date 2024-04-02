<template>
  <div>
    <!--  Сервис placeimg.com, который используется в fakerapi.it на момент написания не работал -->
    <v-img
        src="https://placehold.co/600x400"
        class="user-card-edit__photo"
    />
    <v-card-title>
      {{ fullName }}
    </v-card-title>
    <v-card-text>
      <div class="user-card-edit__value"><span>Пол:</span> {{ getGenderString }}</div>
      <div class="user-card-edit__value"><span>Дата рождения:</span> {{ getBirthdayString }}</div>
      <div class="user-card-edit__value"><span>Адрес:</span> {{ fullAddress }}</div>
      <div class="user-card-edit__value"><span>Телефон:</span> {{ phone }}</div>
      <div class="user-card-edit__value"><span>Email:</span> {{ email }}</div>
      <div class="user-card-edit__value"><span>Веб-сайт:</span> {{ website }}</div>
    </v-card-text>
    <v-card-actions class="justify-center">
      <v-btn @click="handleInitEdit" color="primary">
        Редактировать
      </v-btn>
    </v-card-actions>
  </div>
</template>

<script>
export default {
  name: "UserCardView",
  props: {
    id: Number,
    fullName: String,
    firstname: String,
    lastname: String,
    email: String,
    phone: String,
    birthday: String,
    gender: String,
    address: {
      id: Number,
      street: String,
      streetName: String,
      buildingNumber: String,
      city: String,
      zipcode: String,
      country: String,
      country_code: String,
      latitude: Number,
      longitude: Number,
    },
    website: String,
    image: String,
  },
  computed: {
    getGenderString() {
      return this.gender === 'male' ? 'Мужской' : 'Женский'
    },
    getBirthdayString() {
      return new Date(this.birthday).toLocaleDateString()
    },
    fullAddress() {
      return `${ this.address.zipcode }, ${ this.address.country }, ${ this.address.city },
        ${ this.address.street }, ${ this.address.streetName }, ${ this.address.buildingNumber }`
    }
  },
  methods: {
    handleInitEdit() {
      this.$emit('initEdit')
    }
  }
}
</script>

<style lang="scss" scoped>
.user-card-edit {
  &__photo {
    object-fit: contain;
  }
  &__value {
    span {
      font-weight: bold;
    }
  }
}
</style>
