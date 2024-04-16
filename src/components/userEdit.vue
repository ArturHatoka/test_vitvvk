<template>
  <v-row>
    <v-col cols="6">
      <v-text-field
          label="First Name"
          v-model="userEdit.firstname"
          @input="updateValue"
      />
      <v-text-field
          label="Last Name"
          v-model="userEdit.lastname"
          @input="updateValue"
      />
      <v-text-field
          label="Email"
          v-model="userEdit.email"
          type="email"
          @input="updateValue"
      />
      <v-text-field
          label="Phone"
          v-model="userEdit.phone"
          type="phone"
          @input="updateValue"
      />
      <v-text-field
          label="Website"
          v-model="userEdit.website"
          @input="updateValue"
      />
    </v-col>
    <v-col cols="6">
      <v-row>
        <v-col cols="6">
          <v-menu
              :close-on-content-click="false"
              transition="scale-transition"
              offset-y
              min-width="auto"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                  v-model="userEdit.birthday"
                  label="Birthday"
                  prepend-icon="mdi-calendar"
                  readonly
                  v-bind="attrs"
                  v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker
                v-model="userEdit.birthday"
                min="1950-01-01"
                @change="updateValue"
            />
          </v-menu>
        </v-col>
        <v-col cols="6">
          <v-radio-group
              v-model="userEdit.gender"
              row
          >
            <v-radio
                label="Male"
                value="male"
            ></v-radio>
            <v-radio
                label="Female"
                value="female"
            ></v-radio>
          </v-radio-group>
        </v-col>
      </v-row>
      <v-text-field
          label="Country"
          v-model="userEdit.address.country"
          @input="updateValue"
      />
      <v-text-field
          label="City"
          v-model="userEdit.address.city"
          @input="updateValue"
      />
      <v-row>
        <v-col cols="6" class="pb-0">
          <v-text-field
              label="Street"
              v-model="userEdit.address.street"
              @input="updateValue"
          />
        </v-col>
        <v-col cols="6" class="pb-0">
          <v-text-field
              label="Zipcode"
              v-model="userEdit.address.zipcode"
              @input="updateValue"
          />
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="6" class="pt-0">
          <v-text-field
              label="Longitude"
              v-model="userEdit.address.longitude"
              @input="updateValue"
          />
        </v-col>
        <v-col cols="6" class="pt-0">
          <v-text-field
              label="Latitude"
              v-model="userEdit.address.latitude"
              @input="updateValue"
          />
        </v-col>
      </v-row>

    </v-col>
  </v-row>
</template>
<script>
export default {
  name: 'userEdit',
  props: {
    value:{
      required: true,
      type: Object,
    }
  },
  data() {
    return {
      userEdit: this.value,
    };
  },
  methods: {
    updateValue() {
      this.$emit('input', this.userEdit);
    }
  },
  watch: {
    value(newValue) {
      this.userEdit = newValue;
    }
  }
}
</script>