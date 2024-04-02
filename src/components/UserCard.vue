<template>
  <v-card max-width="390">
    <UserCardEdit v-if="isEdit" :user-data="user" @closeEdit="handleUserEdit"/>
    <UserCardView v-else v-bind="user" @initEdit="handleUserEdit" />
  </v-card>
</template>

<script>
import UserCardView from "@/components/UserCardView";
import UserCardEdit from "@/components/UserCardEdit";
export default {
  name: "UserCard",
  components: { UserCardEdit, UserCardView },
  props: {
    user: {
      type: Object,
      required: true,
    }
  },
  data: () => ({
    isEdit: false
  }),
  methods: {
    handleUserEdit() {
      this.isEdit = !this.isEdit
    }
  }
}
</script>
