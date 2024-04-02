<template>
  <v-app>
    <v-main>
      <div class="container">
        <v-autocomplete
            label="Выберите пользователя"
            :items="users"
            item-text="fullName"
            item-value="id"
            return-object
            v-model="selectedUser"
            class="flex-grow-0"
            outlined
        />
        <UserCard v-if="selectedUser" :user="selectedUser" />
        <div v-else>
          Выберите пользователя для просмотра
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import UserCard from "@/components/UserCard";
export default {
  name: "App",
  components: {UserCard},
  data: () => ({
    users: [],
    selectedUser: null
  }),

  mounted() {
    this.getUsers()
  },

  methods: {
    async getUsers() {
      try {
        await fetch('https://fakerapi.it/api/v1/persons?_locale=ru_RU')
          .then((response) => {
            response.json().then(users => {
              this.users = users.data.map(item => {
                return {
                  fullName: `${item.firstname} ${item.lastname}`,
                  ...item
                }
              })
            })
          })
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.wrapper {
  max-width: 960px;
}
</style>
