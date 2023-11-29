<script setup>
import FormComponent from "./FormComponent.vue";
</script>

<template>
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
          <input type="checkbox" v-model="tableauSelection[index]" />
        </td>
        <td>
          <button @click="supprimerElement(index)">Supprimer</button>
        </td>
      </tr>
    </tbody>
  </table>

  <!-- Afficher le tableau sous forme de texte brut pour le débogage -->
  <pre>{{ tableau }}</pre>
</template>
