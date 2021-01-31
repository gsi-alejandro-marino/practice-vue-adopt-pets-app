<template>
  <div>
    <h1>{{ species | uppercase }} for Adoption</h1>
    <b-table
      striped
      hover
      :items="pets"
    >
      <template #cell(name)="data">
        <router-link :to="`/pets/${species}/${data.index}`">{{ data.value }}</router-link>
      </template>
    </b-table>
  </div>
</template>

<script>

export default {
  props: {
    species: String,
    pets: Array
  },
  filters: {
    uppercase: function (value) {
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
}
</script>
