<template>
  <v-app>
    <v-main>
      <v-container>
        <!-- TODO используйте v-autocomplete для выбора пользователя -->
        <!--      2. Выбор пользователя-->
        <v-autocomplete
            :items="users"
            item-text="fullname"
            label="User"
            v-model="userSelected"
            return-object
            clearable
            @change="setUser"
        />
        <!-- TODO сделать в отдельном блоке отображение информации о выбранном пользователе с использование v-card -->
        <!--      1. Отображение информации о пользователе-->
        <!-- TODO добавить возможность редактировать данные пользователя -->
        <!--      3. Редактирование пользователя-->
        <user-card
            v-if="hasSelectedUser"
            :user="userSelected"
            @update-user="handleUserUpdate"
        />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import UserCard from "@/components/userCard.vue";

export default {
  name: "App",
  components: {UserCard},

  data: () => ({
    userSelected: {},
    users:[],
  }),

  computed: {
    hasSelectedUser() {
      return this.userSelected && Object.keys(this.userSelected).length > 0;
    }
  },

  created() {
    this.getUsers()
  },

  methods: {
    getUsers() {
      fetch('https://fakerapi.it/api/v1/persons?_locale=ru_RU')
          .then(res => res.json())
          .then(({data}) => {
            this.users = data.map(user => ({
              ...user,
              fullname: `${user.firstname} ${user.lastname}`
            }));
          })
          .catch(err => {
            console.error('Error fetching users:', err);
          });
    },

    setUser(user) {
      this.userSelected = user;
    },

    handleUserUpdate(updatedUser) {
      this.userSelected = updatedUser;
      const index = this.users.findIndex(user => user.id === updatedUser.id);
      if (index !== -1) {
        this.$set(this.users, index, updatedUser);
      }
    }
  },
};
</script>
