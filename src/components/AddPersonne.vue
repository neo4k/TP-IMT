<template>
  <div class="submit-form">
    <div v-if="!submitted">

	<br><input type="text" class="" id="id" v-model="personne.id" name="" placeholder="ID"/><br>
    <input type="text" class="" id="name" v-model="personne.name" name="" placeholder="NOM"/><br>
	<input type="text" class="" id="surname" v-model="personne.surname" name="" placeholder="SURNOM"/><br>
	<input type="text" class="" id="phone" v-model="personne.phone" name="" placeholder="TELEPHONE"/><br>
	<input type="text" class="" id="city" v-model="personne.city" name="" placeholder="VILLE"/>
      <!-- A COMPLETER -->

      <br><button @click="creerPersonne" class="btn btn-success">Ajouter</button>
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
