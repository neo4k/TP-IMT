<template>

  <div v-if="currentPersonne">
    {{ currentPersonne.name }}
    {{ currentPersonne.surname }}
    {{ currentPersonne.phone }}
    {{ currentPersonne.city }}

	<br><input type="text" class="" id="id" v-model="currentPersonne.id" name=""/><br>
    <input type="text" class="" id="name" v-model="currentPersonne.name" name=""/><br>
	<input type="text" class="" id="surname" v-model="currentPersonne.surname" name=""/><br>
	<input type="text" class="" id="phone" v-model="currentPersonne.phone" name=""/><br>
	<input type="text" class="" id="city" v-model="currentPersonne.city" name=""/>
  </div>
  <!-- A COMPLETER -->

    <!-- A INCLURE DANS LE FORM -->
    <button class="badge badge-danger mr-2"
      @click="deletePersonne"
    >
      Supprimer
    </button>

    <!-- A INCLURE DANS LE FORM -->
    <button type="submit" class="badge badge-success"
      @click="updatePersonne"
    >
      Modifier
    </button>
    <p>{{ message }}</p>

</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personne",
  data() {
    return {
      currentPersonne: null,
      message: ''
    };
  },
  methods: {
    getPersonne(id) {
	PersonneDataService.get(id)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    updatePersonne() {
      PersonneDataService.update(this.currentPersonne)
      .then(response => {
        this.currentPersonne = response.data;
        console.log(response.data);
        this.message = 'Personne modifiée avec succès!';
      })
      .catch(e => {
        console.log(e);
      });
    },

    deletePersonne() {
      PersonneDataService.delete(this.currentPersonne.id)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
          this.message = 'Personne supprimée avec succès!';
          this.$router.push({ name: "/" });
        })
        .catch(e => {
          console.log(e);
        });
    },
  },
  mounted() {
    this.message = '';
    this.getPersonne(this.$route.params.id);
  }
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
}
</style>
