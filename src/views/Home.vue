<template>
  <div class="home-view-container">
    <h1>Adopt a new best friend.</h1>
    {{ getAllCats.length }}
    {{ animalsCount }}
    <b-button
      @click="togglePetForm"
      variant="primary"
    > Add New Pet </b-button>
    <b-form
      @submit.prevent="handleSubmitForm"
      v-if="showPetForm"
    >
      <b-form-group
        id="input-group-2"
        label="Pet's Name:"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          type="text"
          v-model="formData.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-3"
        label="Species:"
        label-for="input-3"
      >
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Pet's Age:"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          type="number"
          v-model="formData.age"
          placeholder="Enter age"
          required
        ></b-form-input>
      </b-form-group>

      <b-button
        type="submit"
        variant="primary"
      >Submit</b-button>
      <b-button
        type="reset"
        variant="danger"
      >Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmitForm () {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          age,
          name
        }
      }
      this.addPet(payload)
      // reset the form
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
