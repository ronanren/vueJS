<template>
    <h1>Les sorts :</h1>
    <input type="text" id="spell_name_val" v-model="nom" placeholder="Nom">
    <table>
        <tr>
            <th>Arme</th>
            <th>Nom</th>
            <th>Sort</th>
            <th>Ecole</th>
            <th>Classe</th>
        </tr>
        <tr v-for="spell in spellSearch" :key="spell[1]">
            <SpellView :spell="spell"/>
        </tr>
    </table>
</template>

<script>
import SpellView from './components/SpellView.vue'
import data from './assets/data.min.js'
/* eslint-disable */

export default {
  name: 'App',
  components: {
    SpellView
  },
  data: function() {
      return {
          nom: ""
      }
  },
  computed: {
   spellSearch(){
       return data.filter(spell => spell[1].startsWith(this.nom));
   }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
table {
    margin-top: 25px;
}
</style>
