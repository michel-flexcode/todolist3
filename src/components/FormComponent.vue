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
        <th>Sélectionner</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(element, index) in tableau" :key="index">
        <td>{{ element }}</td>
        <td>
          <button @click="supprimerElement(index)">Supprimer</button>
        </td>
        <td>
          <input type="checkbox" v-model="tableauSelection[index]" />
        </td>
      </tr>
    </tbody>
  </table>

  <!-- Afficher le tableau sous forme de texte brut pour le débogage -->
  <pre>{{ tableau }}</pre>
</template>

<script setup>
import { ref } from "vue";

const tableau = ref(["Element 1", "Element 2", "Element 3"]);
const nouvelElement = ref("");
const tableauSelection = ref(Array(tableau.value.length).fill(false));

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
