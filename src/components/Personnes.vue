<template>
  
  <ul>
    <li class="list-group-item"
      :class="{ active: id == currentIndex }"
      v-for="(personne, id) in personnes"
      :key="id"
      @click="setActivePersonne(personne, id)"
    >
      {{ personne.surname }} {{ personne.name }}
    </li>
  </ul>

<div v-if="currentPersonne">
<h3>Prénom :</h3>{{ currentPersonne.surname }}
<h3>Nom :</h3>{{ currentPersonne.name }}
<h3>Téléphone :</h3>{{ currentPersonne.phone }}
<h3>Ville :</h3>{{ currentPersonne.city }}

<br>
    <router-link :to="'/personnes/' + currentPersonne.id" class="btn btn-primary">Modifier</router-link>
  </div>
  <div v-else>
    <br />
    <p>Cliquez sur une des personnes pour afficher les détails.</p>
  </div>

</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personnes",
  data() {
    return {
      personnes: [],
      currentPersonne: null,
      currentIndex: -1,
    };
  },
  methods: {
    getPersonnes() {
      PersonneDataService.getAll()
        .then(response => {
          this.personnes = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    setActivePersonne(personne, index) {
      this.currentPersonne = personne;
      this.currentIndex = personne ? index : -1;
    },
  },
  mounted() {
    this.getPersonnes();
  }
};
</script>
