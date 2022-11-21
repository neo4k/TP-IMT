<template>

	<div v-if="currentPersonne">
		
        <br>
			<div class="form-floating mb-3">
				<input type="text" class="form-control" id="id" v-model="currentPersonne.id" >
					<label for="floatingInput">Identification</label>
				</div>
			<div class="form-floating mb-3">
				<input type="text" class="form-control" id="name" v-model="currentPersonne.name" >
					<label for="floatingInput">Nom de Famille</label>
				</div>

			<div class="form-floating mb-3">
				<input type="text" class="form-control" id="surname" v-model="currentPersonne.surname">
					<label for="floatingInput">Prénom</label>
				</div>

			<div class="form-floating mb-3">
				<input type="text" class="form-control" id="phone" v-model="currentPersonne.phone" >
					<label for="floatingInput">Téléphone</label>
				</div>

			<div class="form-floating mb-3">
				<input type="text" class="form-control" id="city" v-model="currentPersonne.city">
					<label for="floatingInput">Ville</label>
				</div>
		
	</div>

    <!-- A INCLURE DANS LE FORM -->
    <button class="btn btn-danger" @click="deletePersonne">
      Supprimer
    </button>

    <!-- A INCLURE DANS LE FORM -->
    <button type="submit" class="btn btn-warning" @click="updatePersonne"> Modifier </button>
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
