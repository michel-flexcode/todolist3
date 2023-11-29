<template>
  <div>
    <form @submit.prevent="ajouterElement">
      <label
        >Nom :
        <input v-model="nouvelElement" />
      </label>
      <button type="submit">Sauvegarder</button>
    </form>
  </div>

  <table>
    <thead>
      <tr>
        <th>Nom</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(element, index) in tableau" :key="index">
        <td>{{ element }}</td>
        <td>
          <button @click="supprimerElement(index)">Supprimer</button>
        </td>
      </tr>
    </tbody>
  </table>

  <!-- Afficher le tableau sous forme de texte brut pour le débogage -->
  <pre>{{ tableau }}</pre>
</template>

<script setup>
import TableauComponent from "./TableauComponent.vue";

import { ref } from "vue";

const tableau = ref([]);
const nouvelElement = ref("");

const ajouterElement = () => {
  if (nouvelElement.value.trim() !== "") {
    tableau.value.push(nouvelElement.value.trim());
    nouvelElement.value = "";
  }
};

const supprimerElement = (index) => {
  tableau.value.splice(index, 1);
};
</script>
