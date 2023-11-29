<template>
  <div>
    <form @submit.prevent="ajouterElement">
      <label>
        Nom :
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
          <button @click="confirmerSuppression(index)">Supprimer</button>
        </td>
        <td>
          <input type="checkbox" v-model="tableauSelection[index]" />
        </td>
      </tr>
    </tbody>
  </table>

  <!-- Modal de confirmation de suppression -->
  <div v-if="modalSuppression">
    <p>Voulez-vous vraiment supprimer cet élément ?</p>
    <button @click="annulerSuppression">Annuler</button>
    <button @click="validerSuppression">Confirmer</button>
  </div>

  <!-- Afficher le tableau sous forme de texte brut pour le débogage -->
  <pre>{{ tableau }}</pre>
</template>

<script setup>
import { ref } from "vue";

const initialTableau = JSON.parse(localStorage.getItem("tableau")) || [];
const initialTableauSelection =
  JSON.parse(localStorage.getItem("tableauSelection")) || [];

const tableau = ref(initialTableau);
const nouvelElement = ref("");
const tableauSelection = ref(initialTableauSelection);
const indexEnCoursDeSuppression = ref(null);
const modalSuppression = ref(false);

const ajouterElement = () => {
  if (nouvelElement.value.trim() !== "") {
    tableau.value.push(nouvelElement.value.trim());
    nouvelElement.value = "";
    sauvegarderDansLocalStorage();
  }
};

const confirmerSuppression = (index) => {
  indexEnCoursDeSuppression.value = index;
  modalSuppression.value = true;
};

const annulerSuppression = () => {
  indexEnCoursDeSuppression.value = null;
  modalSuppression.value = false;
};

const validerSuppression = () => {
  if (indexEnCoursDeSuppression.value !== null) {
    tableau.value.splice(indexEnCoursDeSuppression.value, 1);
    tableauSelection.value.splice(indexEnCoursDeSuppression.value, 1);
    sauvegarderDansLocalStorage();
    annulerSuppression();
  }
};

const sauvegarderDansLocalStorage = () => {
  localStorage.setItem("tableau", JSON.stringify(tableau.value));
  localStorage.setItem(
    "tableauSelection",
    JSON.stringify(tableauSelection.value)
  );
};
</script>
