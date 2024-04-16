<template>
  <v-card>
    <v-card-title>
      {{isEditing? "Editing" : ""}} {{$props.user.fullname}}
    </v-card-title>

    <v-card-text>
      <user-edit
          v-if="isEditing"
          v-model="editableUser"
      />
      <user-details
          v-else
          :user-details="$props.user"
      />
    </v-card-text>

    <v-card-actions class="justify-space-between">
      <v-btn @click="toggleEditMode">
        {{ isEditing ? 'Cancel' : 'Edit User' }}
      </v-btn>

      <v-btn
          v-if="isEditing"
          color="primary"
          @click="saveUser"
      >
        Save Changes
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
import UserDetails from "@/components/userDetails.vue";
import UserEdit from "@/components/userEdit.vue";

export default {
  name: "UserCard",
  components: {UserEdit, UserDetails},

  props:{
    user: {
      type: Object,
      required: true
    }
  },

  data: () => ({
    isEditing: false,
    editableUser: {}
  }),

  computed:{
    computedFullname(){
      return `${this.editableUser.firstname} ${this.editableUser.lastname}`
    }
  },

  mounted() {
    this.setEditableUser()
  },

  watch: {
    user: {
      handler() {
        this.setEditableUser()
      },
    }
  },

  methods: {
    setEditableUser(){
      this.editableUser = Object.assign({}, this.$props.user)
    },
    toggleEditMode() {
      this.isEditing = !this.isEditing;
    },
    saveUser() {
      this.editableUser.fullname = this.computedFullname
      this.$emit('update-user', this.editableUser);
      this.isEditing = false;
    }
  },
};
</script>