<template>
    <h1>Les sorts :</h1>
    <input type="text" id="spell_name_val" v-model="nom" placeholder="Nom">
    <table>
        <tr>
            <th>Nombre d'armes</th>
            <th>Nombre de sorts</th>
        </tr>
        <tr>
            <td>{{ statArme }}</td>
            <td>{{ statSort }}</td>
        </tr>
    </table>
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
   },
   statArme(){
       let value = data.filter(spell => spell[1].startsWith(this.nom));
       let count = 0;
       let countArray = [];
       for (const v of value){
           if (!countArray.includes(v[0])){
               count++;
               countArray.push(v[0]);
           }
       } 
       return count;
   },
   statSort(){
       let value = data.filter(spell => spell[1].startsWith(this.nom));
       let count = 0;
       let countArray = [];
       for (const v of value){
           if (!countArray.includes(v[2])){
               count++;
               countArray.push(v[0]);
           }
       } 
       return count;
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
    margin-left: auto;
    margin-right: auto;
}
</style>
