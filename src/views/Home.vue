<template>
  <div class="home-view-container">
    <h1>
      Adopt a new best friend
    </h1>
    <h2>
      Cat´s total: {{ getAllCats.length}}
    </h2>
    <h2>
      Animal's total: {{ animalsCount }}
    </h2>
    <br>
    <button class="btn btn-primary mt-3" @click="togglePetForm">
      Add New Pet
    </button>
    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">

      <b-form-group id="input-group-2" label="Pet´s Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="formData.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="exampleInputGroup2" label="Pet's Age:" label-for="exampleInput2">
        <b-form-input
          id="exampleInput2"
          type="number"
          v-model="formData.age"
          required
          placeholder="Enter age" />
      </b-form-group>
      <div class="my-4">
        <b-button type="submit" variant="primary" class="mx-2">Submit</b-button>
        <b-button type="reset" variant="danger" class="mx-2">Reset</b-button>
      </div>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'Home',
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
    handleSubmit () {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      // reset form after submit
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
