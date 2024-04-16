<template>
  <v-card-text>
    <v-row>
      <v-col cols="6" class="d-flex flex-column">
        <span>Birthday: {{ userDetails.birthday }}</span>
        <span>Gender: {{ userDetails.gender }}</span>
        <span>Email: <a :href="'mailto:'+userDetails.email">{{ userDetails.email }}</a></span>
        <span>Phone: <a :href="'tel:'+userDetails.phone">{{ userDetails.phone }}</a></span>
        <span>Website: <a :href="userDetails.website" target="_blank" rel="noopener">{{ userDetails.website }}</a></span>
      </v-col>
      <v-col cols="6" class="d-flex flex-column">
        <span>Country: {{ userDetails.address.country }} {{ userDetails.address.county_code }}</span>
        <span>City: {{ userDetails.address.city }}</span>
        <span>Street: {{ userDetails.address.street }}</span>
        <span>Zipcode: {{ userDetails.address.zipcode }}</span>
        <span>Coords: {{ userDetails.address.longitude }} {{ userDetails.address.latitude }}</span>
      </v-col>
    </v-row>
  </v-card-text>
</template>
<script>
export default {
  name: 'userDetails',
  props:{
    userDetails:{
      required: true,
      type: Object
    }
  }
}
</script>