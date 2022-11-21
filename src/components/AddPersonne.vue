<template>
  <div class="submit-form">
    <div v-if="!submitted">

		<div class="form-floating mb-3">
			<input type="text" class="form-control" id="id" v-model="personne.id" >
				<label for="floatingInput">Identification</label>
			</div>

		<div class="form-floating mb-3">
			<input type="text" class="form-control" id="name" v-model="personne.name" >
				<label for="floatingInput">Nom de Famille</label>
			</div>

		<div class="form-floating mb-3">
			<input type="text" class="form-control" id="surname" v-model="personne.surname">
				<label for="floatingInput">Prénom</label>
			</div>

		<div class="form-floating mb-3">
			<input type="text" class="form-control" id="phone" v-model="personne.phone" >
				<label for="floatingInput">Téléphone</label>
			</div>

		<div class="form-floating mb-3">
			<input type="text" class="form-control" id="city" v-model="personne.city">
				<label for="floatingInput">Ville</label>
			</div>

        <!-- A COMPLETER -->

      <br><button @click="creerPersonne" class="btn btn-outline-primary">Ajouter</button>
    </div>

    <div v-else>
      <h4>Personne ajoutée avec succès!</h4>
      <button class="btn btn-success" @click="resetForm">Ajouter une nouvelle personne</button>
    </div>
  </div>
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "add-personne",
  data() {
    return {
      personne: {
        id: null,
        name: "",
        surname: "",
        phone: "",
        city: ""
      },
      submitted: false
    };
  },
  methods: {
    creerPersonne() {
      var data = {
        id: this.personne.id,
        name: this.personne.name,
        surname: this.personne.surname,
        phone: this.personne.phone,
        city: this.personne.city,
        
    };

      // A COMPLETER
      PersonneDataService.create(data)
      .then(response => {
          console.log(response.data);
          this.submitted = true;
        })
        .catch(e => {
          console.log(e);
        });
    },
    
    resetForm() {
      this.submitted = false;
      this.personne = {};
    }
  }
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>
